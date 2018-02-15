---
title: "Konfigurieren einer SQL Server-Verfügbarkeitsgruppe für das Skalieren von Lesevorgängen auf Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 02/14/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 460eb7ca3163a9a4ca8d53a24fec143f32b701e6
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-linux"></a>Konfigurieren einer SQL Server-Verfügbarkeitsgruppe für das Skalieren von Lesevorgängen unter Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Sie können eine SQL Server immer auf Verfügbarkeit Gruppe (AG) für das Skalieren von Lesevorgängen Arbeitslasten unter Linux konfigurieren. Es gibt zwei Arten von Testreihen-Architekturen. Eine Architektur für hohe Verfügbarkeit verwendet einen Cluster-Manager, um Geschäftskontinuität zu ermöglichen. Diese Architektur kann auch Skalieren von Lesevorgängen Replikate enthalten. Um die hohe Verfügbarkeit-Architektur zu erstellen, finden Sie unter [konfigurieren Sie SQL Server AlwaysOn-Verfügbarkeitsgruppe für hohe Verfügbarkeit unter Linux](sql-server-linux-availability-group-configure-ha.md). Die andere Architektur unterstützt nur Skalieren von Lesevorgängen Arbeitslasten. In diesem Artikel wird das Erstellen einer Verfügbarkeitsgruppe ohne ein Cluster-Manager zum Skalieren von Lesevorgängen Arbeitslasten erläutert. Diese Architektur bietet Lese--Skalierung. Es stellt keine hohen Verfügbarkeit bereit.

>[!NOTE]
>Eine verfügbarkeitsgruppe mit `CLUSTER_TYPE = NONE` zählen Replikate, die auf anderen Betriebssystemplattformen gehostet werden. Es kann keine hohen Verfügbarkeit unterstützen. 

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Erstellen der Verfügbarkeitsgruppe

Erstellen der Verfügbarkeitsgruppe. Set `CLUSTER_TYPE = NONE`. Darüber hinaus legen Sie jedes Replikat mit `FAILOVER_MODE = NONE`. Clientanwendungen, die Ausführung der Analyse oder reporting Arbeitslasten können direkt eine Verbindung herstellen, auf die sekundären Datenbanken. Sie können auch eine schreibgeschützte Routingliste erstellen. Verbindungen mit dem primären Replikat weiterleiten Auslesen der Routingliste im Round-Robin-verbindungsanforderungen an jede der sekundären Replikate.

Die folgende Transact-SQL-Skript erstellt eine Verfügbarkeitsgruppe mit dem Namen `ag1`. Das Skript konfiguriert die Replikaten AG mit `SEEDING_MODE = AUTOMATIC`. Diese Einstellung bewirkt, dass SQL Server die Datenbank automatisch in jeder sekundären Serverinstanz erstellt wird, nachdem sie der Verfügbarkeitsgruppe hinzugefügt wird. Aktualisieren Sie das folgende Skript für Ihre Umgebung. Ersetzen Sie die `<node1>` und `<node2>` Werte mit den Namen der SQL Server-Instanzen, die die Replikate hosten. Ersetzen Sie die `<5022>` Wert mit dem Port, die Sie für den Endpunkt festlegen. Führen Sie das folgende Transact-SQL-Skript auf dem primären SQL Server-Replikat:

```SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'<node1>' WITH (
            ENDPOINT_URL = N'tcp://<node1>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'<node2>' WITH ( 
            ENDPOINT_URL = N'tcp://<node2>:<5022>', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-ag"></a>Verknüpfen von sekundären SQL-Server mit der Verfügbarkeitsgruppe

Die folgende Transact-SQL-Skript verknüpft einen Server mit einer Verfügbarkeitsgruppe mit dem Namen `ag1`. Aktualisieren Sie das Skript für Ihre Umgebung. Führen Sie auf jedem sekundären Replikat für die SQL Server die folgende Transact-SQL-Skript, um die Verfügbarkeitsgruppe zu verknüpfen:

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../includes/ss-linux-cluster-availability-group-create-post.md)]

Diese Verfügbarkeitsgruppe ist eine Konfiguration mit hoher Verfügbarkeit nicht. Wenn Sie hohen Verfügbarkeit benötigen, befolgen Sie die Anweisungen unter [Konfigurieren einer AlwaysOn-Verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md). Erstellen Sie insbesondere die AG mit `CLUSTER_TYPE=WSFC` (in Windows) oder `CLUSTER_TYPE=EXTERNAL` (in Linux). Klicken Sie dann mit entweder Windows Server-Failoverclustering unter Windows oder Schrittmacher unter Linux mit einem Cluster-Manager integrieren.

## <a name="connect-to-read-only-secondary-replicas"></a>Herstellen einer Verbindung mit schreibgeschützten sekundären Replikaten

Es gibt zwei Möglichkeiten zum schreibgeschützten sekundären Replikaten herstellen. Direktes Verbinden mit SQL Server-Instanz, die das sekundäre Replikat hostet und die Datenbanken abzufragen. Sie können auch schreibgeschütztes routing, wofür einen Listener.

* [Lesbare sekundäre Replikate](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [Schreibgeschütztes routing](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>Failover für das primäre Replikat auf einer Verfügbarkeitsgruppe Skalieren von Lesevorgängen

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>Nächste Schritte

* [Konfigurieren einer verteilten Verfügbarkeitsgruppe](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)
* [Weitere Informationen zu Verfügbarkeitsgruppen](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)
* [Ausführen eines erzwungenen manuellen Failovers](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)

