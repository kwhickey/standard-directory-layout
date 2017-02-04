Holds files defining default variable (aka property) values to be used in all environments, for particular workflows.
- The variables are stored in technology-specifc files (e.g. for a "Build" flow, Build.props or Build.psd1 or Build.properties or Build.ini or Build.bat or Build.sh)
- The file, if a complete set of environment-specific variables, can reside at this level of the directory (e.g. Flow01_PlaceholderToBeRenamed.props)
- If a flow requires more than one set of variables files, they should be grouped into a subfolder named after the flow (e.g. `.\Flow01_PlaceholderToBeRenamed\*.*`) 