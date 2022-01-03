---
title: Developer Conventions for Tanzu Application Platform
subtitle: Developer Conventions
weight: 1
---

## <a id='overview'></a>Overview

Developer Conventions is a set of [conventions](../convention-service/about.md) that
enable your workloads to support live-update and debug operations.
It is used alongside the [Tanzu CLI Apps Plug-in](../cli-plugins/apps/overview-installation.md)
and the [Tanzu Dev Tools for VSCode](../vscode-extension/about.md) IDE extension.

## <a id='features'></a>Features

### <a id='enable-live-updates'></a>Enabling Live Updates

Developer Conventions modifies your workload to enable live updates in either of the following situations:

- You deploy a workload by using the Tanzu CLI Apps plug-in and include the flag `--live-update=true`. For more information about how to deploy a workload with the CLI, see [Tanzu apps workload apply](../cli-plugins/apps/command-reference/tanzu_apps_workload_apply.md).
- You deploy a workload by using the `Tanzu: Live Update Start` option through the Tanzu Dev Tools for VSCode extension. For more information about live updating with the Tanzu Dev Tools extension, see [Using Tanzu Dev Tools to get started](../vscode-extension/usage-getting-started.md).

When either of the preceding actions take place, the convention behaves as follows:

1. It looks for the `apps.tanzu.vmware.com/live-update=true` annotation on a PodTemplateSpec associated with a workload.
2. It verifies that the image to which conventions are applied contains a process that can be live updated. 
3. It adds annotations to the PodTemplateSpec to modify the Knative properties `minScale` & `maxScale` such that the minimum and maximum number of Pods is 1. This ensures the eventual running Pod won't be scaled down to 0 during a live update session.

After these changes are made, you can use the Tanzu Dev Tools extension
or the Tilt CLI to make live update changes to source code directly on the cluster.

### <a id='enable-debug'></a>Enabling debugging

Developer Conventions modifies your workload to enable debugging in either of the following situations:

- You deploy a workload by using the Tanzu CLI Apps plug-in and include the flag `--debug=true`. For more information about how to deploy a workload with the CLI, see [Tanzu apps workload apply](../cli-plugins/apps/command-reference/tanzu_apps_workload_apply.md).
- You deploy a workload by using the `Tanzu Java Debug Start` option through the Tanzu Dev Tools for VSCode extension. For more information about debugging with the Tanzu Dev Tools extension, see [Using Tanzu Dev Tools to get started](../vscode-extension/usage-getting-started.md).

When either of the preceding actions take place, the convention behaves as follows:

1. It looks for the `apps.tanzu.vmware.com/debug=true` annotation on a PodTemplateSpec associated with a workload.
2. It checks for the `debug-8` or `debug-9` labels on the image configuration's bill of materials (BOM).
3. It sets the TimeoutSeconds of the Liveness, Readiness, and Startup probes to 600 if currently set to a lower number.
4. It adds annotations to the PodTemplateSpec to modify the Knative properties `minScale` & `maxScale` such that the minimum and maximum number of Pods is 1. This ensures the eventual running Pod won't be scaled down to 0 during a debug session.

After these changes are made, you can use the Tanzu Dev Tools extension or other CLI-based debuggers to debug your workload directly on the cluster.

>**Note**: Currently, Developer Conventions only supports debug operations for Java applications.

### <a id='resource-limits'></a>Resource Limits

The following resource limits are set on the Developer Conventions service:

```
resources:
  limits:
	cpu: 100m
	memory: 256Mi
  requests:
	cpu: 100m
	memory: 20Mi
```

## <a id='installing'></a>Installing

Developer Conventions is released as a Tanzu Package. For information about installing Developer Conventions, see [Installing Tanzu Application Platform](../install-intro.md).

## <a id='uninstalling'></a>Uninstalling

To uninstall Developer Conventions, follow the guide for [Uninstalling Tanzu Application Platform packages](https://docs.vmware.com/en/VMware-Tanzu-Application-Platform/0.4/tap/GUID-uninstall.html). The package name for developer conventions is `developer-conventions`.
