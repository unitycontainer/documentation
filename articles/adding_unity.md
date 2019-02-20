# Adding Unity to Your Application
Unity is designed to support a range of common scenarios for resolving instances of objects that, themselves, depend on other objects or services. However, you must first prepare your application to use Unity. The following procedure describes how to include the necessary assemblies and elements in your code.
## To prepare your application
Before you can install Unity you need to decide if you want to reference packages individually ([Abstractions](https://www.nuget.org/packages/Unity.Abstractions/), [Container](https://www.nuget.org/packages/Unity.Container/)) or use composite [Unity]([Unity](https://www.nuget.org/packages/Unity/)) package. These are certain costs and benefits for each decision.

#### Referencing composite package
 Referencing [Unity]([Unity](https://www.nuget.org/packages/Unity/)) is more appropriate in case of small(ish) project, when everything is contained within one solution. Upgrading such solution is trivial with the help of NuGet Manager.

#### Referencing individual packages
Main benefit of referencing [Abstractions](https://www.nuget.org/packages/Unity.Abstractions/) and [Container](https://www.nuget.org/packages/Unity.Container/) packages individually is when it is used in large project spanning multiple solutions, modules, and project files. 

Normally modular systems have one main application/module with boot-loader responsible for initializing environment, and number of modules loaded by it ([Prism library](https://prismlibrary.github.io/) for example). This boot loader is required to reference both [Abstractions](https://www.nuget.org/packages/Unity.Abstractions/) and [Container](https://www.nuget.org/packages/Unity.Container/) packages.

In such systems modules are created and distributed by various teams and departments and synchronization between these might be a challenge. This is where Unity comes in. 
As stated elsewhere on this site [Unity.Abstractions](https://www.nuget.org/packages/Unity.Abstractions/) contains all declarations required by Unity to operate. Because of that modules could only reference one assembly: [Unity.Abstractions](https://www.nuget.org/packages/Unity.Abstractions/) removing requirement to be recompiled whenever Unity container engine has changed. 

Given that spec changes very infrequently and [Unity.Abstractions](https://www.nuget.org/packages/Unity.Abstractions/) package stays the same most of the time it provides big benefit in terms of saving development time and money.

## Adding Unity to project
Unity container is distributed via NuGet and could be added to a project with the help of NuGet manager of by executing command:
```
Install-Package Unity

or

Install-Package Unity.Abstractions
Install-Package Unity.Container
```

If you wish to use [Floating version references](https://docs.microsoft.com/en-us/nuget/consume-packages/package-references-in-project-files#floating-versions) it is recommended to lock in the minor and major versions and only allow patch version to slide:

```
<PackageReference Include="Unity.Container" Version="5.9.*" />
```
doing so will guarantee that no breaking changes caught you of guard.



