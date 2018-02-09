---
title: "Configure SQL Server AlwaysOn-Verfügbarkeitsgruppe für hohe Verfügbarkeit unter Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/24/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: On Demand
ms.openlocfilehash: 76a5ed98ddd1aa69c11cd371586ce963ebcd97de
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>Configure SQL Server AlwaysOn-Verfügbarkeitsgruppe für hohe Verfügbarkeit unter Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieser Artikel beschreibt, wie eine SQL Server immer auf Availability Group (AG) für hohe Verfügbarkeit unter Linux zu erstellen. Es gibt zwei Konfigurationstypen für Testreihen. Ein *hohe Verfügbarkeit* Konfiguration verwendet einen Cluster-Manager für die Geschäftskontinuität bereitstellen. Diese Konfiguration kann auch Skalieren von Lesevorgängen Replikate enthalten. Dieses Dokument erläutert, wie die Verfügbarkeitsgruppe für hohe Verfügbarkeit zu erstellen.

Sie können auch erstellen eine Verfügbarkeitsgruppe ohne einen Cluster-Manager für *Skalieren von Lesevorgängen*. Die Verfügbarkeitsgruppe für schreibgeschützte Skalierung bietet nur schreibgeschützte Replikate für dezentrales Skalieren der Leistung. Es bietet keine hohen Verfügbarkeit. Zum Erstellen einer Verfügbarkeitsgruppe für das Skalieren von Lesevorgängen finden Sie unter [Konfigurieren einer SQL Server-Verfügbarkeitsgruppe für das Skalieren von Lesevorgängen auf Linux](sql-server-linux-availability-group-configure-rs.md).

Konfigurationen, die hohe Verfügbarkeit und Datenschutz gewährleisten erfordern zwei oder drei synchrone Replikate commit. Mit drei synchronen Replikaten kann die Verfügbarkeitsgruppe automatisch wiederherzustellen, selbst wenn ein Server nicht verfügbar ist. Weitere Informationen finden Sie unter [hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](sql-server-linux-availability-group-ha.md). 

