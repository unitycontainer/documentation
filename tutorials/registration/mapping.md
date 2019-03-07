---
uid: Tutorial.Registration.Mapping
title: Type Mapping
---

# Type Mapping

In service oriented architecture components expose services through well known contracts. In `C#` terms the contracts are the interfaces these components and services are exposing. So when we say service type, in most of the cases, we mean the interfaces implementing the contract. And the components are called Implementation types.

Unity allows to publish these components and make all the contracts they implement available to clients to consume. This publishing and "advertisement" is done by registering types and interfaces (contracts) associated with components.

Type mappings provide mechanism for developer to associate _Service Type_ with _Implementation Type_.