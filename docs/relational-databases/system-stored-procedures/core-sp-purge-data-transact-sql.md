---
title: sp_purge_data (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_purge_data_TSQL
- sp_purge_data
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_data
- management data warehouse, data collector stored procedures
- core.sp_purge_data stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 056076c3-8adf-4f51-8a1b-ca39696ac390
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb74c4993f7a7d013e56061e3a572052c2939a99
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="coresppurgedata-transact-sql"></a>core.sp_purge_data (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt Daten basierend auf einer Beibehaltungsrichtlinie aus dem Verwaltungs-Data Warehouse. Diese Prozedur wird täglich ausgeführt, durch Mdw_purge_data[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag für das Management Datawarehouse mit der angegebenen Instanz verknüpft ist. Sie können mit dieser gespeicherten Prozedur Daten aus dem Verwaltungs-Data Warehouse bedarfsgesteuert entfernen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
core.sp_purge_data  
    [ [ @retention_days = ] retention_days ]  
    [ , [ @instance_name = ] 'instance_name' ]  
    [ , [ @collection_set_uid = ] 'collection_set_uid' ]  
    [ , [ @duration = ] duration ]  
```  
  
## <a name="arguments"></a>Argumente  
 [@retention_days =] *Retention_days*  
 Die Anzahl der Tage für die Beibehaltung von Daten in den Verwaltungs-Data Warehouse-Tabellen. Daten mit einem Zeitstempel, die älter sind als *Retention_days* wird entfernt. *Retention_days* ist **"smallint"**, hat den Standardwert NULL. Wenn angegeben, muss der Wert positiv sein. Wenn der Wert NULL ist, legt der Wert in der valid_through-Spalte in der core.snapshots-Sicht die Zeilen fest, die entfernt werden können.  
  
 [@instance_name =] '*Instance_name*"  
 Der Name der Instanz für den Sammlungssatz. *Instanzname* ist **Sysname**, hat den Standardwert NULL.  
  
 *Instanzname* muss der vollqualifizierte Instanzname sein, besteht aus den Computernamen und den Instanznamen im Format *Computername*\\*Instancename*. Wenn der Wert NULL ist, wird die Standardinstanz auf dem lokalen Server verwendet.  
  
 [@collection_set_uid = ] '*collection_set_uid*'  
 Die GUID für den Sammlungssatz. *collection_set_uid* is **uniqueidentifier**, with a default of NULL. Wenn der Wert NULL ist, werden die qualifizierenden Zeilen aus allen Sammlungssätzen entfernt. Um diesen Wert abzurufen, fragen Sie die syscollector_collection_sets-Katalogsicht ab.  
  
 [@duration =] *Dauer*  
 Die maximale Anzahl der Minuten für die Ausführung des Entfernen-Vorgangs. *Dauer* ist **"smallint"**, hat den Standardwert NULL. Wenn dieser Wert angegeben ist, muss er 0 (null) oder eine positive ganze Zahl sein. Wenn der Wert NULL ist, wird der Vorgang so lange ausgeführt, bis alle gekennzeichneten Zeilen entfernt sind oder bis der Vorgang manuell beendet wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Diese Prozedur wählt Zeilen in der core.snapshots-Sicht aus, die in Abhängigkeit einer Beibehaltungsdauer entfernt werden können. Alle für die Entfernung gekennzeichneten Zeilen werden aus der core.snapshots_internal-Tabelle gelöscht. Das Löschen der vorangehenden Zeilen löst eine Löschweitergabe (cascading delete) in allen Verwaltungs-Data Warehouse-Tabellen aus. Dies wird durch die Verwendung der ON DELETE CASCADE-Klausel erzielt, die für alle Tabellen definiert wird, in denen gesammelte Daten gespeichert werden.  
  
 Jede Momentaufnahme wird mit den zugeordneten Daten in einer expliziten Transaktion gelöscht. Anschließend wird ein Commit ausgeführt. Aus diesem Grund, wenn der entfernen-Vorgangs manuell beendet wurde oder der angegebene Wert für @duration überschritten wird, nur die nicht gespeicherte Daten bleiben. Diese Daten können bei der nächsten Ausführung des Auftrags entfernt werden.  
  
 Die Prozedur muss im Kontext der Verwaltungs-Data Warehouse-Datenbank ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Mdw_admin** (mit EXECUTE-Berechtigung) erforderlich ist.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-running-sppurgedata-with-no-parameters"></a>A. Ausführen von "sp_purge_data" ohne Parameter  
 Im folgenden Beispiel wird core.sp_purge_data ohne Angabe von Parametern ausgeführt. Daher wird der Standardwert NULL mit dem zugeordneten Verhalten für alle Parameter verwendet.  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data;  
GO  
```  
  
### <a name="b-specifying-retention-and-duration-values"></a>B. Angeben von Werten für Beibehalten und Dauer  
 Im folgenden Beispiel werden Daten aus dem Verwaltungs-Data Warehouse entfernt, die älter als 7 Tage sind. Darüber hinaus die @duration Parameter angegeben wird, sodass der Vorgang nicht länger als 5 Minuten ausgeführt wird.  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data @retention_days = 7, @duration = 5;  
GO  
```  
  
### <a name="c-specifying-an-instance-name-and-collection-set"></a>C. Angeben eines Instanznamens und eines Sammlungssatzes  
 Im folgenden Beispiel werden Daten aus dem Verwaltungs-Data Warehouse für einen bestimmten Sammlungssatz in der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt. Da @retention_days nicht angegeben ist, wird der Wert in der Valid_through-Spalte in der core.snapshots-Sicht wird verwendet, um die Zeilen für den Sammlungssatz festzulegen, die entfernt werden.  
  
```  
USE <management_data_warehouse>;  
GO  
-- Get the collection set unique identifier for the Disk Usage system collection set.  
DECLARE @disk_usage_collection_set_uid uniqueidentifier = (SELECT collection_set_uid   
    FROM msdb.dbo.syscollector_collection_sets WHERE name = N'Disk Usage');   
  
EXECUTE core.sp_purge_data @instance_name = @@SERVERNAME, @collection_set_uid = @disk_usage_collection_set_uid;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Prozeduren für den Datensammler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
