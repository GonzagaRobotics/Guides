# GU Robotics CS Team Style Guide

By: Damon Lewis

Last Updated: July 13, 2025

## Introduction

This document is meant to be the overall guide for all CS team members, especially newcomers.

For LICENSE, README, gitignore, and other template files, see the [Templates](./Templates/) directory.

### Clarification of Terms

-   `Must`: This is a requirement. Few or no exceptions will be made.
-   `Should`: This is a recommendation. Exceptions may be made if there is a good reason.
-   `May`: This is an option. Feel free to ask for guidance if you are unsure.

Where the imperative form is used, it is a `Must`. For example, "Use Git" means "You must use Git".

## Linux and ROS Versions

Use Ubuntu 22.04 LTS and ROS2 Humble Hawksbill.

### Update Policy

The Linux and ROS versions will be updated yearly at the start of the fall semester to the next ROS2 LTS and supported Ubuntu LTS, unless dependent software or hardware (particularly the Jetson) does not support the new version. The CS team lead will make the final decision on whether to update.

## Project Structure

We use the `Rover` monorepo for the majority of the rover code. Other projects that do not use ROS2 only need to follow the `README.md` and `LICENSE` requirements below.

The structure of a repository should look like this:

```
RepositoryName
├── launch
|   ├── drive_only.launch.py
│   └── normal.launch.py
├── LICENSE
├── README.md
└── src
    ├── perception
    ├── obstacle_avoidance
    ├── camera_server
    └── other packages
```

### Required Files

Include a `README.md` file that explains the purpose of the workspace, how to build and run the code, and any dependencies or known issues. Include a version number if relevant (see Versioning section below).

Include a `.gitignore` file by copying the template.

Include a `LICENSE` file by copying the template. We use the MIT license.

You should include a launch file (written in Python) that starts the node or nodes in the workspace. These must be in the `launch/` directory and follow the format `launch_name.launch.py`. There can be multiple launch files if needed, but they should be named appropriately.

### Packages

Packages should be focused on a specific task or functionality (the CS team lead has final discretion on the line here). They should contain only a few nodes, ideally one. Packages must be in the `src/` directory of the workspace. Packages names must be written in snake_case per ROS2 requirements.

When creating a new package, use `ros2 pkg create --build-type ament_[cmake|python] --license MIT [package_name]`. This will create a package with the correct structure and CMake or Python build system.

Packages that just contain interfaces must have the suffix `_interfaces`. You should include a `Types.hpp` file in the `include/[package_name]` directory that contains type adapters and other interface-related code. You must modify the `CMakeLists.txt` file to export the directory (see template).

### Versioning

Use Semantic Versioning for your projects, starting at 0.1.0. Use the form `MAJOR.MINOR.PATCH`. Don't include alpha or beta tags in the version number because we track unstable work with branches.

Generally, increment the `PATCH` version for small bug fixes, the `MINOR` version for general changes, and the `MAJOR` version for rewrites or major changes. Currently, manually update `package.xml/setup.py` before merging.

In the rover monorepo, version each package separately. Note that for Python packages, the version number is also used in the `setup.py` file, so it must be updated there as well. The monorepo itself is versioned as v1, v2, etc., upon a merge to `main` from `dev`.

For other repositories, include the version number in the `README.md` file if the repository does not contain multiple packages or is not using ROS2.

### Source Control

Use Git for source control and use GitHub as the remote. All projects must be on the GU Robotics GitHub organization.

All repositories must have the same name as and contain only the workspace they are a part of. Repositories should be public.

In the early stages of a project, it is acceptable to only have a `main` branch. However, once a project is in usage or reaches v1.0.0, it must have a `main` branch and a `dev` branch. The developer may also do this earlier at their discretion. All development should be done on the `dev` branch before being merged into `main`. The `main` branch should always be in a releasable state.

For most repositories, use feature or experiment branches for development. Use `feature/...` for work destined for mainline, or `experimental/...` for short lived tests.

Pull requests do not need approval due to the small team size, but are ideally reviewed by the CS team lead before merging. There are currently no special CI or review processes in place.

For the rover monorepo, work on features or experiments should be done in a feature branch. Keep the name relevant to the work being done. When complete, merge the branch into `dev` for full testing. Branches may be deleted if they are no longer needed.

Use kebab-case for branch names. Do not use uppercase, underscores, or spaces.

## Languages to Use

Write rover code in C++ or Python 3.10. C++ is preferred, especially for critical or performance-sensitive systems. Python is acceptable for prototyping, performance-insensitive systems, or systems that require extensive use of libraries that are easier to use in Python.

If a different language is necessary, it must be approved by the CS team lead through Teams.

For code that runs off the rover (ie. ControlSystem), or for development tools, any common language/dependency management is acceptable alongside. Just be prepared to justify your choice. Typescript and NPM is a preferred combination.

Always commit lock files so builds are reproducible.

## Code Style

Follow the given style guides for the language you are using. If there is a conflict between this guide and the language-specific guide, this guide takes precedence for repository/package level norms.

The rover monorepo includes a `.clang-format` file to help enforce the C++ style guide. Set your editor to use a formatter on save. Copy the file to other repositories if they use ROS2 C++.

### C++

Use the [ROS2 C++ Style Guide](https://docs.ros.org/en/humble/The-ROS2-Project/Contributing/Code-Style-Language-Versions.html#id1).

Modifications:

-   Use `#pragma once` instead of include guards.

### Python

Use [PEP 8](https://peps.python.org/pep-0008/).

Modifications:

-   Prefer single quotes for strings unless escaping is necessary.

## All Naming Conventions

| Entity Type | Convention              | Example                    |
| ----------- | ----------------------- | -------------------------- |
| Repository  | PascalCase              | `Rover`                    |
| branch      | kebab-case              | `feature/new-feature`      |
| Package     | snake_case              | `obstacle_avoidance`       |
| Node        | snake_case              | `camera_server`            |
| Launch File | snake_case (.launch.py) | `rosbridge_only.launch.py` |
