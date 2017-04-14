# Introduction

## APIs

Spark core consists of two APIs - unstructured and structured.

_**Unstructured APIs**_ - RDDS(Resilient Distributed Datasets), Accumulators and Broadcast variables. These are mostly meant for manipulation of raw objects.

_**Structured APIs**_ - DataFrames, DataSets, Spark SQL. These are optimized for working with structured data in the form of tables.

## Spark Applications

Consists of a *driver* process and a set of *executor* processes.

Driver runs on driver node - maintains information about the application, responds to user's program, analyzes, distributes and schedules work across executors.

Executor 