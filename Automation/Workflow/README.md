# Overview

Root folder for storing scripts that encompasses end-to-end workflows that need to be kicked off, which may be chained together.

Often these are things which may be conducted or orchestrated by a Continuous Integration (CI) or Continuous Delivery (CD) server pipeline (e.g. Jenkins).   
- build (build.sh, build.bat, build.ps1, build.msbuild, etc.)
- deploy
- bake (provision?)

Or the top-level artifact which encapsulates a series of tasks that a configuration management automation tool may execute.
- Ansible Playbook
- Chef Recipe
- Puppet Module

*NOTE: Still deciding if this metaphor makes sense for CM automation tool artifacts like this. Need to test-drive this on various CM tools to see if it holds water, or if a different directory/directory-structure needs to house those artifacts*

# How Workflows Run

1. During execution of a workflow, the initial step is to determine the environment that the instantiation is targeting.
   - *This should be passed in as an argument to the call to execute the workflow.*
2. Once the environment is determined, environment-specific overrides or negations of the *Task(s)* to be executed in a workflow may be loaded.
   - If not found, the workflow will fallback to the default *Task* definition
3. With the environment determined, load the environment-context by importing any environment variables defined for the targeted environment (and required by the executed workflow and *Tasks* it encompasses)
4. Run through whole flow (complete union of all possible *Tasks* defined in the workflow) every time.
5. Tasks that are *specific* to only one or a few environments can be appended to the set of tasks to runcan be turned off/on by EnvironmentValues
6. Tasks defined that are not applicable for a targeted environment can be "turned off" (negated) by specifying a negation variable in an appropriate environment variables file for that environment which is imported as part of the workflow
   - Guard tasks that are known to be negated in certain Envs with a negation variable check: 
     - e.g. `<DoTask1 Condition="'$(IsTask1Negated)' != ''">exec ../Provision/<aspect>/Default/<thing>/thing.target`
     - (!) There is a risk of running provisioning that is not meant for production if the Default task is renamed, and so the a production negation does not take effect
	   - A way to mitigate this could be that Production is the default. Any additions not in production are added as additions in other envs. 
	   - May still want an EnvironmentValues/Default folder though, since this is dealing with singular environments, not EnvTypes
   - Guard tasks that are known to NOT have a default, and only need to be run for special envs they're added for with an existence check for the &lt;thing&gt; under the &lt;env&gt; folder:
     - e.g. `<DoTask1 Condition="Exists(../Provision/<aspect>/$(EnvironmentName)/<thing>">`