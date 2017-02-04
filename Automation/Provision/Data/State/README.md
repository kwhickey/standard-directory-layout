tasks that run to ensure state of an environment is consistent with data stored in the corresponding EnvironmentValues folder for an env

Holds a `Default` folder, which contains the default or base definition of any state-data-provisioning script

Also would hold a folder for each "EnvType" (could be "Development", "Testing", "Staging", "Building", "Production", etc.), where an environment-specific version of that file could be defined. Reasons for doing this are:
- Negate the need to process the "thing" for that particular environment (skip it)
- Add additional state-data-provisioning steps or processing for that particular environment
- Override default state-data-provisioning steps or processsing definitions for that particular environement