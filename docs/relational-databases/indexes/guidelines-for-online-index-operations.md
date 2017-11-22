---
title: "Richtlinien für Onlineindexvorgänge | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
caps.latest.revision: "64"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.suite: sql
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.workload: On Demand
ms.openlocfilehash: 6860fb131bb645ca918f7095481776884c0f4f6f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="guidelines-for-online-index-operations"></a>Richtlinien für Onlineindexvorgänge
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Für das Ausführen von Onlineindexvorgängen gelten die folgenden Richtlinien:  
  
-   Gruppierte Indizes müssen offline erstellt, neu erstellt oder gelöscht werden, wenn die zugrunde liegende Tabelle die folgenden LOB-Datentypen (Large Object) enthält: **image**, **ntext**und **text**.  
  
-   Nicht eindeutige, nicht gruppierte Indizes können online erstellt werden, wenn die Tabelle LOB-Datentypen enthält, keine dieser Spalten jedoch in der Indexdefinition als Schlüssel- oder Nichtschlüsselspalte (eingeschlossene Spalte) verwendet wird.  
  
-   Indizes für lokale temp-Tabellen können nicht online erstellt, neu erstellt oder gelöscht werden. Diese Einschränkung gilt nicht für Indizes globaler temporärer Tabellen.
- Indizes können von dort fortgesetzt werden, wo nach einem unerwarteten Fehler, einem Datenbank-Failover oder einem **PAUSE**-Befehl angehalten wurde. Weitere Informationen finden Sie unter [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md). 

