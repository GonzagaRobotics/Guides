# GU Robotics CS Team Style Guide

By: Damon Lewis

Last Updated: September 15, 2024

## Introduction

This document is meant to be a general guide for the CS team, and will largely refer to existing style guides for specific languages. This document will focus more on code organization and project structure.

## Linux and ROS Versions

Use Ubuntu 22 and ROS2 Humble Hawksbill.

## Project Structure

Use workspaces to organize your code. Each workspace should focus on a semi-specific component of the robot. For example, you might have a workspace for object detection, and another for obstacle avoidance, but not a workspace for the autonomous system as a whole.

Write workspace names in PascalCase.

### Required Files

Include a `README.md` file that documents the version and code name, explains the purpose of the workspace, how to build and run the code, and any dependencies or known issues.

Include a `.gitignore` file that contains at least the following:

```
# ROS Generated Files
build/
install/
log/
*.swp

__pycache__/
```

Include a `LICENSE` file. Use the MIT license.

Generally, include a launch file that starts the node or nodes in the workspace. These must be in the `launch/` directory and should generally be named `launch.py`. Launch files must be written in Python.

### Packages

Packages should be small and focused. They should contain only one node or a small group of related nodes. Packages must be in the `src/` directory of the workspace and written in snake_case.

When creating a new package, use `ros2 pkg create --build-type ament_[cmake|python] --license MIT [package_name]`. This will create a package with the correct structure and CMake or Python build system.

Packages that just contain interfaces should have the suffix `_interfaces`. Include a `Types.hpp` file in the include directory that contains type adapters and other useful shortcuts.

### Versioning

Use Semantic Versioning for your projects, starting at 0.1.0. Use the form `MAJOR.MINOR.PATCH`. Don't include alpha or beta tags in the version number.

Generally, increment the `PATCH` version for small bug fixes, the `MINOR` version for general changes, and the `MAJOR` version for rewrites or major changes.

Every so often, releases will be made for all projects. All projects in the same release must work together (ie. 1.6.X of one project must work with 2.0.X of another project). Each of these releases will have a code name that will again be shared by all projects in the release.

Packages have version numbers in their `package.xml` files. These should be updated the same way as the workspace version numbers.

### Source Control

Use Git for source control and use GitHub as the remote. All projects must be on the GU Robotics GitHub organization.

All repositories must have the same name as and contain only the workspace they are a part of. Repositories should be public.

In the early stages of a project, it is acceptable to only have a `main` branch. However, once a project has had a release or has matured sufficiently, it must have a `main` branch and a `dev` branch. All development should be done on the `dev` branch, and the `main` branch must only contain releases.

Branches other than `main` and `dev` are allowed, but should be used sparingly. When used, they should be for experimental features or changes that are not ready for the `dev` branch.

Use kebab-case for branch names.

## Languages to Use

Write rover code in C++ or Python 3. C++ is preferred, especially for critical or performance-sensitive systems. Python is acceptable for prototyping, performance-insensitive systems, or systems that require extensive use of libraries that are easier to use in Python.

If a different language is necessary, it must be approved by the CS team lead.

For code that runs off the rover (ie. ControlSystem), or for development tools, any common language is acceptable. Just be prepared to justify your choice.

## Code Style

Follow the given style guides for the language you are using. If there is a conflict between this guide and the language-specific guide, this guide takes precedence.

### C++

Use the [ROS2 C++ Style Guide](https://docs.ros.org/en/humble/The-ROS2-Project/Contributing/Code-Style-Language-Versions.html#id1).

There are a few modifications:

-   Maximum line length is 120 characters.
-   All variables must use camelCase, including member, static, and global variables.
-   All functions must use camelCase.
-   Constants must be in SCREAMING_SNAKE_CASE.
-   Use `#pragma once` instead of include guards.

### Python

Use [PEP 8](https://peps.python.org/pep-0008/).

There are a few modifications:

-   Maximum line length is 120 characters.
-   Prefer single quotes for strings unless escaping is necessary.
