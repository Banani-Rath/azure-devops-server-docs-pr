---
ms.topic: include
---

::: moniker range="azure-devops-2019"

The **deploymentPool** command is designed to migrate all deployment groups from one deployment pool to another.

```
TfsConfig deploymentpool /migrateDeploymentGroups /fromPool:<source pool name> /toPool:<destination pool name>
```

|Option|Description|
|---|---|
|fromPool|Source pool name.|
|toPool|Destination pool name.|

::: moniker-end