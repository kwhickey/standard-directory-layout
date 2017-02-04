encompasses end-to-end workflows, that may be chained together. Things like 
- build (build.sh, build.bat, build.ps1, build.msbuild, etc.)
- deploy
- bake (provision?)

Initial step is to determine the environment, and load all environment-specific-values (e.g. importing props)
Run through whole flow (complete union of all possible tasks) every time. Tasks will be turned off/on by EnvironmentValues
- Guard tasks that are known to be negated in certain Envs with a negation property check: <DoTask1 Condition="'$(IsTask1Negated)' != ''">exec ../Provision/<aspect>/Default/<thing>/thing.target
 (!) There is a risk of running provisioning that is not meant for production if the Default task is renamed, and so the a production negation does not take effect
	 - A way to mitigate this could be that Production is the default. Any additions not in production are added as additions in other envs. 
	 - May still want an EnvironmentValues/Default folder though, since this is dealing with singular environments, not EnvTypes
       - Guard tasks that are known to NOT have a default, and only need to be run for special envs they're added for with an existence check for the <thing> under the <env> folder: <DoTask1 Condition="Exists(../Provision/<aspect>/$(EnvironmentName)/<thing>">