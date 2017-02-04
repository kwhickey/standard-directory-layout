perform installation of a software-thing. e.g SQL Server (probably all envs), or Visual Studio (probably just under "Development" EnvType)

Holds a `Default` folder, which contains the default or base definition of any software-provisioning script
Also would hold a folder for each "EnvType" (could be "Development", "Testing", "Staging", "Building", "Production", etc.), where an environment-specific version of that file could be defined. Reasons for doing this are:
- Negate the need to process the "thing" for that particular environment (skip it)
- Add additional software-provisioning steps or processing for that particular environment
- Override default software-provisioning steps or processsing definitions for that particular environement