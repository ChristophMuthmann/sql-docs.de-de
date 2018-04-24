---
title: Implementieren von DDL-Triggern | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: triggers
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-ddl
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DDL triggers, implementing
ms.assetid: f44e5340-1d18-40e9-828e-0ffcca091ae3
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ee5bb8bfa415a13edfbb3f53c91492d3e20af5a0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="implement-ddl-triggers"></a>Implementieren von DDL-Triggern
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Dieses Thema enthält Informationen, die Ihnen beim Erstellen von DDL-Triggern, Ändern von DDL-Triggern sowie Deaktivieren oder Löschen von DDL-Triggern helfen sollen.  
  
## <a name="creating-ddl-triggers"></a>Erstellen von DDL-Triggern  
 DDL-Trigger werden mithilfe der CREATE TRIGGER-Anweisung von [!INCLUDE[tsql](../../includes/tsql-md.md)] für DDL-Trigger erstellt.  
  
 **So erstellen Sie einen DDL-Trigger**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
> [!IMPORTANT]  
>  Die Fähigkeit, Resultsets aus Triggern zurückzugeben, wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entfernt. Durch Trigger, die Resultsets zurückgeben, kann es in Anwendungen, die hierfür nicht konzipiert wurden, zu unerwartetem Verhalten kommen. Vermeiden Sie deshalb bei Neuentwicklungen, Resultsets aus Triggern zurückzugeben, und planen Sie die Änderung von Anwendungen, in denen dies derzeit verwendet wird. Legen Sie die Option [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Ergebnisse von Triggern nicht zulassen [auf 1 fest, um zu verhindern, dass Trigger in](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) Resultsets zurückgeben. In einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird die Standardeinstellung für die Option 1 sein.  
  
## <a name="modifying-ddl-triggers"></a>Ändern von DDL-Triggern  
 Wenn Sie die Definition eines DDL-Triggers ändern müssen, können Sie den Trigger entweder löschen und neu erstellen oder den vorhandenen Trigger in einem einzigen Schritt neu definieren.  
  
 Wenn Sie den Namen eines Objekts ändern, auf das ein DDL-Trigger verweist, müssen Sie den Trigger so ändern, dass sein Text den neuen Namen widerspiegelt. Bevor Sie ein Objekt umbenennen, sollten Sie daher erst die Abhängigkeiten des Objekts anzeigen, um feststellen zu können, ob Trigger von der beabsichtigten Änderung betroffen sind.  
  
 Sie können einen Trigger auch ändern, um seine Definition zu verschlüsseln.  
  
 **So ändern Sie einen Trigger**  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
 **So zeigen Sie die Abhängigkeiten eines Triggers an**  
  
-   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
-   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
-   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
## <a name="disabling-and-dropping-ddl-triggers"></a>Deaktivieren und Löschen von DDL-Triggern  
 Wenn ein DDL-Trigger nicht mehr benötigt wird, kann er deaktiviert oder gelöscht werden.  
  
 Durch das Deaktivieren eines DDL-Triggers wird er nicht gelöscht. Der Trigger ist weiterhin als Objekt in der aktuellen Datenbank vorhanden. Der Trigger wird jedoch bei der Ausführung von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, für die er programmiert wurde, nicht ausgelöst. Deaktivierte DDL-Trigger können erneut aktiviert werden. Wenn ein DDL-Trigger aktiviert wird, wird er so ausgelöst wie nach seiner ursprünglichen Erstellung. DDL-Trigger werden beim Erstellen standardmäßig aktiviert.  
  
 Wenn ein DDL-Trigger gelöscht wird, wird er aus der aktuellen Datenbank gelöscht. Objekte oder Daten, für die der DDL-Trigger den Bereich besitzt, sind hiervon nicht betroffen.  
  
 **So deaktivieren Sie einen DDL-Trigger**  
  
-   [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **So aktivieren Sie einen DDL-Trigger**  
  
-   [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **So löschen Sie einen DDL-Trigger**  
  
-   [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)  
  
  
