---
title: "Failoverclusterinstanz – SQL Server on Linux betreiben | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 6f8ba6ed2e56ea4dc97ab68fa85601d94edfe1fc
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>Failoverclusterinstanz – SQL Server on Linux Betrieb

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In diesem Artikel wird erläutert, wie eine SQL-Server-Failoverclusterinstanz (FCI) unter Linux verwendet werden. Wenn Sie eine SQL Server-FCI nicht unter Linux erstellt haben, finden Sie unter [konfigurieren Failoverclusterinstanz – SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md). 

## <a name="failover"></a>Failover

Failover für FCIs ähnelt einem Windows Server-Failovercluster (WSFC). Wenn der Cluster-Knoten die FCI hostet eine Art von Fehler auftritt, sollte die FCI automatisch ein Failover auf einen anderen Knoten ausgeführt. Es gibt keine Möglichkeit zum bevorzugten Besitzer festlegen, sodass Schrittmacher den Knoten auswählt, die dem neuen Host für die FCI ist vorhanden, im Gegensatz zu einem WSFC.

Es gibt Situationen, die sollten Sie manuell die FCI auf einen anderen Knoten fehl. Der Prozess ist nicht die gleiche wie beim FCIs für einen wsfc-Cluster. Für einen wsfc-Cluster werden Ressourcen auf Rollenebene Failover. In Schrittmacher wählen Sie eine Ressource zu verschieben und vorausgesetzt, dass alle Einschränkungen richtig sind, alle anderen geht auch. 

Die Möglichkeit zum Failover hängt von der Linux-Distribution ab. Befolgen Sie die Anweisungen für Ihre Linux-Distributionen.

- [RHEL oder Ubuntu](#rhelFailover)
- [SLES](#slesFailover)

## <a name = "#rhelFailover"></a>Manuelles Failover (RHEL oder Ubuntu)

Um ein manuelles Failover ausführen, führen Sie Onn Red Hat Enterprise Linux (RHEL) oder Ubuntu Server die folgenden Schritte aus.
1.  Führen Sie den folgenden Befehl aus: 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > Schrittmacher Namen der Ressource für die SQL Server-FCI.

   \<NewHostNode > ist der Name des Clusterknotens an, die Sie die FCI gehostet werden soll. 

   Sie erhalten Bestätigung nicht.

2.  Während eines manuellen Failovers erstellt Schrittmacher eine standorteinschränkung für die Ressource, die ausgewählt wurde, manuell verschieben. Um diese Einschränkung anzuzeigen, führen Sie `sudo pcs constraint`.

3.  Nachdem das Failover abgeschlossen ist, entfernen Sie die Einschränkung durch Ausgeben von `sudo pcs resource clear <FCIResourceName>`. 

\<FCIResourceName > Schrittmacher Namen der Ressource für die FCI. 

## <a name = "#slesFailover"></a>Manuelles Failover (SLES)


Verwenden Sie in die Suse Linux Enterprise Server (SLES), die `migrate` -Befehl, um ein manuelles Failover einer SQL Server-FCI. Beispiel:

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName > ist der Teamressourcen-Name für die Failoverclusterinstanz. 

\<NewHostNode > ist der Name des neuen Zielhosts. 


<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
--->

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurieren Sie Failoverclusterinstanz – SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
