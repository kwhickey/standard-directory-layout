Holds files defining default variable (aka property) values to be used by all environments, for configuration.
- The variables are stored in technology-specifc files (e.g. for a "Thing" being configured, Thing.props or Thing.psd1 or Thing.properties or Thing.ini or Thing.bat or Thing.sh)
- The file, if a complete set of environment-specific variables, can reside at this level of the directory (e.g. Thing01_PlaceholderToBeRenamed.props)
- If a thing requires more than one set of variables files, they should be grouped into a subfolder named after the thing (e.g. `.\Thing01_PlaceholderToBeRenamed\*.*`) 
