---
title: "So werden Daten im Abfragespeicher gesammelt | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "09/13/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Abfragespeicher, Datensammlung"
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# So werden Daten im Abfragespeicher gesammelt
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Der Abfragespeicher fungiert als **Flugdatenschreiber** und sammelt durchgehend Kompilier- und Laufzeitinformationen, die sich auf Abfragen und Pläne beziehen. Daten, die sich auf Abfragen beziehen, werden in den internen Tabellen beibehalten und dem Benutzer durch eine Reihe von Sichten dargestellt.  
  
## Sichten  
 Das folgende Diagramm zeigt Abfragespeichersichten und ihre logischen Beziehungen, wobei Kompilierzeitinformationen als blaue Entitäten dargestellt werden:  
  
 ![query-store-process-1views](../../relational-databases/performance/media/query-store-process-1views.png "query-store-process-1views")  
  
 **Sichtbeschreibungen**  
  
|Sicht|Description|  
|----------|-----------------|  
|**sys.query_store_query_text**|Stellt eindeutige Abfragetexte dar, die in der Datenbank ausgeführt wurden. Kommentare und Leerzeichen vor und nach dem Abfragetext werden ignoriert. Kommentare und Leerzeichen im Text werden nicht ignoriert. Jede Anweisung im Batch generiert einen separaten Abfragetexteintrag.|  
|**sys.query_context_settings**|Stellt eindeutige Kombinationen von Einstellungen zur Planauswirkung dar, unter denen Abfragen ausgeführt werden. Derselbe Abfragetext, der mit unterschiedlichen Einstellungen zur Planauswirkung ausgeführt wurde, erzeugt separate Abfrageeinträge im Abfragespeicher, da `context_settings_id` Teil des Abfrageschlüssels ist.|  
|**sys.query_store_query**|Abfrageeinträge, die im Abfragespeicher separat nachverfolgt und erzwungen werden. Ein einzelner Abfragetext kann mehrere Abfrageeinträge erzeugen, wenn er unter unterschiedlichen Kontexteinstellungen oder außerhalb im Vergleich zu innerhalb verschiedener [!INCLUDE[tsql](../../includes/tsql-md.md)]-Module (gespeicherte Prozeduren, Trigger usw.) ausgeführt wird.|  
|**sys.query_store_plan**|Stellt den geschätzten Plan für die Abfrage mit den Kompilierzeitstatistiken dar. Der gespeicherte Plan entspricht einem Plan, den Sie durch die Verwendung von `SET SHOWPLAN_XML ON` erhalten würden.|  
|**sys.query_store_runtime_stats_interval**|Der Abfragespeicher trennt die Zeit in automatisch generierte Zeitfenster (Intervalle) und speichert aggregierte Statistiken für jeden ausgeführten Plan auf diesem Intervall. Die Größe des Intervalls wird gesteuert durch die Konfigurationsoption „Intervall für Statistikerfassung“ (in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) oder durch `INTERVAL_LENGTH_MINUTES` mithilfe von [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md).|  
|**sys.query_store_runtime_stats**|Aggregierte Laufzeitstatistiken für ausgeführte Pläne. Alle erfassten Metriken werden in Form von 4 Statistikfunktionen ausgedrückt: Mittelwert, Minimum, Maximum und Standardabweichung.|  
  
 Weitere Informationen zu Abfragespeichersichten finden Sie im Abschnitt **Zugehörige Sichten, Funktionen und Prozeduren** in [Überwachen der Leistung mit dem Abfragespeicher](https://msdn.microsoft.com/library/dn817826.aspx).  
  
## Abfrageverarbeitung  
 Der Abfragespeicher interagiert mit der Abfrageverarbeitungspipeline mit den folgenden wichtigen Punkten:  
  
1.  Wenn die Abfrage zum ersten Mal kompiliert wird, werden der Abfragetext und der ursprüngliche Plan an den Abfragespeicher gesendet  
  
2.  Wenn die Abfrage neu kompiliert wird, wird der Plan im Abfragespeicher aktualisiert. Wenn ein neuer Plan erstellt wird, fügt der Abfragespeicher den neuen Planeintrag für die Abfrage ein und behält die vorherigen Pläne zusammen mit deren Ausführungsstatistiken.  
  
3.  Bei der Abfrageausführung werden Laufzeitstatistiken an den Abfragespeicher gesendet. Der Abfragespeicher sorgt für genaue aggregierte Statistiken für jeden Plan, der innerhalb des aktuell aktiven Intervalls ausgeführt wurde.  
  
4.  Während der Kompilierung und Prüfung für Neukompilierungsphasen bestimmt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ob sich im Abfragespeicher ein Plan befindet, der auf die aktuell ausgeführte Abfrage angewendet werden sollte. Falls ein erzwungener Plan vorhanden ist und der Plan im Prozedurcache sich davon unterscheidet, wird die Abfrage neu kompiliert – auf dieselbe Weise wie wenn PLAN HINT auf diese Abfrage angewendet wird. Dieser Vorgang erfolgt transparent in der Benutzeranwendung.  
  
 Das folgende Diagramm stellt die oben erläuterten Punkte der Integration dar:  
  
 ![query-store-process-2processor](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor")  
  
 Zur Minimierung des E/A-Aufwands werden neue Daten im Speicher erfasst. Schreibvorgänge werden in eine Warteschlange eingereiht und danach auf den Datenträger geleert. Abfrage- und Planinformationen („Plan Store“ im nachstehenden Diagramm) werden mit minimaler Latenz geleert. Die Laufzeitstatistiken (Runtime Stats) verbleiben solange im Arbeitsspeicher, wie dies mit der `DATA_FLUSH_INTERVAL_SECONDS``SET QUERY_STORE`. Im SSMS-Dialogfeld „Abfragespeicher“ können Sie einen Wert für **Datenleerungsintervall (Minuten)** eingeben, der in einen Sekundenwert konvertiert wird.  
  
 ![query-store-process-3plan](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan")  
  
 Im Fall eines Systemabsturzes kann der Abfragespeicher Laufzeitdaten bis zu einer durch `DATA_FLUSH_INTERVAL_SECONDS` definierten Menge verlieren. Mit dem Standardwert von 900 Sekunden (15 Minuten) besteht ein optimales Gleichgewicht zwischen der Abfrageerfassungsleistung und der Datenverfügbarkeit.  
Im Fall einer Arbeitsspeicherauslastung können Laufzeitstatistiken früher auf den Datenträger geleert werden als mit `DATA_FLUSH_INTERVAL_SECONDS` definiert.  
Während dem Lesen der Abfragespeicherdaten werden arbeitsspeicherinterne und auf dem Datenträger gespeicherte Daten transparent zusammengeführt.  
  
 ![query-store-process-4planinfo](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

  
## Siehe auch  
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Bewährte Methoden für den Abfragespeicher](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [Katalogsichten des Abfragespeichers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  