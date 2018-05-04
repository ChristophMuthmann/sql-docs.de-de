---
title: Sys. fn_hadr_backup_is_preferred_replica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_backup_is_preferred_replica_TSQL
- sys.fn_hadr_backup_is_preferred_replica
- fn_hadr_backup_is_preferred_replica_TSQL
- fn_hadr_backup_is_preferred_replica
dev_langs:
- TSQL
helpviewer_keywords:
- backup on secondary replicas
- active secondary replicas [SQL Server], backup on secondary replicas
- sys.fn_hadr_backup_is_preferred_replica function
ms.assetid: 61b9be77-e2f6-4da1-b2ae-a62cbe226145
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3cf2513671262ec2a5e1d62755572e541f548a62
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnhadrbackupispreferredreplica--transact-sql"></a>Sys. fn_hadr_backup_is_preferred_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Dient zum Ermitteln, ob das aktuelle Replikat das bevorzugte Sicherungsreplikat ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_hadr_backup_is_preferred_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>Argumente  
 "*Dbname*"  
 Der Name der zu sichernden Datenbank. *Dbname* Typ Sysname ist.  
  
## <a name="returns"></a>Rückgabewert  
 Gibt 1 zurück, wenn die Datenbank auf der aktuellen Instanz das bevorzugte Replikat ist. Andernfalls wird 0 zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie diese Funktion in einem Sicherungsskript, um zu ermitteln, ob sich die aktuelle Datenbank auf dem für Sicherungen bevorzugten Replikat befindet. Sie können ein Skript über jedes Verfügbarkeitsreplikat ausführen. Jeder dieser Aufträge greift auf dieselben Daten ein, um zu bestimmen, welcher Auftrag auszuführen, nur eine der geplanten Aufträge in den Sicherungsstatus folglich wechselt eigentlich. Beispielcode kann sich wie folgt zusammensetzen.  
  
```  
If sys.fn_hadr_backup_is_preferred_replica( @dbname ) <> 1   
BEGIN  
-- If this is not the preferred replica, exit (probably without error).  
END  
-- If this is the preferred replica, continue to do the backup.  
  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-sysfnhadrbackupispreferredreplica"></a>A. Verwenden von sys.fn_hadr_backup_is_preferred_replica  
 Im folgenden Beispiel wird 1 zurückgegeben, wenn die aktuelle Datenbank dem bevorzugten Sicherungsreplikat entspricht.  
  
```  
SELECT sys.fn_hadr_backup_is_preferred_replica ('TestDB');  
GO  
```  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten & #40; SQLServer & #41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen Always On-Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [Aktive sekundäre Replikate: Sicherung auf sekundären Replikaten &#40;Always On-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)[Always On-Verfügbarkeitsgruppen Katalogsichten &#40;Transact-SQL    &#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)  
  
  
