---
uid: Specification.Unity
title: Unity Container Specification
---

1. <xref:Specification.Introduction>
1. Terms and Definitions
    1. Injection
    1. Dependency
    1. Contract
        * Type
        * Name
    1. Metadata
    1. Lifetime
1. Workflow
    1. Setup
        1. Creating Container
            1. Root
            1. Scopes
        1. Type Contracts
            1. Implicit
            1. Mapping
            1. Explicit
                * Instance
                * Factory
                * Type
        1. Provide Services
            1. Locate Contract
                1. Existing
                1. Hierarchical
                1. None
                    1. Create Locally
                    1. With the registration
                    1. At the root
            1. Execute contract
                1. From lifetime manager
                1. From pipeline
        1. Manage created objects



# Unity Container Specification

## 1 Introduction

[!include [Introduction](1-introduction.md)]

[!include [Terms and Definitions](2-definitions.md)]

## 3 Workflow

[!include [Workflow](workflow.md)]

[!code-csharp [Overrides](../src/Abstractions/src/Dependency/Injection/Abstracts/InjectionMember.cs#Overrides)]


[!code-csharp [Implementation](../src/Abstractions/src/Dependency/Injection/Abstracts/InjectionMember.cs#Implementation)]
