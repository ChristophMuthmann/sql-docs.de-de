---
title: "Abrufen von Informationen zu DDL-Triggern | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-ddl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Metadaten [SQL Server], Trigger"
  - "Statusinformationen [SQL Server], DDL-Trigger"
  - "DDL-Trigger, Metadaten"
ms.assetid: 462becea-292a-4b9e-bb98-533e89733911
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Abrufen von Informationen zu DDL-Triggern
  Die in diesem Abschnitt aufgeführten Katalogsichten können zum Abrufen von Informationen zu DLL-Triggern verwendet werden.  
  
 **So rufen Sie Informationen zu Ereignissen oder Ereignisgruppen ab, bei denen ein DDL-Trigger ausgelöst werden kann**  
  
-   [sys.trigger_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-event-types-transact-sql.md)  
  
 **So zeigen Sie die Abhängigkeiten eines Triggers an**  
  
-   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
-   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
-   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
## Datenbankbezogene DLL-Trigger  
 **So rufen Sie Informationen zu datenbankbezogenen Triggern ab**  
  
-   [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
 **So rufen Sie Informationen zu Datenbankereignissen ab, die Trigger auslösen**  
  
-   [sys.trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)  
  
 **So zeigen Sie die Definition eines datenbankbezogenen Triggers an**  
  
-   [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)  
  
 **So rufen Sie Informationen zu auf CRL-Datenbanken bezogenen Trigger ab**  
  
-   [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)  
  
## Serverbezogene DLL-Trigger  
 **So rufen Sie Informationen zu serverbezogenen Triggern ab**  
  
-   [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)  
  
 **So rufen Sie Informationen zu Serverereignissen ab, die Trigger auslösen**  
  
-   [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)  
  
 **So zeigen Sie die Definition eines serverbezogenen Triggers an**  
  
-   [sys.server_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)  
  
 **So rufen Sie Informationen zu auf CRL-Server bezogenen Triggern ab**  
  
-   [sys.server_assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
## Siehe auch  
 [DDL-Trigger](../../relational-databases/triggers/ddl-triggers.md)  
  
  