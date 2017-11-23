---
title: Sp_helpdb (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 365a72bec07a7da1dbec8e3fa695f60b314a273e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdb-transact-sql"></a>sp_helpdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu einer angegebenen Datenbank oder zu allen Datenbanken zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@dbname=** ] **"***Namen***"**  
 Der Name der Datenbank, für die Informationen ausgegeben werden. *Namen* ist **Sysname**, hat keinen Standardwert. Wenn *Namen* nicht angegeben ist, **Sp_helpdb** Informationen zu allen Datenbanken in der **sys.databases** -Katalogsicht angezeigt.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Datenbankname.|  
|**DB_SIZE**|**vom Datentyp nvarchar(13)**|Gesamtgröße der Datenbank.|  
|**Besitzer**|**sysname**|Datenbankbesitzer, z. B. **sa**.|  
|**DBID**|**smallint**|Datenbank-ID|  
|**erstellt**|**nvarchar(11)**|Erstellungsdatum der Datenbank.|  
|**status**|**nvarchar(600)**|Eine durch Trennzeichen getrennte Liste mit Werten von Datenbankoptionen, die zurzeit für die Datenbank festgelegt sind.<br /><br /> Optionen mit booleschen Werten werden nur aufgelistet, wenn sie aktiviert sind. Nicht boolesche Optionen sind aufgeführt, mit den entsprechenden Werten in Form von *Option_name*=*Wert*.<br /><br /> Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|**COMPATIBILITY_LEVEL**|**tinyint**|Datenbank-Kompatibilitätsgrad: 60, 65, 70, 80 oder 90.|  
  
 Wenn *Name* angegeben ist, es wurde ein zusätzliches Resultset, das die dateizuordnung für die angegebene Datenbank anzeigt.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**vom Typ NCHAR(128)**|Logischer Dateiname der Datei.|  
|**FileID**|**smallint**|Die Datei-ID|  
|**Dateiname**|**NCHAR(260)**|Betriebssystem-Dateiname (physischer Dateiname).|  
|**Dateigruppe**|**vom Datentyp nvarchar(128)**|Dateigruppe, zu der die Datei gehört.<br /><br /> NULL = Datei ist eine Protokolldatei. Sie gehört nie zu einer Dateigruppe.|  
|**Größe**|**nvarchar(18)**|Dateigröße in MB.|  
|**MaxSize**|**nvarchar(18)**|Maximale Größe, auf die die Datei vergrößert werden kann. Mit UNLIMITED in diesem Feld kann die Datei so lange vergrößert werden, bis der Datenträger voll ist.|  
|**Wachstum**|**nvarchar(18)**|Vergrößerungsinkrement der Datei. Hiermit wird die Menge des Speicherplatzes, der hinzugefügt wird, zu der Datei, die jedes Mal neuer Speicherplatz benötigt wird.|  
|**Verwendung**|**varchar(9)**|Verwendung der Datei. Für eine Datendatei ist der Wert **'nur Daten'** und der Wert ist für die Protokolldatei **'nur protokollieren'**.|  
  
## <a name="remarks"></a>Hinweise  
 Die **Status** Spalte im Resultset festlegen, Berichte, welche Optionen in der Datenbank auf ON festgelegt wurde haben. Alle Datenbankoptionen werden nicht gemeldet, indem Sie die **Status** Spalte. Um eine vollständige Liste der aktuellen datenbankoptionseinstellungen anzuzeigen, verwenden die **sys.databases** -Katalogsicht angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Wenn eine einzelne Datenbank angegeben wird, die Mitgliedschaft in der **öffentlichen** Rolle in der Datenbank ist erforderlich. Wenn keine Datenbank angegeben ist, Mitgliedschaft in der **öffentlichen** -Rolle in der **master** Datenbank muss angegeben werden.  
  
 Wenn eine Datenbank nicht zugegriffen werden kann, **Sp_helpdb** zeigt die Fehlermeldung 15622 und alle verfügbaren Informationen über die Datenbank an, wie möglich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-information-about-a-single-database"></a>A. Zurückgeben von Informationen für eine einzelne Datenbank  
 Im folgenden Beispiel werden Informationen zur [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank angezeigt.  
  
```tsql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>B. Zurückgeben von Informationen für alle Datenbanken  
 Im folgenden Beispiel werden Informationen zu allen Datenbanken auf dem Server mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angezeigt.  
  
```tsql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 ["Sys.FileGroups" &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Sys. master_files &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
