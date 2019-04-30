---
uid: Tutorial.Mapping
title: Type Mapping
---

# Type Mapping

In service oriented architecture components expose services through well known contracts. In `C#` terms the contracts are the abstract classes or interfaces these components and services are exposing. So when we say service type, in most of the cases, we mean the interfaces implementing the contract. And the components are called Implementation types.

Unity allows to publish these components and make all the contracts they implement available to clients to consume. This publishing and "advertisement" is done by registering types and interfaces (contracts) associated with components.

## Registration Type

Registration type is the type of the 'Contract' this service provides. It could be the [Type](xref:System.Type) of the service itself of any of the base types it implements.

## Service To Implementation Mapping

The mapping is done when service is registered. Any type of registration (Type, Factory, Instance) allow to associate a service with different contracts.