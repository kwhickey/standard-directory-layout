# Overview
* A folder would exist for each database that is to be hosted in this logical SQL Server instance. 
* This folder would also server as the project folder for a SQL Server Data Tools (SSDT) Database project, and so there would be a `.sqlproj` file beneath each database folder.
* The `*.sln` solution file(s) that group the database projects together would remain in this folder.

# Folder/Subfolder Structure Explanation
*NOTE: The folder structure in the `db01_PlaceholderToBeRenamed` folder and that follows is a *union* of a customized folders structure used on past projects with `DBDeploy` and custom scripting, with the folder structure used by SQL Server Data Tools "Datbase Projects"*
 - *Because of this there are probably some redundant folders that need to be consolidated in the final strucutre (depending on the database change management strategy employed by the project team). Examples of conflicts or duplicative folders are:*
   - `db01_PlaceholderToBeRenamed\Baseline\Tables` and `db01_PlaceholderToBeRenamed\Tables`
   - `db01_PlaceholderToBeRenamed\Baseline\Deltas` and `db01_PlaceholderToBeRenamed\Tables`
   - `db01_PlaceholderToBeRenamed\Baseline\Data` and `db01_PlaceholderToBeRenamed\DataScripts`
   - `db01_PlaceholderToBeRenamed\Baseline\Security\**` and `db01_PlaceholderToBeRenamed\Security`

*Current folder structure underneath each database folder, folder descriptions, and options within that folder structure:*

```
C:.
\---db01_PlaceholderToBeRenamed  # The name of the database
    +---Baseline                 # The set of files invoked only once, when the database is initially created (or re-created as part of a nuke-and-pave)
    |   +---Data                 # The reference data and any seed data to load as part of the initial creation or re-creation of the database
    |   +---Deltas               # The set of Deltas to run *after* the initial set of tables are created, to modify those tables. Databases can be "re-baselined" by archiving a set of active Delta scripts (from ..\Deltas) in this folder
    |   +---Security
    |   |   +---Roles            # The initial set of database-level Roles to create, which encapsulate permission grants/denies
    |   |   +---Schemas          # The initial set of database schemas to create in this database
    |   |   \---Users            # The initial set of Users to create in this database
    |   \---Tables               # The initial set of Tables to create in this database
    +---CheckConstraints         # The active set of CHECK constraints that will be used for this database (typically all existing are nuked, and then re-paved with these)
	+---DataScripts              # The set of DataScripts to run. Unknown whether these need to be idempotent and re-runnable, or if they are only run once (according to SSDT Database Projects)
    +---Deltas                   # The registry of incremental change scripts that have been created for this database. The numbered deltas are compared against an active database to determine which ones need to run. These would also run only after Baseline scripts were first run.
    +---Functions                # The active set of Functions that will be used for this database (typically all existing are nuked, and then re-paved with these)
    +---Security                 # When using SSDT Database Projects, scripts in here define the users, roles (and possibly schemas?) for a database
    +---Snapshots                # When using SSDT Database Projects, this will hold historical *.dacpac snapshots of the state of a database schema at a point in time
    +---Storage                  # When using SSDT Database Projects, this will hold scripts that define the physical layout of this database, in terms of files and filegroups
    +---StoredProcedures         # The active set of Stored Procedures that will be used for this database (typically all existing are nuked, and then re-paved with these). Note, when using SSDT Database Project, this folder is actually called "Stored Procedures", with a space. It is unknown if that can be configured
    +---Synonyms                 # The active set of Synonyms that will be used for this database (typically all existing are nuked, and then re-paved with these). Note, when using SSDT Database Project, this folder is actually called "Stored Procedures", with a space. It is unknown if that can be configured
    +---Tables                   # When using SSDT Database Projects, the complete definition of all active Tables in this database
    +---Triggers                 # The active set of Triggers that will be used for this database (typically all existing are nuked, and then re-paved with these) 
    +---Types                    # The active set of Types that will be used for this database (typically all existing are nuked, and then re-paved with these)
    \---Views                    # The active set of Views that will be used for this database (typically all existing are nuked, and then re-paved with these)
```

## Baseline Folder Script Order
*NOTE: When employing the custom strategy that uses the `Baseline` folder's files to create the baseline database instance, the order of execution is*
1. Security\Schemas
2. Tables
3. Security\Roles
4. Security\Users
5. Deltas (will bring the baseline set of tables up to date to the latest delta in this folder)
