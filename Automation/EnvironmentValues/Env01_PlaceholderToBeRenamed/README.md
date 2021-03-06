Define environment-specific variables (aka properties) in the folder structures below this folder.

The environment-specific files under here containing variables for a particular aspect and component should *attempt* to import their default variables for that aspect and component in the `/Automation/EnvironmentVariables/Default/Aspect/Component/*.*` file. This attempt should be fault-tolerant, and not fail if the default file(s) are not found, since the component may be so unique in each environment that there is no default values.

Importing default values ensures each environment starts with the same baseline of default variable values. Then (technology-permitting), those default variable values can be overridden by re-declaring them in a specific environment.