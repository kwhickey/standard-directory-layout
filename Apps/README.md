Applications reside in their own subfolder within this folder that share these characteristics:
- They are intended to be built and deployed to production
- logically fall under the concern that this source code repository covers,
- which have some kind of compile-time or run-time dependency on each other

They could be background (windows service or daemon) apps, web apps, console apps, desktop apps, web services, etc.

Solution files (`*.sln`) would ideally be placed at the top-level of this directory, and aggregate one or more of the applications in subfolders of this directory into a logical grouping that are managed in a single Visual Studio session.