# PHP Development Standards Guide

## Table of Contents

- [0. Introduction](README.md)
- [1. Preface](Preface.md)
- [2. Project Development Standards](Project.md/#project)
- [3. PHP Coding Standards](PHP.md/#php)
  - [3.1. Naming Conventions](PHP.md/#name)
  - [3.2. Constants Definition](PHP.md/#constant)
  - [3.3. Code Formatting](PHP.md/#format)
  - [3.4. OOP Guidelines](PHP.md/#oop)
  - [3.5. Concurrency Handling](PHP.md/#concurrent)
  - [3.6. Control Statements](PHP.md/#control)
  - [3.7. Others](PHP.md/#other)
- [4. MySQL Database Design Standards](Mysql.md/#mysql)
  - [4.1. Table Creation Guidelines](Mysql.md/#buildtable)
  - [4.2. Index Guidelines](Mysql.md/#index)
  - [4.3. SQL Statements](Mysql.md/#sql)
  - [4.4. ORM Mapping](Mysql.md/#orm)
- [5. Unit Testing Standards](UnitTest.md/#test)
- [6. Exception and Logging Standards](Log.md/#exception-log)
  - [6.1. Exception Handling](Log.md/#exception)
  - [6.2. Logging Guidelines](Log.md/#log)
- [7. Security Standards](Safe.md/#safe)


## Version History

| Version | Name | Update Date | Notes |
| :-----:| :----: | :----: | :---- |
| 0.0.1 | PHP | 2025/01/13 | - |

## Terminology

1. ORM (Object Relation Mapping): A technique that converts data between object-oriented programming languages and databases, referring to frameworks like Laravel, Hyperf, etc.
2. NPE (java.lang.NullPointerException): Null Pointer Exception.
