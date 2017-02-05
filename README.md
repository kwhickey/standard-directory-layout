# Overview
_**standard-directory-layout**_: A good starting layout for source code in a software project that separates concerns and leaves room for growth in the future.

# Adding New Technologies
The original structure on the `master` branch is intended to be generic, and apply as a starting point for any project with any solution stack. Subtle changes may need to take place from the generic structure based on the conventions of your chosen solution stack or language. For instance:
* to word casing (upper/lower, uderscores, PascalCased, camelCased, etc.) may need to take place, 
* and possibly some new or substituted folders

If you want to templatize for a specific solution stack, which will add folders/conventions unique to it, **<u>create a branch for that technology or language</u>** *(An example already is the `sqlserver` branch adds in database folder structure for tracking source-files that help build up a SQL Server database).*

If the branches are kept sufficiently distinct, where a single concern is added to its own branch, then a starter project template for a full solution stack could theoretically be built-up by merging together branches for the chosen technologies.


<br/><br/><br/>
<p align="right"><sub><em>NOTE: Originally "forked" from GitHub: <a href="https://github.com/kwhickey/standard-directory-layout">kwhickey/standard-directory-layout</a></sub></p>
