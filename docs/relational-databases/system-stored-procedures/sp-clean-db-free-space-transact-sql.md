---
title: Sp_clean_db_free_space (Transact-SQL) | Microsoft Docs
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
- sp_clean_db_free_space_TSQL
- sp_clean_db_free_space
dev_langs: TSQL
helpviewer_keywords:
- sp_clean_db_free_space
- ghost records
ms.assetid: faa96f7e-be92-47b1-8bc5-4dbba5331655
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: caa993ac619beb627c6f0e5a486c72af4e323f96
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spcleandbfreespace-transact-sql"></a>sp_clean_db_free_space (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt restliche aufgrund der Datenänderungsroutinen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf Datenbankseiten belassene Informationen. sp_clean_db_free_space bereinigt alle Seiten in allen Dateien der Datenbank.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_clean_db_free_space   
[ @dbname ] = 'database_name'   
[ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @dbname=] '*Database_name*"  
 Der Name der zu bereinigenden Datenbank. *Dbname* ist **Sysname** und darf nicht NULL sein.  
  
 [ @cleaning_delay=] '*Delay_in_seconds*"  
 Gibt das Intervall zwischen dem Bereinigen von Seiten an. Hierdurch werden die Auswirkungen auf das E/A-System verringert. *Delay_in_seconds* ist **Int** hat den Standardwert 0.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 DELETE-Vorgänge aus einer Tabelle oder Updatevorgänge, aufgrund derer, die eine Zeile verschoben sofort auf einer Seite Speicherplatz kann durch Entfernen der Verweise auf die Zeile. Unter bestimmten Umständen kann die Zeile jedoch als inaktiver Datensatz (ghost record) weiter physisch auf der Datenseite vorhanden sein. Inaktive Datensätze werden regelmäßig durch einen im Hintergrund ausgeführten Prozess entfernt. Restdaten werden nicht zurückgegeben, durch die [!INCLUDE[ssDE](../../includes/ssde-md.md)] als Antwort auf Abfragen. In Umgebungen, in denen die physische Sicherheit der Daten- oder Sicherungsdateien gefährdet ist, können Sie jedoch die inaktiven Datensätze mithilfe von sp_clean_db_free_space löschen.  
  
 Die zum Ausführen von sp_clean_db_free_space erforderliche Dauer hängt von der Größe der Datei, dem freien Speicherplatz und der Kapazität des Datenträgers ab. Weil sich das Ausführen von sp_clean_db_free_space erheblich auf die E/A-Aktivität auswirken kann, sollten Sie diese Prozedur außerhalb der normalen Betriebszeit ausführen.  
  
 Vor dem Ausführen von sp_clean_db_free_space sollten Sie eine vollständige Datenbanksicherung durchführen.  
  
 Die verwandte [Sp_clean_db_file_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md) gespeicherte Prozedur kann eine einzelne Datei bereinigt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der Datenbankrolle db_owner.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Restinformationen aus der `AdventureWorks2012`-Datenbank gelöscht.  
  
```  
USE master;  
GO  
EXEC sp_clean_db_free_space   
@dbname = N'AdventureWorks2012' ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
