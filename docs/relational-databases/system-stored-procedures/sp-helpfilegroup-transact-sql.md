---
title: Sp_helpfilegroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpfilegroup_TSQL
- sp_helpfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfilegroup
ms.assetid: 619716b5-95dc-4538-82ae-4b90b9da8ebc
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b63d83c356be706dcff0fb6b80372c064f00742b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpfilegroup-transact-sql"></a>sp_helpfilegroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Namen und Attribute von Dateigruppen zurück, die der aktuellen Datenbank zugeordnet sind.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpfilegroup [ [ @filegroupname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@filegroupname =** ] **'***name***'**  
 Der logische Name einer beliebigen Dateigruppe in der aktuellen Datenbank. *name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Wenn *name* nicht angegeben ist, werden alle Dateigruppen in der aktuellen Datenbank aufgelistet, und nur das erste Resultset im Resultsetabschnitt wird angezeigt.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**groupname**|**sysname**|Name der Dateigruppe.|  
|**groupid**|**smallint**|Numerischer Dateigruppenbezeichner.|  
|**FileCount**|**int**|Die Anzahl von Dateien in der Dateigruppe.|  
  
 Wenn *name* angegeben ist, wird eine Zeile für jede Datei in der Dateigruppe zurückgegeben.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**file_in_group**|**sysname**|Der logische Name der Datei in der Dateigruppe.|  
|**fileid**|**smallint**|Numerischer Dateibezeichner.|  
|**Dateiname**|**NCHAR(260)**|Der physische Name der Datei, einschließlich des Verzeichnispfades.|  
|**size**|**nvarchar(15)**|Die Dateigröße in KB.|  
|**maxsize**|**nvarchar(15)**|Die maximale Größe der Datei.<br /><br /> Dies ist die maximale Größe, auf die die Datei vergrößert werden kann. Mit UNLIMITED in diesem Feld kann die Datei so lange vergrößert werden, bis der Datenträger voll ist.|  
|**growth**|**nvarchar(15)**|Vergrößerungsinkrement der Datei. Dies zeigt den Speicherplatz an, der jedes Mal der Datei hinzugefügt wird, wenn neuer Speicherplatz benötigt wird.<br /><br /> 0 = Die Datei weist eine feste Größe auf und wird nicht vergrößert.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-all-filegroups-in-a-database"></a>A. Zurückgeben aller Dateigruppen in einer Datenbank  
 Im folgenden Beispiel werden Informationen zu den Dateigruppen in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank zurückgegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup;  
GO  
```  
  
### <a name="b-returning-all-files-in-a-filegroup"></a>B. Zurückgeben aller Dateien in einer Dateigruppe  
 Im folgenden Beispiel werden Informationen zu allen Dateien in der `PRIMARY`-Dateigruppe der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank zurückgegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup 'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datenbankdateien und Dateigruppen](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
