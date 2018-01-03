---
title: Dynamische Verwaltungssichten (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- database scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], about dynamic management objects
- server state information [SQL Server]
- dynamic management functions [SQL Server]
- metadata [SQL Server], dynamic management objects
- dynamic management views [SQL Server]
- DMVs [SQL Server]
- functions [SQL Server], dynamic management
- server scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server]
ms.assetid: cf893ecb-0bf6-4cbf-ac00-8a1099e405b1
caps.latest.revision: "41"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 803982ea5e9ce81d280eeb4ba09319d671d6a87c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="system-dynamic-management-views"></a>Dynamische Verwaltungssichten System
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Dynamische Verwaltungssichten (DMVs) und -funktionen geben Serverstatusinformationen zurück, mit denen der Zustand einer Serverinstanz überwacht, Probleme diagnostiziert und die Leistung optimiert werden kann.  
  
> [!IMPORTANT]  
>  Dynamische Verwaltungssichten und -funktionen geben interne, implementierungsspezifische Statusdaten zurück. Die Schemas und die zurückgegebenen Daten können in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geändert werden. Deshalb kann es sein, dass dynamische Verwaltungssichten und -funktionen in zukünftigen Versionen nicht mit den dynamischen Verwaltungssichten und -funktionen in dieser Version kompatibel sind. In zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erweitert Microsoft möglicherweise die Definition der dynamischen Verwaltungssichten, indem am Ende der Spaltenliste z.B. Spalten hinzugefügt werden. Von der Verwendung der Syntax `SELECT * FROM dynamic_management_view_name` im Produktionscode wird abgeraten, da sich die Anzahl der zurückgegebenen Spalten möglicherweise ändert und Ihre Anwendung dadurch beschädigt werden kann.  
  
 Es gibt zwei Arten von dynamischen Verwaltungssichten und -funktionen:  
  
-   Dynamische Verwaltungssichten und -funktionen mit Serverbereich. Sie erfordern die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
-   Dynamische Verwaltungssichten und -funktionen mit Datenbankbereich. Sie erfordern die VIEW DATABASE STATE-Berechtigung für die Datenbank.  
  
## <a name="querying-dynamic-management-views"></a>Abfragen von dynamischen Verwaltungssichten  
 Auf dynamische Verwaltungssichten kann in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen mithilfe zweiteiliger, dreiteiliger oder vierteiliger Namen verwiesen werden. Auf dynamische Verwaltungsfunktionen kann andererseits in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen mithilfe zweiteiliger oder dreiteiliger Namen verwiesen werden. Auf dynamische Verwaltungssichten und -funktionen kann in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht mithilfe einteiliger Namen verwiesen werden.  
  
 Alle dynamischen Verwaltungssichten und -funktionen sind im sys-Schema vorhanden und verwenden die Benennungskonvention dm_*. Wenn Sie eine dynamische Verwaltungssicht oder -funktion verwenden, müssen Sie vor dem Namen der Sicht oder Funktion das sys-Schema als Präfix einfügen. Führen Sie z. B. die folgende Abfrage aus, um die dynamische Verwaltungssicht dm_os_wait_stats abzufragen:  
  
 ```sql
SELECT wait_type, wait_time_ms  
FROM sys.dm_os_wait_stats;  
```  
  
### <a name="required-permissions"></a>Erforderliche Berechtigungen  
 Zum Abfragen einer dynamischen Verwaltungssicht oder -funktion sind die SELECT-Berechtigung für das Objekt und die VIEW SERVER STATE- oder VIEW DATABASE STATE-Berechtigung erforderlich. Auf diese Weise können Sie den Zugriff eines Benutzers oder eines Anmeldenamens selektiv auf dynamische Verwaltungssichten und -funktionen einschränken. Dazu erstellen Sie zunächst den Benutzer in master und verweigern dem Benutzer dann die SELECT-Berechtigung für die dynamischen Verwaltungssichten oder -funktionen, auf die er keinen Zugriff haben soll. Der Benutzer kann dann diese dynamischen Verwaltungssichten oder -funktionen unabhängig vom Datenbankkontext des Benutzers nicht auswählen.  
  
> [!NOTE]  
>  DENY hat Vorrang. Daher kann ein Benutzer, dem die VIEW SERVER STATE-Berechtigung erteilt, aber die VIEW DATABASE STATE-Berechtigung verweigert wurde, zwar Informationen auf Serverebene, aber keine Informationen auf Datenbankebene anzeigen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 Dynamische Verwaltungssichten und -funktionen wurden in die folgenden Kategorien unterteilt.  
  
|||  
|-|-|  
|[AlwaysOn-Verfügbarkeit dynamische Verwaltungssichten und Funktionen (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)|[Dynamische Verwaltungssichten für Speicheroptimierte Tabelle &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)|  
|[Dynamische Verwaltungssichten in Bezug auf Change Data Capture &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/2a771d7d-693a-4f56-9227-02cd00e0e200)|[Objekt über verbundene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Nachverfolgen von Änderungen verbundene dynamische Verwaltungssichten](http://msdn.microsoft.com/library/dc8a0af9-fcd8-4c34-9453-5132717c9bdb)|[Abfragebenachrichtigungen verbundene dynamische Verwaltungssichten &#40; abgefragt werden Transact-SQL &#41;](http://msdn.microsoft.com/library/92eb22d8-33f3-4c17-b32e-e23acdfbd8f4)|  
|[Common Language Runtime in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)|[Mit der Replikation verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)|  
|[Datenbank-Spiegelungssitzung verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/04fb21de-1b5e-4a8e-9ca6-1b78ad278db1)|[Die Ressourcenkontrolle in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)|  
|[Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)|[Sicherheitsbezogene dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Ausführung bezogene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)|[Serverbezogene dynamische Verwaltungssichten und -funktionen (Transact-SQL)](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Dynamische Verwaltungssichten für erweiterte Ereignisse](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)|[Dynamische Verwaltungssichten in Verbindung mit Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)|  
|[FileStream und FileTable dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)|[Räumliche Daten beziehen, dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/c542ac38-451f-43a5-bf8c-4edd38bb738e)|  
|[Volltextsuche und semantische Suche dynamische Verwaltungssichten und Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)|[SQL Datawarehouse und dynamische Verwaltungssichten für Parallel Datawarehouse &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)|  
|[Geografische Replikation dynamische Verwaltungssichten und-Funktionen &#40; Azure SQL-Datenbank &#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)|[SQL Server-Betriebssystem in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)|  
|[Index-verbundene dynamische Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)|[Dynamische Verwaltungssichten für Stretch-Datenbank &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/1193efce-a105-49a9-a8b8-26b063485567)|  
|[Ich O in Verbindung mit dynamischen Verwaltungssichten und-Funktionen &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)|[Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)|  

  
## <a name="see-also"></a>Siehe auch  
 [Erteilen Sie Serverberechtigungen für &#40; Transact-SQL &#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)   
 [Erteilen der Datenbankberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)   
 [Systemsichten &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
