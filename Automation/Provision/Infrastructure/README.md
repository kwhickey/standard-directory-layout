establish or re-establish (nuke and pave?) an infrastructure-thing

Holds a `Default` folder, which contains the default or base definition of any infrastructure-provisioning script

Also would hold a folder for each "EnvType" (could be "Development", "Testing", "Staging", "Building", "Production", etc.), where an environment-specific version of that file could be defined. Reasons for doing this are:
- Negate the need to process the "thing" for that particular environment (skip it)
- Add additional infrastructure-provisioning steps or processing for that particular environment
- Override default infrastructure-provisioning steps or processsing definitions for that particular environement