perform configuration of the thing, probably consuming EnvironmentValues to do so

Holds a `Default` folder, which contains the default or base definition of any configuration script
Also would hold a folder for each "EnvType" (could be "Development", "Testing", "Staging", "Building", "Production", etc.), where an environment-specific version of that file could be defined. Reasons for doing this are:
- Negate the need to process the "thing" for that particular environment (skip it)
- Add additional configuration steps or processing for that particular environment
- Override default configuration steps or processsing definitions for that particular environement