Alle Server müssen entweder physisch oder virtuell sein, und virtuelle Server muss auf die gleiche Virtualisierungsplattform. Diese Anforderung ist, da die Agents Zäune plattformspezifisch sind. Finden Sie unter [Richtlinien für einen Gastcluster](https://access.redhat.com/articles/29440#guest_policies).

## <a name="roadmap"></a>Roadmap

Die Schritte zum Erstellen einer Verfügbarkeitsgruppe auf Linux-Servern zwecks hoher Verfügbarkeit unterscheiden sich von den Schritten in einem Windows Server-Failovercluster. Die folgende Liste beschreibt die allgemeinen Schritte: 

1. [Konfigurieren von SQL Server auf drei Clusterservern](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Alle drei Server in der Verfügbarkeitsgruppe müssen auf der gleichen Plattform - physisch oder virtuell - werden, da Linux hoher Verfügbarkeit Zäune-Agents verwendet, um Ressourcen auf den Servern zu isolieren. Die Agents Zäune sind für jede Plattform spezifisch.

2. Erstellen der Verfügbarkeitsgruppe. Dieser Schritt wird in diesem Artikel aktuelle behandelt. 

3. Konfigurieren eines Cluster-Ressourcen-Managers wie Schrittmacher an.
   
   Die Möglichkeit zum Konfigurieren eines Cluster-Ressourcen-Managers, hängt von der bestimmten Linux-Distribution ab. Finden Sie unter den folgenden Links für spezifische Anweisungen Verteilung: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >Produktionsumgebungen sind einen Fencing-Agent, wie STONITH für hohe Verfügbarkeit erforderlich. Die Demos in dieser Dokumentation verwenden Zäune-Agents. Die Demos sind für das Testen und nur die Überprüfung. 
   
   >Ein Linux-Cluster verwendet Fencing, um den Cluster in einen bekannten Zustand zurückzugeben. Die Methode zum Konfigurieren von Fencing hängt davon ab, die Verteilung und der Umgebung. Derzeit ist Fencing nicht in einige Cloudumgebungen verfügbar. Weitere Informationen finden Sie unter [Richtlinien zur Unterstützung für RHEL hohe Verfügbarkeit Cluster - Virtualisierungsplattformen](https://access.redhat.com/articles/29440).
   
   >SLES, finden Sie unter [SUSE Linux Enterprise-Erweiterung für hohe Verfügbarkeit](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. Fügen Sie der Verfügbarkeitsgruppe als Ressource im Cluster hinzu.  

   Die Möglichkeit, die Verfügbarkeitsgruppe als Ressource im Cluster hinzufügen, hängt von der Linux-Distribution ab. Finden Sie unter den folgenden Links für spezifische Anweisungen Verteilung: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Erstellen der Verfügbarkeitsgruppe

Für eine Konfiguration mit hoher Verfügbarkeit, die automatische Failover wird sichergestellt, muss die Verfügbarkeitsgruppe mindestens drei Replikate. Einer der folgenden Konfigurationen können hohe Verfügbarkeit nicht unterstützen:

- [Drei synchroner Replikate](sql-server-linux-availability-group-ha.md#threeSynch)

- [Zwei synchrone Replikate plus ein Replikat für die Konfiguration](sql-server-linux-availability-group-ha.md#twoSynch)

Informationen finden Sie unter [hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](sql-server-linux-availability-group-ha.md).

>[!NOTE]
>Die Verfügbarkeitsgruppen können zusätzliche synchrone oder asynchrone Replikate enthalten. 

Erstellen der Verfügbarkeitsgruppe für hohe Verfügbarkeit unter Linux. Verwenden der [CREATE AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-availability-group-transact-sql) mit `CLUSTER_TYPE = EXTERNAL`. 

* Verfügbarkeitsgruppe – `CLUSTER_TYPE = EXTERNAL` gibt an, dass eine externe Cluster-Entität die AG verwaltet. Schrittmacher ist ein Beispiel für eine externe Cluster-Entität. Wenn der AG-Clustertyp extern ist, 

* Legen Sie die primären und sekundäre Replikaten `FAILOVER_MODE = EXTERNAL`. 
   Gibt an, dass das Replikat mit einem externen Cluster-Manager, z. B. Schrittmacher interagiert. 

Die folgende Transact-SQL-Skripts erstellen eine Verfügbarkeitsgruppe für hohe Verfügbarkeit, die mit dem Namen `ag1`. Das Skript konfiguriert die Replikaten AG mit `SEEDING_MODE = AUTOMATIC`. Diese Einstellung bewirkt, dass SQL Server die Datenbank automatisch in jeder sekundären Serverinstanz erstellt. Aktualisieren Sie das folgende Skript für Ihre Umgebung. Ersetzen Sie die `<node1>`, `<node2>`, oder `<node3>` Werte mit den Namen der SQL Server-Instanzen, die die Replikate hosten. Ersetzen Sie die `<5022>` mit dem Port, den Sie für die datenbankspiegelungs-Endpunkt Daten festlegen. Um die Verfügbarkeitsgruppe zu erstellen, führen Sie die folgende Transact-SQL für die SQL Server-Instanz, die das primäre Replikat hostet.

Führen Sie **nur eine** der folgenden Skripts: 

- [Erstellen einer Verfügbarkeitsgruppe mit drei synchronen Replikaten](#threeSynch).
- [Erstellen einer Verfügbarkeitsgruppe mit zwei synchronen Replikaten und ein Replikat für die Konfiguration](#configOnly)
- [Erstellen einer Verfügbarkeitsgruppe mit zwei synchronen Replikaten](#readScale).

<a name="threeSynch"></a>

- Erstellen Sie AG mit drei synchroner Replikate

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'<node1>' 
            WITH (
               ENDPOINT_URL = N'tcp://<node1>:<5022>',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node2>' 
            WITH ( 
               ENDPOINT_URL = N'tcp://<node2>:<5022>', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node3>'
           WITH( 
              ENDPOINT_URL = N'tcp://<node3>:<5022>', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >Führen Sie nach dem Ausführen des obigen Skripts zum Erstellen von einer AG mit drei synchronen Replikate nicht das folgende Skript aus:

- Erstellen Sie AG mit zwei synchronen Replikaten und ein Replikat für die Konfiguration:

   >[!IMPORTANT]
   >Diese Architektur ermöglicht eine beliebige Edition von SQL Server das dritte Replikat hosten. Beispielsweise kann das dritte Replikat auf SQL Server Enterprise Edition gehostet werden. Enterprise Edition, ist der einzige gültige Endpunkttyp `WITNESS`. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'<node1>' WITH ( 
          ENDPOINT_URL = N'tcp://<node1>:<5022>', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node2>' WITH (  
          ENDPOINT_URL = N'tcp://<node2>:<5022>',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node3>' WITH ( 
          ENDPOINT_URL = N'tcp://<node3>:<5022>', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- Erstellen von AG mit zwei synchronen Replikaten

   Zwei Replikate mit den Verfügbarkeitsmodus für synchrone einschließen. Das folgende Skript erstellt z. B. eine AG aufgerufen `ag1`. `node1`und `node2` Replikate im synchronen Modus mit automatischem seeding und automatisches Failover zu hosten.

   >[!IMPORTANT]
   >Führen Sie nur das folgende Skript zum Erstellen einer Verfügbarkeitsgruppe mit zwei synchronen Replikaten. Das folgende Skript kann nicht ausgeführt werden, wenn Sie entweder dieses Skript ausgeführt haben. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
      N'node1' WITH (
         ENDPOINT_URL = N'tcp://node1:5022',
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      ),
      N'node2' WITH ( 
         ENDPOINT_URL = N'tcp://node2:5022', 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```


Sie können auch konfigurieren eine Verfügbarkeitsgruppe mit `CLUSTER_TYPE=EXTERNAL` mit SQL Server Management Studio oder PowerShell. 

### <a name="join-secondary-replicas-to-the-ag"></a>Verknüpfen Sie sekundärer Replikate mit der Verfügbarkeitsgruppe

Die folgende Transact-SQL-Skript verknüpft eine SQL Server-Instanz mit einer Verfügbarkeitsgruppe mit dem Namen `ag1`. Aktualisieren Sie das Skript für Ihre Umgebung. Führen Sie für jede SQL Server-Instanz, die ein sekundäres Replikat hostet die folgende Transact-SQL, um die Verfügbarkeitsgruppe zu verknüpfen.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>Nachdem Sie die Verfügbarkeitsgruppe erstellt haben, müssen Sie Integration mit einer Cluster-Technologie wie Schrittmacher für hohe Verfügbarkeit konfigurieren. Für eine Skalieren von Lesevorgängen-Konfiguration mit Testreihen, beginnend mit [!INCLUDE [SQL Server version](..\includes\sssqlv14-md.md)], das Einrichten eines Clusters ist nicht erforderlich.

Wenn Sie die in diesem Dokument beschriebenen Schritte ausführen, müssen Sie eine Verfügbarkeitsgruppe, die noch nicht gruppiert ist. Der nächste Schritt besteht, um den Cluster hinzuzufügen. Diese Konfiguration gilt für Read-Scale/Load balancing Szenarien, es ist nicht vollständig für hohe Verfügbarkeit. Für hohe Verfügbarkeit müssen Sie als Clusterressource die Verfügbarkeitsgruppe hinzufügen. Finden Sie unter [nächste Schritte](#next-steps) Anweisungen. 

## <a name="notes"></a>Hinweise

>[!IMPORTANT]
>Nachdem Sie den Cluster und fügen Sie als Clusterressource der Verfügbarkeitsgruppe hinzu, können Sie Transact-SQL keine für ein Failover der AG-Ressourcen. SQL Server-Cluster-Ressourcen unter Linux werden mit dem Betriebssystem nicht als eng verbunden, da es sich auf einem Windows Server Failover Cluster (WSFC) handelt. SQL Server-Dienst ist nicht über das Vorhandensein des Clusters. Alle Orchestrierung erfolgt über die Verwaltungstools. Verwenden Sie in RHEL oder Ubuntu `pcs`. Verwenden Sie SLES `crm`. 

>[!IMPORTANT]
>Wenn die Verfügbarkeitsgruppe eine Clusterressource ist, besteht ein bekanntes Problem in der aktuellen Version, in denen erzwungenes Failover ohne Datenverlust zu einem Replikat im asynchronen nicht funktioniert. Dies wird in der zukünftigen Version behoben werden. Manuelle oder automatische Failover auf ein synchrones Replikat erfolgreich ausgeführt wird. 


## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren Sie Red Hat Enterprise Linux-Cluster für SQL Server-Verfügbarkeitsgruppe Clusterressourcen](sql-server-linux-availability-group-cluster-rhel.md)

[Konfigurieren von SUSE Linux Enterprise Server-Cluster für Clusterressourcen für SQL Server-Verfügbarkeitsgruppe](sql-server-linux-availability-group-cluster-sles.md)

[Konfigurieren Sie Ubuntu-Cluster für SQL Server-Verfügbarkeitsgruppe Clusterressourcen](sql-server-linux-availability-group-cluster-ubuntu.md)
