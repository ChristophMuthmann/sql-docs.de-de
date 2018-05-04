---
title: Sp_helpfile (Transact-SQL) | Microsoft Docs
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
- sp_helpfile
- sp_helpfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: dc7dde2cbd3ec6b3361785b7d9f02931f812b730
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpfile-transact-sql"></a>sp_helpfile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die physischen Namen und Attribute der Dateien zurück, die der aktuellen Datenbank zugeordnet sind. Bestimmen Sie mithilfe dieser gespeicherten Prozedur die Namen von Dateien, die an den Server angefügt oder von diesem getrennt werden sollen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@filename =** ] **'***name***'**  
 Der logische Name einer beliebigen Datei in der aktuellen Datenbank. *name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Wenn *Namen* ist nicht angegeben ist, werden die Attribute aller Dateien in der aktuellen Datenbank zurückgegeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Logischer Dateiname der Datei.|  
|**fileid**|**smallint**|Numerischer Bezeichner der Datei. Wird nicht zurückgegeben, wenn *Namen* angegeben *.*|  
|**Dateiname**|**NCHAR(260)**|Physischer Dateiname.|  
|**filegroup**|**sysname**|Dateigruppe, zu der die Datei gehört.<br /><br /> NULL = Die Datei ist eine Protokolldatei. Sie gehört nie zu einer Dateigruppe.|  
|**size**|**nvarchar(15)**|Die Dateigröße in KB.|  
|**maxsize**|**nvarchar(15)**|Maximale Größe, auf die die Datei vergrößert werden kann. Mit UNLIMITED in diesem Feld kann die Datei so lange vergrößert werden, bis der Datenträger voll ist.|  
|**growth**|**nvarchar(15)**|Vergrößerungsinkrement der Datei. Zeigt die Menge an Speicherplatz an, die jedes Mal der Datei hinzugefügt wird, sobald neuer Speicherplatz erforderlich wird.<br /><br /> 0 = Die Datei weist eine feste Größe auf und wird nicht vergrößert.|  
|**Verwendung**|**varchar(9)**|Für die Datendatei ist der Wert **'nur Daten'** und der Wert ist für die Protokolldatei **'nur protokollieren'**.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt Informationen zu den Dateien in [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] zurück.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfile;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datenbankdateien und Dateigruppen](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
