<pre>

/Automation
  /Workflow # encompasses end-to-end workflows, that may be chained together. Things like build, deploy, bake (provision?)
    # Initial step is to determine the environment, and load all environment-specific-values (e.g. importing props)
    # Run through whole flow (complete union of all possible tasks) every time. Tasks will be turned off/on by EnvironmentValues
    #   - Guard tasks that are known to be negated in certain Envs with a negation property check: <DoTask1 Condition="'$(IsTask1Negated)' != ''">exec ../Provision/<aspect>/Default/<thing>/thing.target
    #     (!) There is a risk of running provisioning that is not meant for production if the Default task is renamed, and so the a production negation does not take effect
    #         - A way to mitigate this could be that Production is the default. Any additions not in production are added as additions in other envs. 
    #         - May still want an EnvironmentValues/Default folder though, since this is dealing with singular environments, not EnvTypes
    #   - Guard tasks that are known to NOT have a default, and only need to be run for special envs they're added for with an existence check for the <thing> under the <env> folder: <DoTask1 Condition="Exists(../Provision/<aspect>/$(EnvironmentName)/<thing>">
  /Provision
	/Infrastructure # establish or re-establish (nuke and pave?) an infrastructure-thing
	  /Default
	    /<thing>
	      /thing.targets # or thing.ps1, or thing.cmd, or thing.sh, thing.sql
	  /EnvType1 # e.g. Development, Test, Staging, Build, Production, etc. Only necessary to negate default, or for special additions for that env
	  /EnvType2
	/Software # perform installation of a software-thing. e.g SQL Server (probably all envs), or Visual Studio (probably just under "Development" EnvType)
	  /Default
	    /<thing>
	      /thing.targets # or thing.ps1, or thing.cmd, or thing.sh, thing.sql
	  /EnvType1 # e.g. Development, Test, Staging, Build, Production, etc. Only necessary to negate default, or for special additions for that env
	  /EnvType2
	/Data
	  /Configuration # perform configuration of the thing, probably consuming EnvironmentValues to do so
	    /Default
	      /<thing>
	        /thing.targets # or thing.ps1, or thing.cmd, or thing.sh, thing.sql
	    /EnvType1 # e.g. Development, Test, Staging, Build, Production, etc. Only necessary to negate default, or for special additions for that env
	    /EnvType2
	  /State # tasks that run to ensure state of an environment is consistent with data stored in the corresponding EnvironmentValues folder for an env
	    /Default
	      /<thing>
	        /thing.targets # or thing.ps1, or thing.cmd, or thing.sh, thing.sql
	    /EnvType1 # e.g. Development, Test, Staging, Build, Production, etc. Only necessary to negate default, or for special additions for that env
	    /EnvType2
  /EnvironmentValues
    /Default # undecided whether this needs to be the full set of default env-values, and if so, do envs import this then override? Or, should the thing-provisioning tasks have default values? Leaning towards full default set here, then can be imported+overridden
      /Workflow
        /<flow>
          /flow.props
      /Provision
        /Infrastructure
          /<thing>
            /thing.props 
        /Software
          /<thing>
            /thing.props 
        /Data
          /Configuration
            /<thing>
              /thing.props 
          /State
            /<thing>
              /thing.props 
    /<env>
      /Workflow
        /<flow>
          /flow.props # should *attempt* (without failure) to import the default variable file at `/Automation/EnvironmentVariables/Default/Workflow/flow/flow.props` , then override variables and/or add anything extra
      /Provision
        /Infrastructure
          /<thing>
            /thing.props # should *attempt* (without failure) to import the default variable file at `/Automation/EnvironmentVariables/Default/Infrastructure/thing/thing.props` , then override variables and/or add anything extra
        /Software
          /<thing>
            /thing.props # should *attempt* (without failure) to import the default variable file at `/Automation/EnvironmentVariables/Default/Software/thing/thing.props` , then override variables and/or add anything extra
        /Data
          /Configuration
            /<thing>
              /thing.props # should *attempt* (without failure) to import the default variable file at `/Automation/EnvironmentVariables/Default/Data/Configuration/thing/thing.props` , then override variables and/or add anything extra
          /State
            /<thing>
              /thing.props # hould *attempt* (without failure) to import the default variable file at `/Automation/EnvironmentVariables/Default/Data/State/thing/thing.props` , then override variables and/or add anything extra

</pre>