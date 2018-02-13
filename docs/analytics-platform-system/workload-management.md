---
title: Arbeitsauslastungsverwaltung (SQLServer PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/12/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69063b1a-a8f3-453a-83ab-afbe7eb4f463
caps.latest.revision: 
ms.openlocfilehash: 738818a49491fbf8f8df491cac2f10ebdeedf3bf
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="workload-management"></a>Arbeitsauslastungsverwaltung
Verwaltungsfunktionen für SQL Server-PDW-arbeitsauslastung können Benutzer und Administratoren Zuweisen von Anforderungen an die Konfiguration des Speichers und Parallelität vorab festgelegt. Verwenden Sie arbeitsauslastungsverwaltung zum Verbessern der Leistung Ihrer arbeitsauslastung entweder consistent "und" gemischte, indem Anforderungen an die entsprechenden Ressourcen haben, ohne alle Anforderungen ewig eingabeereignisübermittlung ermöglicht.  
  
Mit der arbeitsauslastung containerverwaltungstechniken in SQL Server PDW könnten Sie z. B.:  
  
-   Reservieren Sie eine große Anzahl von Ressourcen zu einem Auftrag laden.  
  
-   Geben Sie weitere Ressourcen für einen columnstore-Index erstellen.  
  
-   Problembehandlung bei ein HashJoin langsam ausgeführt, um festzustellen, ob sie mehr Arbeitsspeicher benötigt, und weisen Sie ihm mehr Arbeitsspeicher.  
  
## <a name="Basics"></a>Workload-Management-Grundlagen  
  
### <a name="key-terms"></a>Schlüsselbegriffe  
Arbeitsauslastungsverwaltung  
*Arbeitsauslastungsverwaltung* ist die Fähigkeit, verstehen und System-Ressourcenverwendung anpassen, um die optimale Leistung für gleichzeitige Anforderungen zu erzielen.  
  
Ressourcenklasse  
In SQL Server-PDW eine *Ressourcenklasse* ist eine integrierte Serverrolle, die vorab zugeordneten für den Arbeitsspeicher und Parallelität Grenzwerten. SQL Server PDW ordnet die Ressourcen auf Anforderungen gemäß der Ressource Klasse Serverrollen-Mitgliedschaft des Anmeldenamens, der den Anforderungen übermittelt.  
  
Auf den Serverknoten verwendet die Implementierung der Ressourcenklassen das Feature "Ressourcenkontrolle" in SQL Server an. Weitere Informationen zur Ressourcenkontrolle finden Sie unter [Resource Governor](http://msdn.microsoft.com/en-us/library/bb933866(v=sql.11).aspx) auf MSDN.  
  
### <a name="understand-current-resource-utilization"></a>Verstehen der aktuellen Ressourcenverwendung  
Um System-Ressourcenverwendung für die momentan ausgeführten Anforderungen zu verstehen, verwenden Sie die dynamischen Verwaltungssichten von SQL Server PDW. Sie können z. B. DMVs verwenden, um zu verstehen, wenn ein langsam ausgeführte große HashJoin profitieren kann, durch die Verwendung von mehr Arbeitsspeicher.  
  
<!-- MISSING LINKS
For examples, see [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md).  
-->
  
### <a name="adjust-resource-allocations"></a>Ressource Zuordnungen anpassen  
Ändern Sie zum Anpassen der ressourcennutzung der Ressource Mitgliedschaft des Anmeldenamens, der die Anforderung übermittelt wird. Die Ressource Klasse Serverrollen heißen **Mediumrc**, **Largerc**, und **Xlargerc**. Sie stellen Zuordnungen groß, Mittel und extragroßen Ressource bzw. dar.  
  
Z. B. um eine große Menge an Systemressourcen auf eine Anforderung zuzuordnen, Hinzufügen der Anmeldename, der die Anforderung zu senden, ist die **Largerc** -Serverrolle. Die folgende ALTER SERVER ROLE-Anweisung fügt die Anmeldung Anna Largerc-Serverrolle.  
  
```sql  
ALTER SERVER ROLE largerc ADD MEMBER Anna;  
```  
  
## <a name="RC"></a>Beschreibungen der Resource-Klasse  
Die folgende Tabelle beschreibt die Ressourcenklassen und ihren System Resource-Zuordnungen.  
  
|Ressourcenklasse|Anfordern von Bedeutung|Maximaler Arbeitsspeicher Verwendung *|Parallelität Slots (maximal 32 =)|Description|  
|------------------|----------------------|--------------------------|---------------------------------------|---------------|  
|default|Medium|400 MB|1|Standardmäßig ist jeder Anmeldung eine kleine Menge an Arbeitsspeicher und Parallelitätsressourcen für ihre Anforderungen zulässig.<br /><br />Wenn eine Ressourcenklasse ein Anmeldename hinzugefügt wird, hat die neue Klasse Vorrang vor. Wenn eine Anmeldung aus allen Ressourcenklassen gelöscht wird, wird die Anmeldung an Standardeinstellung Ressourcenzuordnungsrichtlinien zurückgesetzt.|  
|MediumRC|Medium|1200 MB|3|Beispiele für Anforderungen, die eventuell die mittlere Ressourcenklasse:<br /><br />CTAS-Vorgänge, die großen hashjoins.<br /><br />Wählen Sie die Vorgänge, die mehr Arbeitsspeicher zu vermeiden, auf den Datenträger Zwischenspeichern erforderlich ist.<br /><br />Laden von Daten in gruppierte columnstore-Indizes ein.<br /><br />Erstellen, Neuerstellen und Organisieren von gruppierten columnstore-Indizes für kleinere Tabellen, die 10-15 Spalten aufweisen.|  
|largerc|High|2.8 GB|7|Beispiele für Anforderungen, die möglicherweise große Resource-Klasse:<br /><br />Sehr große CTAS-Vorgänge, die sehr große hashjoins oder große Aggregationen, z. B. große ORDER BY- oder GROUP BY-Klauseln enthalten.<br /><br />Wählen Sie die Vorgänge, die große Mengen an Arbeitsspeicher für Vorgänge wie z. B. hashjoins oder Aggregationen wie z. B. ORDER BY- oder GROUP BY-Klauseln erfordern<br /><br />Laden von Daten in gruppierte columnstore-Indizes ein.<br /><br />Erstellen, Neuerstellen und Organisieren von gruppierten columnstore-Indizes für kleinere Tabellen, die 10-15 Spalten aufweisen.|  
|xlargerc|High|8.4 GB|22|Die Klasse von sehr groß ist für Anforderungen, die sehr groß Ressourcenverbrauch zur Laufzeit erforderlich machen.|  
  
<sup>*</sup>Maximale speicherauslastung ist eine Näherung darstellt.  
  
### <a name="request-importance"></a>Anfordern von Bedeutung  
Die Anforderung Wichtigkeit ordnet die Menge an CPU-Zeit, die SQL Server, auf den Serverknoten, ausgeführt auf Anforderungen zurückgibt.  Anforderungen mit höherer Priorität erhalten mehr CPU-Zeit.  
  
### <a name="maximum-memory-usage"></a>Maximale Speicherauslastung  
Maximale speicherauslastung ist die Höchstmenge des verfügbaren Arbeitsspeichers an, innerhalb jedes Leerzeichen für die Verarbeitung eine Anforderung verwendet werden kann. Beispielsweise können eine Anforderung Mediumrc bis zu 1200 MB für die Verarbeitung innerhalb jedes Verteilungspunkts. Es ist aber trotzdem wichtig, um sicherzustellen, dass Daten nicht verzerrt werden, um zu vermeiden, dass einige Verteilungen, die meiste Arbeit ausführen.  
  
### <a name="concurrency-slots"></a>Parallelität von Bereitstellungsslots  
Das Ziel der Zuweisung von 1, 3, 7 und 22 Parallelität Slots ist zu groß und klein Prozesse zur gleichen Zeit ausgeführt werden, ohne Blockierung kleine Prozess aus, wenn ein großer Prozess ausgeführt wird.  SQL Server PDW zuordnen kann bis zu 32 Parallelität Steckplätze 1 Extragroß Anforderung (22 Steckplätze), 1 großen Anforderung (7 Steckplätze) und 1 mittlere Anforderung (3 Steckplätze) zur gleichen Zeit ausgeführt.  
  
Beispiele für bis zu 32 Parallelität Slots für gleichzeitige Anforderungen zuzuordnen:  
  
-   28 Slots = 4 große  
  
-   30 Slots = 10 Mittel  
  
-   32 Steckplätze = 32 Standard  
  
-   32 Steckplätze = Extragroß 1 + 1 große + 1 Mittel  
  
-   32 Steckplätze = 2 Mittel für große + 4 + 6 Standard  
  
Nehmen Sie an 6 große Anforderungen an SQL Server PDW übermittelt werden, und klicken Sie dann auf 10 Standard-Anforderungen gesendet werden. SQL Server PDW verarbeitet Anforderungen in der Reihenfolge ihrer Priorität wie folgt:  
  
-   Weisen Sie 28 Parallelität Slots zum start der anforderungsverarbeitung 4 groß wie der Arbeitsspeicher zur Verfügung steht, und behalten Sie 2 große Anforderungen in der Warteschlange bei.  
  
-   Reservieren Sie 4 Parallelität Steckplätze zum start der anforderungsverarbeitung 4 Standard, und halten Sie 6 Standard-Anforderungen in der Warteschlange.  
  
Anforderungen abgeschlossen wurden und Parallelität Steckplätze verfügbar, werden die restlichen Anforderungen entsprechend den verfügbaren Ressourcen und Priorität von SQL Server PDW zugewiesen werden. Z. B. wenn 7 Parallelität Slots geöffnet sind, haben wartende Anforderungen große höheren Priorität für die Steckplätze 7 als wartende Anforderungen mittlere.  Wenn 6 Steckplätze öffnen, klicken Sie dann belegt SQL Server PDW 6 mehr Standardgröße Anforderungen. Allerdings müssen Arbeitsspeicher und Parallelität Slots alle verfügbar sein, bevor SQL Server PDW eine Anforderung zum ausführen können.  
  
Innerhalb jeder Ressourcenklasse führen Sie die Anforderungen in First out (FIFO) ersten nacheinander aus.  
  
## <a name="GeneralRemarks"></a>Allgemeine Hinweise  
Wenn ein Anmeldename Mitglied von mehr als eine Ressourcenklasse ist, hat die Klasse mit der meisten Ressourcen Vorrang vor.  
  
Wenn eine Anmeldung hinzugefügt oder aus einer Ressourcenklasse gelöscht, wird diese Änderung für alle zukünftigen Anforderungen sofort wirksam; aktuelle Anforderungen, die darauf warten ausgeführt oder sind nicht betroffen. Der Anmeldename muss nicht zu trennen und erneut eine Verbindung herstellen, damit die Änderung erfolgen.  
  
Für jede Anmeldung werden die Einstellungen für die Ressource auf einzelne Anweisungen und -Vorgänge und nicht für die Sitzung angewendet.  
  
Vor SQL Server PDW eine Anweisung ausgeführt wird, wird versucht, die Parallelität Steckplätze, die erforderlich sind, für die Anforderung abzurufen. Wenn sie genügend Steckplätze Parallelität abrufen kann, verschiebt SQL Server PDW die Anforderung in einen Zustand warten auf den ausgeführt. Alle Ressourcen-System, das die Anforderung bereits zugewiesen wurden, werden zurück an das System zurückgegeben.  
  
Die meisten SQL-Anweisungen stets die standardzuordnungen für die Ressource benötigen, und daher nicht vom Ressourcenklassen gesteuert werden. Beispielsweise CREATE LOGIN nur eine kleine Menge an Ressourcen benötigt, und wird die Standardressourcen zugeordnet, selbst wenn die Anmeldung, das Aufrufen von CREATE LOGIN Mitglied ist eine eine Ressourcenklasse.  Wenn Anna ein Mitglied der Ressourcenklasse Largerc ist, und sie eine CREATE LOGIN-Anweisung übermittelt, wird die CREATE LOGIN-Anweisung mit der Standardanzahl von Ressourcen ausgeführt.  
  
SQL-Anweisungen und Vorgänge, die Ressourcenklassen unterliegen:  
  
-   ALTER INDEX REBUILD  
  
-   ALTER INDEX REORGANIZE  
  
-   ALTER-TABELLE NEU ERSTELLEN  
  
-   ERSTELLEN VON GRUPPIERTEN INDEX  
  
-   CREATE CLUSTERED COLUMNSTORE INDEX  
  
-   ERSTELLEN, WÄHLEN SIE FÜR TABELLE ALS  
  
-   ERSTELLEN, WÄHLEN SIE DIE TABELLE ALS REMOTE  
  
-   Laden von Daten mit **Dwloader**.  
  
-   INSERT SELECT  
  
-   UPDATE  
  
-   DELETE  
  
-   RESTORE DATABASE, wenn in einem eingebaut mit Weitere Serverknoten wiederherstellen.  
  
-   Wählen Sie aus, mit Ausnahme von nur-DMV-Abfragen  
  
## <a name="Limits"></a>Einschränkungen  
Die Ressourcenklassen steuern, Arbeitsspeicher und Parallelität Zuordnungen.  Sie keine e/a-Vorgänge steuern.  
  
## <a name="Metadata"></a>Metadata  
DMVs, die Informationen über Ressourcenklassen und Klassenmember Ressourcen enthalten.  
  
-   [sys.server_role_members](../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
-   [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
DMVs, die Aufschluss über den Status der Anforderungen und die Ressourcen, die sie benötigen:  
  
-   [sys.dm_pdw_lock_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
-   [sys.dm_pdw_resource_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
Verwandte Systemsichten verfügbar gemacht werden, aus der SQL Server-DMVs auf den Serverknoten. Finden Sie unter [SQL Server-dynamische Verwaltungssichten](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) Links zu DMVs auf MSDN.  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodes_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_resource_governor_resource_pools  
  
-   sys.dm_pdw_nodws_resource_governor_workload_groups  
  
-   sys.dm_pdw_nodes_exec_sessions  
  
-   sys.dm_pdw_nodes_exec_requests  
  
-   sys.dm_pdw_nodes_exec_query_memory_grants  
  
-   sys.dm_pdw_nodes_exec_query_resource_semaphores  
  
-   sys.dm_pdw_nodes_os_memory_brokers  
  
-   sys.dm_pdw_nodes_os_memory_cache_entries  
  
-   sys.dm_pdw_nodes_exec_cached_plans  
  
## <a name="RelatedTasks"></a>Verwandte Aufgaben  
[Workload-Verwaltungsaufgaben](workload-management-tasks.md)  
  
<!-- MISSING LINKS
See the Workload Management section of [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md) for the following tasks:  
  
1.  Find the number of active requests for each resource group.  
  
2.  Determine if my requests need more memory  
  
3.  Determine if there are a high number of query optimizations or suboptimal plan generations.  
  
4.  Determine Average CPU time per request in each resource pool to date  
  
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
