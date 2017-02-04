The folder to hold automated tests for the project. The directory structures in here should mirror the source code directory structure from the top-level (root) folder.
Tests should show up in the same relative path under here that they do in the source directory tree. For instance:
   
   /App/MyCoolApp/Code/FeatureN/ProcessDataForFeatureN.cs
   
would have tests in:

   /Tests/App/MyCoolApp/Code/FeatureN/ProcessDataForFeatureNTests.cs

And if `ProcessDataForFeatureN.cs` was in a CSharp project that made assembly `Some.FullyQualified.Namespace.MyCoolApp.Code.dll`, then a good convention to follow would be that the `ProcessDataForFeatureNTests.cs` test class be in a project that yields DLL `Some.FullyQualified.Namespace.MyCoolApp.Code.Tests.dll`