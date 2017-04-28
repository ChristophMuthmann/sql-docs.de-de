---
title: Verwaltungs-Data Warehouse | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data collector [SQL Server], management data warehouse
- data warehouse
- management data warehouse
ms.assetid: 9874a8b2-7ccd-494a-944c-ad33b30b5499
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0430b88308cb3ebc07b1addfb2e34575150fa41e
ms.lasthandoff: 04/11/2017

---
# <a name="management-data-warehouse"></a>Verwaltungs-Data Warehouse
  Das Verwaltungs-Data Warehouse ist eine relationale Datenbank, die alle Daten enthält, die von einem Server gesammelt werden, der das Datensammlungsziel ist. Diese Daten werden dazu verwendet, die Berichte für die Systemdaten-Sammlungssätze zu generieren. Sie können auch für benutzerdefinierte Berichte verwendet werden.  
  
 Die Datensammlerinfrastruktur definiert die Aufträge und Wartungspläne, die für die Implementierung der vom Datenbankadministrator definierten Beibehaltungsrichtlinien erforderlich sind.  
  
> [!IMPORTANT]  
>  Für diese Version des Datensammlers wird das Verwaltungs-Data Warehouse mithilfe des einfachen Wiederherstellungsmodells erstellt, um die Protokollierung zu minimieren. Sie sollten das entsprechende Wiederherstellungsmodell für Ihre Organisation implementieren.  
  
## <a name="deploying-and-using-the-data-warehouse"></a>Bereitstellen und Verwenden des Data Warehouses  
 Sie können dieses Verwaltungs-Data Warehouse auf derselben Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installieren, die den Datensammler ausführt. Wenn die Serverressourcen oder die Leistung auf dem überwachten Server ein Problem darstellen, können Sie das Verwaltungs-Data Warehouse auf einem anderen Computer installieren.  
  
 Die erforderlichen Schemas sowie die Objekte für die vordefinierten Systemdaten-Sammlungssätze werden erstellt, sobald Sie das Verwaltungs-Data Warehouse erstellen. Bei den Schemas, die erstellt werden, handelt es sich um „core“ und „snapshots“. Ein drittes Schema, „custom_snapshots“, wird bei der Erstellung von benutzerdefinierten Sammlungssätzen mit Sammlungselementen erstellt, die den generischen T-SQL-Abfragesammlertyp verwenden.  
  
###### <a name="core-schema"></a>Core-Schema  
 Das core-Schema beschreibt die Tabellen, gespeicherten Prozeduren und Sichten, die zum Organisieren und Identifizieren gesammelter Daten verwendet werden. Diese Tabellen werden für alle Datentabellen, die für einzelne Sammlertypen erstellt werden, freigegeben. Dieses Schema ist gesperrt und kann nur vom Besitzer der Datenbank des Verwaltungs-Data Warehouse geändert werden. Den Namen der Tabellen in diesem Schema wird das Präfix "core" vorangestellt.  
  
 In der folgenden Tabelle werden die Datenbanktabellen im core-Schema beschrieben. Mithilfe dieser Datenbanktabellen kann der Datensammler nachverfolgen, woher die Daten kamen, wer sie eingefügt hat und wann sie in das Data Warehouse hochgeladen wurden.  
  
|Tabellenname|Beschreibung|  
|----------------|-----------------|  
|core.performance_counter_report_group_items|Speichert Informationen darüber, wie die Leistungsindikatoren in den Berichten des Verwaltungs-Data Warehouse gruppiert und aggregiert werden sollen.|  
|core.snapshots_internal|Identifiziert jede neue Momentaufnahme. Immer dann, wenn ein neues Uploadpaket beginnt, einen neuen Datenbatch in ein Data Warehouse hochzuladen, wird in diese Tabelle eine neue Zeile eingefügt.|  
|core.snapshot_timetable_internal|Speichert Informationen über die Momentaufnahmezeiten. Die Momentaufnahmezeit wird in einer separaten Tabelle gespeichert, da viele Momentaufnahmen zur nahezu gleichen Zeit auftreten können.|  
|core.source.info_internal|In dieser Tabelle werden Informationen über die Datenquelle gespeichert. Diese Tabelle wird immer dann aktualisiert, wenn ein neuer Sammlungssatz beginnt, Daten in das Data Warehouse hochzuladen.|  
|core.supported_collector_types_internal|Enthält die IDs von registrierten Sammlertypen, die Daten in das Verwaltungs-Data Warehouse hochladen können. Diese Tabelle wird nur dann aktualisiert, wenn das Schema des Warehouse so aktualisiert wird, sodass ein neuer Sammlertyp unterstützt wird. Wenn das Verwaltungs-Data Warehouse erstellt wird, wird diese Tabelle mit den IDs der vom Datensammler bereitgestellten Sammlertypen aufgefüllt.|  
|core.wait_categories|Enthält die Kategorien, die verwendet werden, um Wartetypen entsprechend ihrem wait_type-Merkmal zu gruppieren.|  
|core.wait_types|Enthält die vom Datensammler erkannten Wartetypen.|  
|core.purge_info_internal|Gibt an, dass eine Anforderung gestellt wurde, das Entfernen von Daten aus dem Verwaltungs-Data Warehouse zu beenden.|  
  
 Die vorgenannten Tabellen werden zusammen mit den Tabellen des Sammlertyps verwendet, um Informationen zu speichern. Zum Beispiel verwendet der generische SQL-Ablaufverfolgungs-Sammlertyp die folgenden Tabellen, um die Ablaufverfolgungsdaten zu speichern:  
  
