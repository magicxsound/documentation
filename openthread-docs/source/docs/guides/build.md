---
title: Building OpenThread
description: "How to fetch the sources and produce an OpenThread build."
---

!!! note
    Starter page. Verify each command against the upstream
    [openthread/openthread](https://github.com/openthread/openthread) README before publishing.

## Prerequisites

Clone the repository and install the build dependencies:

```bash
git clone --recursive https://github.com/openthread/openthread.git
cd openthread
./script/bootstrap
```

## Build

OpenThread builds with CMake. Each supported platform has its own build target:

```bash
./script/cmake-build simulation
```

## Next steps

- [Running in simulation](/docs/guides/simulation.md)
- [CLI reference](/docs/reference/cli.md)
