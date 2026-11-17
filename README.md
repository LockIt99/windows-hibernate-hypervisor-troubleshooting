# windows-hibernate-hypervisor-troubleshooting
Troubleshooting Windows 11 Hibernate unavailable errors caused by the Windows hypervisor, VBS and Memory Integrity.
# Hibernate: "An internal system component has disabled hibernation. Hypervisor"

A Windows 11 troubleshooting guide documenting how to resolve the error:

> An internal system component has disabled hibernation. Hypervisor

## Problem

Running `powercfg /a` reports that Hibernate is unavailable because an internal system component, identified as the Hypervisor, has disabled it.

Consequently:
- Hibernate is unavailable.
- Fast Startup is unavailable.
- `powercfg /h on` alone does not resolve the issue.

## Investigation and Solution

This guide documents the investigation of three related Windows components:

1. Windows Hypervisor
2. Virtualization-Based Security (VBS)
3. Memory Integrity (HVCI)

The working solution in the tested Windows 11 setup involved:

- Disabling Memory Integrity through Windows Security.
- Disabling VBS through Windows security configuration.
- Disabling hypervisor launch using:

  `bcdedit /set hypervisorlaunchtype off`

- Enabling hibernation:

  `powercfg /h on`

After restarting, Hibernate and Fast Startup became available.

## Important

Disabling the Windows hypervisor prevents WSL 2 and Docker Desktop's WSL 2 backend from working.

This guide also explains how to restore virtualization when WSL 2 and Docker Desktop are needed.

Disabling VBS and Memory Integrity reduces Windows security protections. Understand the implications before applying these changes.

## Detailed Troubleshooting Guide

[Read the complete troubleshooting Wiki](https://github.com/Lockit99/windows-hibernate-hypervisor-troubleshooting/wiki/Hibernate-An-internal-system-component-has-disabled-hibernation-Hypervisor)

## Disclaimer

This solution was tested on one Windows 11 system. Results may vary depending on hardware, firmware, Windows build, and security configuration.

## Contributions

Have you encountered the same issue or discovered another solution? Contributions, corrections, and additional test results are welcome.

**The goal is simple: help others solve this problem without losing an entire day troubleshooting it.**