-   core.source_info_internal  
  
-   core.snapshots_internal  
  
-   snapshots.trace_info  
  
-   snapshots.trace_data  
  
###### <a name="snapshots-schema"></a>Momentaufnahme-Schema  
 Das Momentaufnahme-Schema beschreibt die Objekte, die zum Speichern und Verwalten der von den bereitgestellten Sammlertypen gesammelten Daten erforderlich sind. Die Tabellen in diesem Schema sind fest und müssen während des Lebenszyklus des Sammlertyps nicht geändert werden. Wenn Änderungen erforderlich sind, kann das Schema nur von Mitgliedern der mdw_admin-Rolle geändert werden. Diese Tabellen werden erstellt, um die von den Systemdaten-Sammlungssätzen gesammelten Daten zu speichern.  
  
 Die folgenden Tabellen zeigen einen Teil des Verwaltungs-Data Warehouse-Schemas, das für die Serveraktivitäts- und Abfragestatistik-Sammlungssätze erforderlich ist.  
  
-   Ressourcentabellen auf Systemebene  
  
    -   **snapshots.os_wait_stats**  
  
    -   **snapshots.os_latch_stats**  
  
    -   **snapshots.os_schedulers**  
  
    -   **snapshots.os_memory_clerks**  
  
    -   **snapshots.os_memory_nodes**  
  
    -   snapshots.sql_process_and_system_memory  
  
-   Systemaktivität  
  
    -   snapshots.active_sessions_and_requests  
  
-   Abfragestatistik  
  
    -   snapshots.query_stats  
  
-   E/A-Statistik  
  
    -   **snapshots.io_virtual_file_stats**  
  
-   Abfragetext und -plan  
  
    -   snapshots.notable_query_text  
  
    -   snapshots.notable_query_plan  
  
-   Normalisierte Abfragestatistik  
  
    -   snapshots.distinct_queries  
  
    -   snapshots.distinct_query_to_handle  
  
 **Custom_snapshots-Schema**  
  
 Das custom_snapshots-Schema beschreibt die neuen Tabellen und Sichten, die erstellt werden, wenn mithilfe von Standard- oder Sammlertypen von Drittanbietern benutzerdefinierte Sammlungssätze erstellt werden. Jeder Sammlertyp, für den eine neue Datentabelle für ein Sammelelement erforderlich ist, kann diese Tabelle in diesem Schema erstellen. Neue Tabellen können in diesem Schema von Mitgliedern der mdw_writer-Rolle hinzugefügt werden. Alle anderen Änderungen am Schema können nur von Mitgliedern der mdw_admin-Rolle vorgenommen werden.  
  
 Detaillierte Informationen zu Datentyp und Inhalt für die Datenbanktabellenspalten erhalten Sie, indem Sie die Dokumentation für die entsprechende gespeicherte Prozedur des Datensammlers für die einzelnen Tabellen lesen.  
  
### <a name="best-practices"></a>Bewährte Methoden  
 Für die Arbeit mit dem Verwaltungs-Data Warehouse werden die folgenden bewährten Methoden empfohlen:  
  
-   Ändern Sie die Metadaten der Tabellen im Verwaltungs-Data Warehouse nicht, außer Sie fügen einen neuen Sammlertyp hinzu.  
  
-   Ändern Sie die Daten nicht direkt im Verwaltungs-Data Warehouse. Durch Ändern der gesammelten Daten werden die gesammelten Daten ungültig.  
  
-   Statt direkt auf die Tabellen zuzugreifen, sollten Sie zum Zugriff auf Instanz- und Anwendungsdaten die dokumentierten gespeicherten Prozeduren und Funktionen verwenden, die vom Datensammler bereitgestellt werden. Die Tabellennamen und -definitionen können sich ändern. Sie ändern sich mit Sicherheit, wenn Sie die Anwendung aktualisieren. Darüber hinaus kann es auch in künftigen Versionen zu geänderten Tabellennamen und -definitionen kommen.  
  
## <a name="change-history"></a>Änderungsverlauf  
  
|Aktualisierter Inhalt|  
|---------------------|  
|Die Tabelle core.performance_counter_report_group_items wurde dem Abschnitt „Core-Schema“ hinzugefügt.|  
|Die Liste von Tabellen im Abschnitt "Momentaufnahme-Schema" wurde aktualisiert. snapshots.os_memory_clerks,snapshots.sql_process_and_system_memory und snapshots.io_virtual_file_stats wurden hinzugefügt. snapshots.os_process_memory und snapshots.distinct_query_stats wurden entfernt.|  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für das Verwaltungs-Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)   
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [Anzeigen eines Sammlungssatzberichts &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
  
