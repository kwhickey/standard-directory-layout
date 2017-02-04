```
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
              /thing.props # should *attempt* (without failure) to import the default variable file at `/Automation/EnvironmentVariables/Default/Data/State/thing/thing.props` , then override variables and/or add anything extra
```

<table>
  <thead>
  <tr>
    <th>Term</th>
    <th>Context</th>
    <th>Description</th>
    <th>Synonyms</th>
    <th>Examples</th>
    <th>Notes</th>
  </tr>
  <thead>
  <tbody>
  <tr>
    <td>Environment Type</td>
    <td> </td>
    <td>An intended purpose for which a hosted ArCADIE system (instance) is to be used.</td>
    <td><ul><li>Environment Type</li><li>EnvType</li></ul></td>
    <td>
      <ul>
        <li>Production</li>
        <li>Staging</li>
        <li>Testing</li>
        <li>Building</li>
        <li>Development</li>
      </ul>
    </td>
    <td>Should conform to the "enum" of values commented in our &lt;env&gt;.msbuild files next to the &lt;EnvType&gt;property.</td>
  </tr>
  <tr>
    <td>Environment Instance</td>
    <td>An instance of an environment type</td>
    <td>A fully operational incarnation of the ArCADIE system.</td>
    <td><ul><li>Environment Instance</li><li>Instance</li><li>Environment</li><li>Site</li></ul></td>
    <td>
      <ul>
        <li>BLD01</li>
        <li>INT01</li>
        <li>TST01</li>
        <li>TST05</li>
        <li>STG01</li>
        <li>STG02</li>
      </ul>
    </td>
    <td>It is possible that all components that make up an environment be hosted on a single "Node" (e.g. dev box), so an Environment Instance could equate to a "Node" in some caseIt is also possible that two environment instances, or components of each, are sharing the same machine. e.g. stage01 and stage02 share a web server, and also share a db server.</td>
  </tr>
  <tr>
    <td>Machine</td>
    <td>Machine in an environment instance</td>
    <td>A server or virtual machine with a identifiable name and network (IP) address.</td>
    <td><ul><li>Machine</li><li>Node</li><li>Box</li><li>VM</li><li>Server</li><ul></td>
    <td>
      <ul>
        <li>PROJ-TST-01-APP</li>
        <li>PROJ-TST-01-DB</li>
        <li>PROJ-TST-01-DW</li>
        <li>PROJ-STG-02-APP</li>
      </ul>
    </td>
    <td> </td>
  </tr>
  <tr>
    <td>Aspect</td>
    <td>Aspect being provisioned</td>
    <td>The aspect of system or operational entity that is being automated</td>
    <td> </td>
    <td><ul><li>Infrastructure</li><li>Software</li><li>Data</li><li><ul><li>Configuration Data</li><li>State Data</li></ul></li></ul></td>
    <td>This can be hierarchical. E.g. aspects having sub-aspects or groupings beneath them</td>
  </tr>
  <tr>
    <td>Component</td>
    <td>A Component in an Environment Instance</td>
    <td>An independent and separately installable/configurable piece of a runtime operation that plays an important part. Typically these are configuration items or data items that are under "configuration control" according to our Configuration Managment process.</td>
    <td><ul><li>Component</li><li>Role</li><li>Thing</li></ul></td>
    <td>
      <ul>
        <li>IIS</li>
        <li>SQL Server database server</li>
        <li>Visual Studio</li>
        <li>SiteMinder</li>
        <li>Icon Files</li>
      </ul>
    </td>
    <td>Depending on how detailed your automation needs to get, and at what degree things vary at that level (on different machines, envs), this component could be made of other components to automate.</td>
  </tr>
  <tr>
    <td>Concern</td>
    <td>A concern of a component</td>
    <td>The concern or sub-specialty of the component to automate/configure/provision</td>
    <td> </td>
    <td>
      <ul>
        <li>The IIS Site</li>
        <li>Global Web.config's appSettings</li>
        <li>The server certificates</li>
      </ul>
    </td>
    <td>It's really relative to how big the component/thing is being provisioned. That component or thing may break down into many other components or things, or concerns about those components or things.In terms of where these fall into standard directory layout, they may be "top-level" with other component-level things, or may fall undereath a component.</td>
  </tr>
  <tr>
    <td>Task</td>
    <td>A Task in a Workflow</td>
    <td>An executable "unit" that performs some work (e.g. in a workflow)</td>
    <td> </td>
    <td><ul><li>InstallXyz (where Xyz may be some software)</li><li>Copy</li><li>Delete</li><li>Compile</li><li>Log</li><li>Zip/Unzip</li></ul></td>
    <td>The "unit" of a task may be very low-level, or may be a higher-order task that is really performing a collection of lower-level tasks together to accomplish a higher-level Task.In this case, the distinction is a bit confusing between Workflow (as comprising several tasks) and a higher-order Task. A Workflow generally chains together logically different operations, and is likely not atomic. Whereas a higher-order Task should still be mostly an atomic operation (either all-succeeding, or all-failing).</td>
  </tr>
  </tbody>
</table>
