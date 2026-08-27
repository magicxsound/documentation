---
title: Running in simulation
description: "Run a Thread network on a workstation, without hardware."
---

!!! note
    Starter page. Fill in from the upstream simulation documentation.

The simulation build lets you run a multi-node Thread network as ordinary
processes on a workstation, which is the fastest way to try OpenThread without
radio hardware.

## Prerequisites

- A [simulation build](/docs/guides/build.md) of OpenThread.

## Forming a network

Start a node and bring up a new Thread network:

```bash
dataset init new
dataset commit active
ifconfig up
thread start
```

Check that the node became a leader:

```bash
state
```
