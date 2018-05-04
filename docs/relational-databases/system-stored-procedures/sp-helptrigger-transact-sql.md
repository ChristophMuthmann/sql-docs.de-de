---
title: "\"sp_helptrigger\" (Transact-SQL) | Microsoft Docs"
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 003d14b4c74775a891599f2c3a7451e6bf1928ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelptrigger-transact-sql"></a>sp_helptrigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Typen der DML-Trigger zurück, die in der angegebenen Tabelle für die aktuelle Datenbank definiert sind. "sp_helptrigger" kann nicht mit DDL-Triggern verwendet werden. Abfrage der [gespeicherte Systemprozeduren](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) stattdessen die Katalogsicht.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@tabname=** ] **"***Tabelle***"**  
 Der Name der Tabelle in der aktuellen Datenbank, für die Triggerinformationen zurückgegeben werden sollen. *Tabelle* ist **nvarchar(776)**, hat keinen Standardwert.  
  
 [ **@triggertype=** ] **'***type***'**  
 Der Typ des DML-Triggers, zu dem Informationen zurückgegeben werden sollen. *Typ* ist **char(6)**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**DELETE**|Gibt DELETE-Triggerinformationen zurück.|  
|**INSERT**|Gibt INSERT-Triggerinformationen zurück.|  
|**UPDATE**|Gibt UPDATE-Triggerinformationen zurück.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Die folgende Tabelle zeigt die im Resultset enthaltenen Informationen an.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|Name des Triggers.|  
|**trigger_owner**|**sysname**|Name des Besitzers der Tabelle, für die der Trigger definiert ist.|  
|**isupdate**|**int**|1=UPDATE-Trigger<br /><br /> 0=Kein UPDATE-Trigger|  
|**isdelete**|**int**|1=DELETE-Trigger<br /><br /> 0=Kein DELETE-Trigger|  
|**isinsert**|**int**|1=INSERT-Trigger<br /><br /> 0=Kein INSERT-Trigger|  
|**isafter**|**int**|1=AFTER-Trigger<br /><br /> 0=Kein AFTER-Trigger|  
|**isinsteadof**|**int**|1=INSTEAD OF-Trigger<br /><br /> 0=Kein INSTEAD OF-Trigger|  
|**trigger_schema**|**sysname**|Name des Schemas, zu dem der Trigger gehört.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert [die Konfiguration der Metadatensichtbarkeit](../../relational-databases/security/metadata-visibility-configuration.md) -Berechtigung für die Tabelle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `sp_helptrigger` ausgeführt, um Informationen zu den Triggern in der `Person.Person`-Tabelle zu erzeugen.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
