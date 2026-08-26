# Legacy Build and ARGoS 3 Migration Notes

## What the source targets

The implementation targets ARGoS 2. Evidence includes:

- include paths beginning with `argos2/`;
- `argos-configuration` XML using ARGoS 2 controller and entity syntax;
- `footbot_*` control interfaces from the older Swarmanoid namespace;
- Qt4/OpenGL discovery in the loop-function CMake files; and
- ARGoS 2 dynamic-linking and Qt user-function APIs.

## What is missing from the archive

The repository contains module-level CMake files but no preserved top-level CMake project or exact operating-system/toolchain manifest. The XML files expect shared libraries under paths such as:

```text
build/controllers/footbot_foraging/libfootbot_foraging.so
build/loop_functions/foraging_loop_functions/libforaging_loop_functions.so
```

A historical rebuild therefore requires reconstructing the original ARGoS 2 project layout and dependencies.

## Recommended modernisation path

1. Create a container or virtual machine for the legacy ARGoS 2 toolchain.
2. Reconstruct a top-level build using an official ARGoS 2 example from the same release.
3. Compile the controller before enabling Qt visualisation code.
4. Run one minimal XML experiment and validate sensors, wheel motion, and plug-in loading.
5. Record a known-good output file and simulation screenshot.
6. Only then begin a separate ARGoS 3 port branch.

## ARGoS 3 porting work

An ARGoS 3 migration is not a header-only update. It requires review of:

- namespaces and controller base classes;
- sensor and actuator names;
- foot-bot entity and plug-in registration;
- loop-function APIs;
- Qt/OpenGL user-function APIs;
- XML controller, physics-engine, media, and entity syntax; and
- CMake package discovery and library linkage.

Keep the historical source unchanged on the archive branch and implement the port in a dedicated branch with small, testable commits.

