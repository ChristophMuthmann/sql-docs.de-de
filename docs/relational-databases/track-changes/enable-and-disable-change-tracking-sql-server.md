---
title: "Aktivieren und Deaktivieren der &#196;nderungsnachverfolgung (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "08/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Änderungsnachverfolgung [SQL Server], deaktivieren"
  - "Datenänderungen [SQL Server]"
  - "Änderungsnachverfolgung [SQL Server], aktivieren"
  - "Nachverfolgen von Datenänderungen [SQL Server]"
  - "Änderungsnachverfolgung [SQL Server], konfigurieren"
  - "Daten [SQL Server], ändern"
ms.assetid: 1c92ec7e-ae53-4498-8bfd-c66a42a24d54
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Aktivieren und Deaktivieren der &#196;nderungsnachverfolgung (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie die Änderungsnachverfolgung für Datenbanken und Tabellen aktivieren und deaktivieren können.  
  
## Aktivieren der Änderungsnachverfolgung für eine Datenbank  
 Bevor Sie die Änderungsnachverfolgung verwenden können, müssen Sie die Änderungsnachverfolgung auf Datenbankebene aktivieren. Im folgenden Beispiel wird gezeigt, wie die Änderungsnachverfolgung mit [ALTER DATABASE](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)aktiviert werden kann.  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
