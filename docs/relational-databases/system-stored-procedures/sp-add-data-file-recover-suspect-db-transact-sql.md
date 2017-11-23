---
title: Sp_add_data_file_recover_suspect_db (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- sp_add_data_file_recover_suspect_db
- sp_add_data_file_recover_suspect_db_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_add_data_file_recover_suspect_db
ms.assetid: b25262aa-a228-48b7-8739-6581c760b171
caps.latest.revision: "51"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aca68c9bbbe8d8b16b80411dc2543699297737ba
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spadddatafilerecoversuspectdb-transact-sql"></a>sp_add_data_file_recover_suspect_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fügt einer Dateigruppe eine Datendatei hinzu, wenn die Wiederherstellung für eine Datenbank wegen unzureichendem Speicherplatzes (Fehler 1105) für die Dateigruppe nicht ausgeführt werden kann. Nachdem die Datei hinzugefügt wurde, deaktiviert diese gespeicherte Prozedur die Einstellung, die die Datenbank als fehlerverdächtig kennzeichnet, und führt die Wiederherstellung der Datenbank durch. Die Parameter sind dieselben wie für ALTER DATABASE *Database_name* Datei hinzufügen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_data_file_recover_suspect_db [ @dbName= ] 'database'   
    , [ @filegroup = ] 'filegroup_name'   
    , [ @name = ] 'logical_file_name'   
    , [ @filename= ] 'os_file_name'   
    , [ @size = ] 'size'   
    , [ @maxsize = ] 'max_size'   
    , [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@dbName=** ] **"***Datenbank* **"**  
 Der Name der Datenbank. *Datenbank* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@filegroup=** ] **"***Filegroup_name* **"**  
 Die Dateigruppe, der die angegebene Datei hinzugefügt werden soll. *Filegroup_name* ist **nvarchar(260)**, hat den Standardwert NULL, gibt die primäre Datei.  
  
 [  **@name=** ] **"***Logical_file_name* **"**  
 Der Name, der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Verweis auf die Datei verwendet wird. Der Name muss auf dem Server eindeutig sein. *Logical_file_name* ist **nvarchar(260)**, hat keinen Standardwert.  
  
 [  **@filename=** ] **"***logische* **"**  
 Der Pfad und der Dateiname, die vom Betriebssystem für die Datei verwendet werden. Die Datei muss sich auf einer Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s befinden. *physischer Dateiname* ist **nvarchar(260)**, hat keinen Standardwert.  
  
 [  **@size=** ] **"***Größe* **"**  
 Die Anfangsgröße der Datei. *Größe* ist **nvarchar(20)**, hat den Standardwert NULL. Geben Sie eine ganze Zahl; Verwenden Sie keine Dezimalzahl. Die Suffixe MB und KB können verwendet werden, um Megabyte bzw. Kilobyte als Einheit anzugeben. Die Standardeinheit ist MB. Der Mindestwert ist 512 KB. Wenn *Größe* nicht angegeben ist, wird der Standardwert ist 1 MB.  
  
 [  **@maxsize=** ] **"***Max_size* **"**  
 Die maximale Größe, auf die die Datei vergrößert werden kann. *Max_size* ist **nvarchar(20)**, hat den Standardwert NULL. Geben Sie eine ganze Zahl; Verwenden Sie keine Dezimalzahl. Die Suffixe MB und KB können verwendet werden, um Megabyte bzw. Kilobyte als Einheit anzugeben. Die Standardeinheit ist MB.  
  
 Wenn *Max_size* nicht angegeben ist, wird die Datei wird vergrößert, bis der Datenträger voll ist. Das Anwendungsprotokoll von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows warnt den Administrator, bevor der Speicherplatz auf einem Datenträger erschöpft ist.  
  
 [  **@filegrowth=** ] **"***Growth_increment* **"**  
 Die Menge an Speicherplatz, die der Datei jedes Mal dann hinzugefügt wird, wenn neuer Speicherplatz erforderlich wird. *Growth_increment* ist **nvarchar(20)**, hat den Standardwert NULL. Durch den Wert 0 wird angezeigt, dass die Datei nicht vergrößert wird. Geben Sie eine ganze Zahl; Verwenden Sie keine Dezimalzahl. Der Wert kann in MB, KB oder Prozent (%) angegeben werden. Wenn der Wert in Prozent angegeben wird, ist growth increment der angegebene Prozentsatz der Dateigröße zum Zeitpunkt der Vergrößerung. Bei Zahlen ohne Angabe von MB, KB oder % wird standardmäßig MB verwendet.  
  
 Wenn *Growth_increment* NULL ist, der Standardwert ist 10 % und der Mindestwert beträgt 64 KB. Die angegebene Größe wird auf den nächsten durch 64 KB teilbaren Wert gerundet.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Ausführungsberechtigungen erhält standardmäßig die Mitglieder der **Sysadmin** festen Serverrolle "". Diese Berechtigungen sind nicht übertragbar.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wurde die `db1`-Datenbank bei der Wiederherstellung aufgrund unzureichenden Speicherplatzes (Fehler 1105) in der `fg1`-Dateigruppe als fehlerverdächtig gekennzeichnet.  
  
```  
USE master;  
GO  
EXEC sp_add_data_file_recover_suspect_db db1, fg1, file2,  
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_file2.mdf', '1MB';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Sp_add_log_file_recover_suspect_db &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
