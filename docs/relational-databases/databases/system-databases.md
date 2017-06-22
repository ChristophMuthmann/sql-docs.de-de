---
title: Systemdatenbanken | Microsoft-Dokumentation
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
- system databases [SQL Server]
- displaying system database data
- modifying system data
- viewing system database data
ms.assetid: 30468a7c-4225-4d35-aa4a-ffa7da4f1282
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9ed6df401b8bdac3926c919d4dda039c2b4a1fa6
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="system-databases"></a>Systemdatenbanken
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enthält die folgenden Systemdatenbanken.  
  
|Systemdatenbank|Beschreibung|  
|---------------------|-----------------|  
|[master-Datenbank](../../relational-databases/databases/master-database.md)|Zeichnet alle Informationen auf Systemebene für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]auf.|  
|[msdb-Datenbank](../../relational-databases/databases/msdb-database.md)|Wird vom SQL Server-Agent verwendet, um Termine für Warnungen und Aufträge zu planen.|  
|[model-Datenbank](../../relational-databases/databases/model-database.md)|Wird als Vorlage für alle Datenbanken verwendet, die für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erstellt werden. Änderungen, die an der **model** -Datenbank vorgenommen werden, z. B. an der Datenbankgröße, der -sortierung, am Wiederherstellungsmodell und an anderen Datenbankoptionen, werden auf jede Datenbank angewendet, die anschließend erstellt wird.|  
|[Ressourcendatenbank](../../relational-databases/databases/resource-database.md)|Eine schreibgeschützte Datenbank, die Systemobjekte enthält, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]enthalten sind. Systemobjekte werden physisch in der **** Ressourcendatenbank gespeichert, logisch jedoch im **sys** -Schema jeder Datenbank angezeigt.|  
|[tempdb-Datenbank](../../relational-databases/databases/tempdb-database.md)|Ein Arbeitsbereich zum Speichern von temporären Objekten oder Zwischenresultsets.|  
  
## <a name="modifying-system-data"></a>Ändern von Systemdaten  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt keine direkten Updates der Informationen in Systemobjekten (z. B. Systemtabellen, gespeicherten Systemprozeduren und Katalogsichten) durch Benutzer. Stattdessen stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen vollständigen Satz administrativer Tools zur Verfügung, die Benutzern das umfassende Verwalten des Systems sowie aller Benutzer und Objekte in einer Datenbank ermöglichen. Dabei handelt es sich z. B. um:  
  
-   Verwaltungsprogramme, z. B. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   SQL-SMO-API. Über diese API können Programmierer vollständige Funktionen zum Verwalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in ihren Anwendungen bereitstellen.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts und gespeicherte Prozeduren. Diese können gespeicherte Systemprozeduren und [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL-Anweisungen verwenden.  
  
 Diese Tools schützen Anwendungen vor Änderungen an den Systemobjekten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss z. B. in neuen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einigen Fällen Änderungen an den Systemtabellen durchführen, um neue Funktionen in den jeweiligen Versionen zu unterstützen. Anwendungen, die SELECT-Anweisungen ausgeben, die direkt auf Systemtabellen verweisen, sind häufig auf das alte Format der Systemtabellen angewiesen. Standorte können möglicherweise erst dann auf eine neue Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisiert werden, nachdem die Anwendungen umgeschrieben wurden, die SELECT-Anweisungen für Systemtabellen ausführen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] berücksichtigt die durch gespeicherte Systemprozeduren, DDL und SQL-SMO veröffentlichten Schnittstellen, und versucht, die Abwärtskompatibilität dieser Schnittstellen aufrechtzuerhalten.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt keine Unterstützung für Trigger zur Verfügung, die für die Systemtabellen definiert wurden, da durch sie der Systembetrieb verändert werden kann.  
  
> [!NOTE]  
>  Systemdatenbanken dürfen nicht in Verzeichnissen von UNC-Freigaben enthalten sein.  
  
## <a name="viewing-system-database-data"></a>Anzeigen von System-Datenbankdaten  
 Sie sollten keine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen schreiben, von denen die Systemtabellen direkt abgefragt werden, es sei denn, Sie können die von der Anwendung benötigten Informationen nur auf diese Weise abrufen. Anwendungen sollten Katalog- und Systeminformationen mithilfe der folgenden Mechanismen abrufen:  
  
-   Systemkatalogsichten  
  
-   SQL-SMO  
  
-   WMI-Schnittstelle (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation)  
  
-   Katalogfunktionen, Methoden, Attribute oder Eigenschaften der in der Anwendung verwendeten Daten-API, z. B. ADO, OLE DB oder ODBC  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] : Gespeicherte Systemprozeduren und integrierte Funktionen  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Sichern und Wiederherstellen von Systemdatenbanken &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [Ausblenden von Systemobjekten im Objekt-Explorer](http://msdn.microsoft.com/library/c01d8804-838c-4f75-b78c-80e41e4fffdc)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
 [Datenbanken](../../relational-databases/databases/databases.md)  
  
  