```  
  
 Sie können die Änderungsnachverfolgung auch in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] aktivieren. Verwenden Sie hierzu das Dialogfeld [Datenbankeigenschaften &#40;Seite Änderungsnachverfolgung&#41;](../../relational-databases/databases/database-properties-changetracking-page.md).  
  
 Bei der Aktivierung der Änderungsnachverfolgung können Sie die CHANGE_RETENTION-Option und die AUTO_CLEANUP-Option angeben. Die Werte können Sie nach der Aktivierung der Änderungsnachverfolgung jederzeit ändern.  
  
 Der Änderungsbeibehaltungswert gibt den Zeitraum an, für den Änderungsnachverfolgungsinformationen geführt werden. Änderungsnachverfolgungsinformationen, die älter sind als der angegebene Zeitraum, werden in regelmäßigen Abständen entfernt. Bei der Festlegung dieses Werts ist zu berücksichtigen, wie häufig Anwendungen mit den Tabellen in der Datenbank synchronisiert werden. Die angegebene Beibehaltungsdauer muss wenigstens so lange sein wie der maximale Zeitraum zwischen Synchronisierungen. Ruft eine Anwendung Änderungen in längeren Intervallen ab, werden möglicherweise falsche Ergebnisse zurückgegeben, da einige Änderungsinformationen wahrscheinlich entfernt wurden. Zur Vermeidung falscher Ergebnisse kann eine Anwendung die CHANGE_TRACKING_MIN_VALID_VERSION-Systemfunktion verwenden, um zu ermitteln, ob das Intervall zwischen den Synchronisierungen zu lang war.  
  
 Mit der AUTO_CLEANUP-Option können Sie den Cleanup-Task aktivieren oder deaktivieren, mit dem alte Nachverfolgungsinformationen entfernt werden. Dies kann hilfreich sein, wenn ein temporäres Problem vorliegt, das eine Synchronisierung von Anwendungen verhindert, und der Prozess zum Entfernen von Änderungsnachverfolgungsinformationen, die älter sind als die Beibehaltungsdauer, angehalten werden muss, bis das Problem behoben wurde.  
  
 Beachten Sie generell für Datenbanken, für die die Änderungsnachverfolgung verwendet wird, Folgendes:  
  
-   Zur Verwendung der Änderungsnachverfolgung muss für den Datenbankkompatibilitätsgrad 90 oder höher festgelegt werden. Wenn eine Datenbank einen Kompatibilitätsgrad von weniger als 90 aufweist, können Sie die Änderungsnachverfolgung konfigurieren. Allerdings gibt dann die CHANGETABLE-Funktion, die verwendet wird, um Änderungsnachverfolgungsinformationen abzurufen, einen Fehler zurück.  
  
-   Die Momentaufnahmeisolation ist die einfachste Möglichkeit, die Konsistenz aller Änderungsnachverfolgungsinformationen sicherzustellen. Aus diesem Grund sollte für die Momentaufnahmeisolation für die Datenbank auf jeden Fall ON festgelegt werden. Weitere Informationen finden Sie unter [Verwenden der Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md).  
  
## Aktivieren der Änderungsnachverfolgung für eine Tabelle  
 Die Änderungsnachverfolgung muss für jede nachzuverfolgende Tabelle aktiviert werden. Nach der Aktivierung der Änderungsnachverfolgung werden für alle Zeilen in der Tabelle, die von einem DML-Vorgang betroffen sind, Änderungsnachverfolgungsinformationen beibehalten.  
  
 Im folgenden Beispiel wird gezeigt, wie die Änderungsnachverfolgung für eine Tabelle mit [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)aktiviert werden kann.  
  
```tsql  
ALTER TABLE Person.Contact  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
 Sie können die Änderungsnachverfolgung für eine Tabelle auch in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] aktivieren. Verwenden Sie hierzu das Dialogfeld [Tabelleneigenschaften &#40;Seite Änderungsnachverfolgung&#41;](../../relational-databases/databases/database-properties-changetracking-page.md).  
  
 Ist für die TRACK_COLUMNS_UPDATED-Option ON festgelegt, speichert [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in der internen Änderungsnachverfolgungstabelle zusätzliche Informationen dazu, welche Spalten aktualisiert wurden. Mit Spaltennachverfolgung kann eine Anwendung aktiviert werden, um nur die aktualisierten Spalten zu synchronisieren. Hiermit können Effizienz und Leistung gesteigert werden. Da die Verwaltung der Spaltennachverfolgungsinformationen jedoch zusätzlichen Speicherplatz beansprucht, ist diese Option standardmäßig deaktiviert.  
  
## Deaktivieren der Änderungsnachverfolgung für Datenbanken oder Tabellen  
 Die Änderungsnachverfolgung muss zunächst für alle Tabellen mit Änderungsnachverfolgung deaktiviert werden, bevor die Änderungsnachverfolgung auch für die Datenbank deaktiviert werden kann. Ermitteln Sie für eine Datenbank die Tabellen mit aktivierter Änderungsnachverfolgung mit der [sys.change_tracking_tables](../Topic/sys.change_tracking_tables%20\(Transact-SQL\).md)-Katalogsicht.  
  
 Wenn für keine Tabelle einer Datenbank Änderungen nachverfolgt werden, können Sie die Änderungsnachverfolgung für die Datenbank deaktivieren. Im folgenden Beispiel wird gezeigt, wie die Änderungsnachverfolgung für eine Datenbank mit [ALTER DATABASE](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)deaktiviert werden kann.  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF  
```  
  
 Im folgenden Beispiel wird gezeigt, wie die Änderungsnachverfolgung für eine Tabelle mit [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)deaktiviert werden kann.  
  
```tsql  
ALTER TABLE Person.Contact  
DISABLE CHANGE_TRACKING;  
```  
  
## Siehe auch  
 [Datenbankeigenschaften &#40;Seite Änderungsnachverfolgung&#41;](../../relational-databases/databases/database-properties-changetracking-page.md)   
 [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](../Topic/sys.change_tracking_databases%20\(Transact-SQL\).md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../Topic/sys.change_tracking_tables%20\(Transact-SQL\).md)   
 [Nachverfolgen von Datenänderungen &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Informationen zur Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [Arbeiten mit Änderungsdaten &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [Verwalten der Änderungsnachverfolgung &#40;SQL Server&#41;](../../relational-databases/track-changes/manage-change-tracking-sql-server.md)  
  
  