> [!NOTE]  
>  Onlineindexvorgänge sind nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den Editionen unterstützte Funktionen](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Die folgende Tabelle enthält eine Auflistung der Indexvorgänge, die online ausgeführt werden können, der Indizes, die von diesen Onlinevorgängen ausgeschlossen sind und fortsetzbaren Indexrestriktionen. Zusätzliche Einschränkungen werden ebenfalls aufgeführt.  
  
| Onlineindexvorgang | Ausgeschlossene Indizes | Andere Einschränkungen |  
|----------------------------|----------------------|------------------------|  
|ALTER INDEX REBUILD|Deaktivierter gruppierter Index oder deaktivierte indizierte Sicht<br /><br /> XML-Index<br /><br />Columnstore-Index <br /><br /> Index für eine lokale temp-Tabelle|Die Angabe des ALL-SchlüsselwOrts kann bewirken, dass die Operation einen Fehler erzeugt, wenn die Tabelle einen ausgeschlossenen Index enthält.<br /><br /> Weitere Einschränkungen zum Neuerstellen deaktivierter Indizes gelten ebenfalls. Weitere Informationen finden Sie unter [Deaktivieren von Indizes und Einschränkungen](../../relational-databases/indexes/disable-indexes-and-constraints.md).|  
|CREATE INDEX|XML-Index<br /><br /> Eindeutiger gruppierter Ausgangsindex für eine Sicht<br /><br /> Index für eine lokale temp-Tabelle||  
|CREATE INDEX WITH DROP_EXISTING|Deaktivierter gruppierter Index oder deaktivierte indizierte Sicht<br /><br /> Index für eine lokale temp-Tabelle<br /><br /> XML-Index||  
|DROP INDEX|Deaktivierter Index<br /><br /> XML-Index<br /><br /> Nicht gruppierter Index<br /><br /> Index für eine lokale temp-Tabelle|Es können nicht mehrere Indizes in einer einzigen Anweisung angegeben werden.|  
|ALTER TABLE ADD CONSTRAINT (PRIMARY KEY oder UNIQUE)|Index für eine lokale temp-Tabelle<br /><br /> Gruppierter Index|Es ist nur jeweils eine Unterklausel gleichzeitig zulässig. Sie können z. B. PRIMARY KEY- oder UNIQUE-Einschränkungen nicht in der gleichen ALTER TABLE-Anweisung hinzufügen oder löschen.|  
|ALTER TABLE DROP CONSTRAINT (PRIMARY KEY oder UNIQUE)|Gruppierter Index||  
  
 Die zugrunde liegende Tabelle kann nicht geändert, abgeschnitten oder gelöscht werden, während ein Onlineindexvorgang ausgeführt wird.  
  
 Die beim Erstellen oder Löschen eines gruppierten Indexes angegebene Einstellung für die Onlineoption (ON oder OFF) wird auf alle nicht gruppierten Indizes angewendet, die neu erstellt werden müssen. Wenn der gruppierte Index z. B. online mithilfe von CREATE INDEX WITH DROP_EXISTING, ONLINE=ON erstellt wird, werden alle zugeordneten nicht gruppierten Indizes ebenfalls online neu erstellt.  
  
 Wenn Sie einen UNIQUE-Index online erstellen oder neu erstellen, versuchen die Indexerstellung und eine gleichzeitige Benutzertransaktion möglicherweise, den gleichen Schlüssel einzufügen. Dies verletzt die Eindeutigkeit. Wenn eine von einem Benutzer in den neuen Index (Ziel) eingegebene Zeile eingefügt wird, bevor die ursprüngliche Zeile aus der Quelltabelle in den neuen Index verschoben wird, schlägt der Onlineindexvorgang fehl.  
  
 Obwohl der Fall nicht häufig auftritt, kann der Onlineindexvorgang aufgrund von Benutzer- oder Anwendungsaktivitäten einen Deadlock bewirken, wenn sie mit den Datenbankupdates interagiert. In diesen seltenen Fällen wählt [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] die Benutzer- oder Anwendungsaktivität als Deadlockopfer aus.  
  
 Sie können gleichzeitige Onlineindex-DDL-Operationen für die gleiche Tabelle oder Sicht nur dann ausführen, wenn Sie mehrere neue, nicht gruppierte Indizes erstellen oder nicht gruppierte Indizes neu organisieren. Alle anderen gleichzeitig durchgeführten Onlineindexvorgänge erzeugen einen Fehler. Sie können z. B. keinen neuen Index online erstellen, während Sie einen vorhandenen Index für die gleiche Tabelle online neu erstellen.  
  
 Ein Onlinevorgang kann nicht ausgeführt werden, wenn ein Index eine Spalte des Datentyps für große Objekte enthält und wenn dieselbe Transaktion vor diesem Onlinevorgang Updatevorgänge enthält. Um dieses Problem zu umgehen, platzieren Sie den Onlinevorgang außerhalb der Transaktion oder vor den Updates in der Transaktion.  
  
## <a name="disk-space-considerations"></a>Überlegungen zum Speicherplatz  
 Onlineindexvorgänge erfordern mehr Speicherplatz als Offlineindexvorgänge. 
 - Beim Erstellen und Wiederherstellen von Indizes ist zusätzlicher Speicherplatz erforderlich, damit der Index erstellt (oder wiederhergestellt) werden kann. 
 - Darüber hinaus ist Speicherplatz für den temporären Zuordnungsindex erforderlich. Dieser temporäre Index wird in Onlineindexvorgängen verwendet, die einen gruppierten Index erstellen, neu erstellen oder löschen.
- Das Löschen eines gruppierten Indexes online benötigt den gleichen Speicherplatz wie das Erstellen (oder Wiederherstellen) eines gruppierten Indexes online. 

Weitere Informationen finden Sie unter [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
## <a name="performance-considerations"></a>Leistungsaspekte  
 Zwar ermöglichen Onlineindexvorgänge gleichzeitige Benutzerupdateaktivitäten, die Indexvorgänge benötigen jedoch mehr Zeit, wenn die Updateaktivitäten umfangreich sind. In der Regel sind Onlineindexvorgänge langsamer als die entsprechenden Offlineindexvorgänge, und zwar unabhängig davon, in welchem Umfang gleichzeitige Updateaktivitäten ausgeführt werden.  
  
 Da sowohl die Quell- als auch die Zielstrukturen während des Onlineindexvorgangs verwaltet werden, kann die Ressourcenverwendung für Einfüge-, Update- und Löschtransaktionen bis um das Doppelte zunehmen. Dieser Vorgang kann einen Leistungsabfall und erhöhte Ressourcenverwendung (insbesondere CPU-Zeit) während des Indexvorgangs bewirken. Onlineindexvorgänge werden vollständig protokolliert.  
  
 In der Regel werden Onlinevorgänge empfohlen, Sie sollten jedoch Ihre Umgebung sowie besondere Anforderungen berücksichtigen. Es kann vorteilhafter sein, Indexvorgänge offline auszuführen. Dabei besitzen Benutzer während der Operation nur eingeschränkten Zugriff auf die Daten, der Vorgang wird jedoch schneller abgeschlossen und verwendet weniger Ressourcen.  
  
 Auf Mehrprozessorcomputern, auf denen SQL Server 2016 ausgeführt wird, verwenden Indexanweisungen möglicherweise mehrere Prozessoren, um die Scan- und Sortiervorgänge auszuführen, die mit der Indexanweisung verknüpft sind, genau so, wie andere Abfragen dies tun. Sie können die MAXDOP-Indexoption verwenden, um die Anzahl der Prozessoren für den Onlineindexvorgang zu steuern. Auf diese Weise können Sie die Ressourcen, die vom Indexvorgang verwendet werden, mit den Ressourcen gleichzeitiger Benutzer ausgleichen. Weitere Informationen finden Sie unter [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md). Weitere Informationen zu den Editionen von SQL Server, die parallele Indexvorgänge unterstützen, finden Sie unter [Von den Editionen unterstützte Funktionen](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Da eine Sperre des Typs S- oder Sch-M in der Abschlussphase des Indexvorgangs aktiviert wird, sollten Sie Vorsicht walten lassen, wenn Sie einen Onlineindexvorgang innerhalb einer expliziten Benutzertransaktion ausführen, z. B. in einem BEGIN TRANSACTION...COMMIT-Block. In diesem Fall bleibt die Sperre aktiviert, bis die Transaktion beendet ist, und beeinträchtigt daher die Benutzerparallelität.  
  
 Die Onlineneuerstellung von Indizes kann die Fragmentierung erhöhen, wenn diese für die `MAX DOP > 1` -Option und die `ALLOW_PAGE_LOCKS = OFF` -Option aktiviert ist. Weitere Informationen finden Sie unter [Vorgehensweise: Onlineneuerstellung von Indizes kann zu erhöhter Fragmentierung führen](http://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx).  
  
## <a name="transaction-log-considerations"></a>Überlegungen zum Transaktionsprotokoll  
 Umfangreiche Indexvorgänge, die offline oder online ausgeführt werden, können große Datenlasten generieren, die das Transaktionsprotokoll schnell füllen können. Damit sichergestellt wird, dass für den Indexvorgang ein Rollback ausgeführt werden kann, kann das Transaktionsprotokoll erst abgeschnitten werden, nachdem der Indexvorgang abgeschlossen wurde; das Protokoll kann jedoch während des Indexvorgangs gesichert werden. Aus diesem Grund muss das Transaktionsprotokoll für die Dauer des Indexvorgangs genügend Speicherplatz zum Speichern der Transaktionen des Indexvorgangs sowie ggf. der gleichzeitigen Benutzertransaktionen aufweisen. Weitere Informationen finden Sie unter [Transaction Log Disk Space for Index Operations](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md).  

## <a name="resumable-index-rebuild-considerations"></a>Überlegungen zur fortsetzbaren Neuerstellung von Indizes

> [!NOTE]
> Weitere Informationen finden Sie unter [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md). 
>

Für das Ausführen einer fortsetzbaren Neuerstellung eines Onlineindex gelten die folgenden Richtlinien:
-   Verwalten, Planen und Erweitern von Indexwartungsfenstern. Sie können einen Vorgang zur Neuerstellung eines Index mehrmals anhalten und neu starten, um Ihr Wartungsfenster anzupassen.
- Wiederherstellen nach Fehlern bei der Indexneuerstellung (z.B. Datenbank-Failover oder wenn kein Speicherplatz mehr verfügbar war).
- Wenn ein Indexvorgang angehalten wird, wird sowohl für den ursprünglichen Index als auch für den neu erstellten Index Speicherplatz benötigt, und beide müssen während des DML-Vorgangs aktualisiert werden.

- Ermöglicht das Abschneiden von Abschneideprotokollen während eines Vorgangs zur Neuerstellung eines Index (dieser Vorgang kann für einen regulären Onlineindexvorgang nicht durchgeführt werden).
- Die Option SORT_IN_TEMPDB=ON wird nicht unterstützt.

> [!IMPORTANT]
> Für die fortsetzbare Neuerstellung muss kein Abschneiden mit langer Ausführungsdauer geöffnet bleiben. Deswegen kann das Protokoll während dieses Vorgangs gekürzt werden, was eine bessere Verwaltung des Protokollspeicherplatzes gestattet. Mit dem neuen Entwurf haben wir es geschafft, dass notwendige Daten zusammen mit allen erforderlichen Verweisen für den Neustart des fortsetzbaren Vorgangs in einer Datenbank gehalten werden.
>

Im Allgemeinen besteht kein Leistungsunterschied zwischen fortsetzbaren und nicht fortsetzbaren Neuerstellungen von Onlineindizes. Wenn Sie einen fortsetzbaren Index aktualisieren, während ein Vorgang zur Indexneuerstellung unterbrochen ist:
- Bei Arbeitsauslastungen, die meistens nur gelesen werden, ist die Leistungsauswirkung unbedeutend. 
- Bei Arbeitsauslastungen, die oft aktualisiert werden, tritt möglicherweise eine Minderung des Durchsatzes auf (bei unseren Tests ergab sich eine Minderung von unter 10%).

Im Allgemeinen besteht kein Unterschied bei der Defragmentierungsqualität zwischen fortsetzbaren und nicht fortsetzbaren Onlineindexneuerstellungen.
 
## <a name="related-content"></a>Verwandte Inhalte  
 [Funktionsweise von Onlineindexvorgängen](../../relational-databases/indexes/how-online-index-operations-work.md)  
  
 [Ausführen von Onlineindexvorgängen](../../relational-databases/indexes/perform-index-operations-online.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  
