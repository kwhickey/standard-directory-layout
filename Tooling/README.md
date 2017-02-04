This would hold any apps or utilities or tools or helpers that are NOT shipped to production, but aid in the development process.

Examples might be
- A code-generator that reverse engineers code (e.g. from the database (Entity Framework POCO generators for example), or UML models, a DSL, etc.) 
- Script that scrubs data perhaps, or cleanly deletes some data from a dev/test db, or builds up test data
- Some kind of converter, maybe it parses a set of files in one format and converts them to another (XML to JSON? MSBuild properties to PowerShell properties?)

These should be one-off tools that are run by a person. Things that are routinely run as part of automation should likely be filed away under the Automation folder.