If there are EnvironmentVariables which are good defaults for most/all environments, then they should be declared in a file under here, and then imported during some provisioning/configuration Task so that they will be used as the baseline (default) value for all environments.

If not defined here, then the "default" value will be whatever is hard-coded into the source-controlled files that contain variable data. Note that these may still be overridden/replaced by environment-specific variable values that are declared in a file under one of the `../<env>` folders, given that the file is imported during some provisioning/configuration Task.

*NOTE: Undecided whether this needs to be the full set of default env-values, and if so, do envs import this then override? Or, should the thing-provisioning tasks have default values?* 

*Leaning towards full default set here, then can be imported+overridden*