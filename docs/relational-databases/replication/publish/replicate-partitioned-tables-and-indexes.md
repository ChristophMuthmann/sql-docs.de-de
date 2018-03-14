---
title: Replizieren partitionierter Tabellen und Indizes | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/10/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitioned indexes [SQL Server], replicating
- partitioned tables [SQL Server], replicating
- replication [SQL Server], partitioned tables
- publishing [SQL Server replication], partitioned tables
- transactional replication, partitioned tables
ms.assetid: c9fa81b1-6c81-4c11-927b-fab16301a8f5
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 35e53afc080178d27e99a74da3be023159ee95b2
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="replicate-partitioned-tables-and-indexes"></a>Replizieren partitionierter Tabellen und Indizes
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Durch die Partitionierung können große Tabellen oder Indizes einfacher verwaltet werden, da Sie Teilmengen von Daten schnell und effizient verwalten und darauf zugreifen können und gleichzeitig die Integrität einer Datensammlung erhalten können. Weitere Informationen finden Sie unter [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md). Die Replikation unterstützt die Partitionierung durch Bereitstellung einer Gruppe von Eigenschaften, die angeben, wie partitionierte Tabellen und Indizes behandelt werden sollen.  
  
## <a name="article-properties-for-transactional-and-merge-replication"></a>Artikeleigenschaften für die Transaktions- und Mergereplikation  
 In der folgenden Tabelle sind die Objekte aufgelistet, die zum Partitionieren von Daten verwendet werden.  
  
|Objekt|Erstellt mit|  
|------------|----------------------|  
|Partitionierte Tabelle oder partitionierter Index|CREATE TABLE oder CREATE INDEX|  
|Partitionsfunktion|CREATE PARTITION FUNCTION|  
|Partitionsschema|CREATE PARTITION SCHEME|  
  
 Die erste Gruppe von Eigenschaften, die mit der Partitionierung in Zusammenhang stehen, sind Artikelschemaoptionen, die bestimmen, ob Partitionierungsobjekte auf den Abonnenten kopiert werden sollen. Diese Schemaoptionen können folgendermaßen festgelegt werden:  
  
-   Auf der Seite **Artikeleigenschaften** des Assistenten für neue Veröffentlichungen oder im Dialogfeld Veröffentlichungseigenschaften. Geben Sie für die Eigenschaften **Tabellenpartitionierungsschemas kopieren** und **Indexpartitionierungsschemas kopieren** den Wert **true**an, um die in der obigen Tabelle aufgeführten Objekte zu kopieren. Informationen zum Zugriff auf die Seite **Artikeleigenschaften** finden Sie unter [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Mithilfe des Parameters *schema_option* einer der folgenden gespeicherten Prozeduren:  
  
    -   [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) oder [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) für die Transaktionsreplikation  
  
    -   [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) oder [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) für die Mergereplikation  
  
     Geben Sie die entsprechenden Schemaoptionswerte an, um die in der obigen Tabelle aufgelisteten Objekte zu kopieren. Informationen zum Angeben von Schemaoptionen finden Sie unter [Specify Schema Options](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
 Durch die Replikation werden Objekte während der Erstsynchronisierung auf den Abonnenten kopiert. Wenn im Partitionsschema andere Dateigruppen als die PRIMARY-Dateigruppe verwendet werden, müssen diese vor der Erstinitialisierung auf dem Abonnenten vorhanden sein.  
  
 Nachdem der Abonnent initialisiert wurde, werden Datenänderungen an den Abonnenten weitergegeben und auf die entsprechenden Partitionen übertragen. Änderungen am Partitionsschema werden jedoch nicht unterstützt. Bei Transaktions- und Mergereplikationen wird die Replikation der folgenden Befehle nicht unterstützt: ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME bzw. die Anweisung REBUILD WITH PARTITION von ALTER INDEX Die ihnen zugeordneten Änderungen werden nicht automatisch auf den Abonnenten repliziert. Es liegt in der Zuständigkeit des Benutzers, ähnliche Änderungen manuell für den Abonnenten vorzunehmen.  
  
## <a name="replication-support-for-partition-switching"></a>Replikationsunterstützung für Partitionswechsel  
 Ein wesentlicher Vorteil der Tabellenpartitionierung besteht in der Fähigkeit, Teilmengen von Daten rasch und effizient zwischen Partitionen zu verschieben. Daten werden mit dem Befehl SWITCH PARTITION verschoben. Wenn eine Tabelle für die Replikation aktiviert wurde, werden SWITCH PARTITION-Vorgänge aus folgenden Gründen standardmäßig blockiert:  
  
-   Wenn Daten in eine oder aus einer Tabelle verschoben werden, die auf dem Verleger, aber nicht auf dem Abonnenten vorhanden sind, können die Daten von Verleger und Abonnenten inkonsistent werden. Dieses Problem tritt i. d. R. auf, wenn Daten in eine oder aus einer Stagingtabelle verschoben werden.  
  
-   Wenn der Abonnent über eine andere Definition für die partitionierte Tabelle verfügt als der Verleger, dann schlägt der Verteilungs-Agent fehl, wenn er Änderungen auf dem Abonnenten anzuwenden versucht.  
  
 Trotz dieser potenziellen Probleme können Partitionswechsel für Transaktionsreplikationen aktiviert werden. Bevor Sie Partitionswechsel aktivieren, müssen Sie sicherstellen, dass alle an einem Partitionswechsel beteiligten Tabellen sowohl auf dem Verleger als auch auf dem Abonnenten vorhanden sind und dass die Tabellen- und Partitionsdefinitionen auf dem Verleger und dem Abonnenten identisch sind.  
  
 Wenn Partitionen bei den Verlegern und Abonnenten über das gleiche Partitionsschema verfügen, können Sie *allow_partition_switch* zusammen mit *replication_partition_switch* aktivieren, wodurch nur die "partition switch"-Anweisung für den Abonnenten repliziert wird. Sie können auch *allow_partition_switch* aktivieren, ohne die DDL zu replizieren. Dies ist hilfreich, wenn Sie alte Monate aus der Partition auslagern möchten und die replizierte Partition jedoch für ein weiteres Jahr für Sicherungszwecke auf dem Abonnenten aufbewahren möchten.  
  
 Wenn Sie über die aktuelle Version Partitionswechsel für SQL Server 2008 R2 aktivieren, benötigen Sie möglicherweise schon in naher Zukunft auch Teilungs- und Mergevorgänge. Stellen Sie vor dem Ausführen von Teilungs- oder Mergevorgängen in replizierten Tabellen sicher, dass für die fragliche Partition keine replizierten Befehle ausstehen. Sie sollten außerdem sicherstellen, dass für die Partition während der Teilungs- und Mergevorgänge keine DML-Vorgänge ausgeführt werden. Wenn Transaktionen vorhanden sind, die nicht vom Protokollleser verarbeitet wurden, oder DML-Vorgänge für eine Partition einer replizierten Tabelle ausgeführt werden, während ein Teilungs- oder Mergevorgang stattfindet (an dem die gleiche Partition beteiligt ist), kann das zu einem Verarbeitungsfehler beim Protokolllese-Agent führen. Um den Fehler zu beheben, ist möglicherweise eine erneute Initialisierung des Abonnements erforderlich.  
  
> [!WARNING]  
>  Sie sollten keinen Partitionswechsel für Peer-zu-Peer-Veröffentlichungen aktivieren, da die ausgeblendete Spalte dazu verwendet wird, um Konflikte zu erkennen und aufzulösen.  
  
### <a name="enabling-partition-switching"></a>Aktivieren des Partitionswechsels  
 Die folgenden Eigenschaften von Transaktionsveröffentlichungen ermöglichen es den Benutzern, das Verhalten von Partitionswechseln in einer replizierten Umgebung zu steuern:  
  
-   **@allow_partition_switch**, wenn diese Eigenschaft auf **Tabellenpartitionierungsschemas kopieren**festgelegt wird, kann SWITCH PARTITION für die Veröffentlichungsdatenbank ausgeführt werden.  
  
-   **@replicate_partition_switch** bestimmt, ob die SWITCH PARTITION DDL-Anweisung auf Abonnenten repliziert werden soll. Diese Option ist nur gültig, wenn **@allow_partition_switch** auf **Tabellenpartitionierungsschemas kopieren**.  
  
 Sie können diese Eigenschaften beim Erstellen der Veröffentlichung mit [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) oder nach der Erstellung der Veröffentlichung mit [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) festlegen. Wie bereits erwähnt, unterstützen Mergereplikationen keine Partitionswechsel. Entfernen Sie die Tabelle aus der Datenbank, um SWITCH PARTITION für eine Tabelle auszuführen, die für Mergereplikationen aktiviert wurde.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
