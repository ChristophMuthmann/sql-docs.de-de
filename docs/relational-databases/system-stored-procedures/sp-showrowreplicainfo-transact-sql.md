---
title: Sp_showrowreplicainfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords:
- sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d584c011b61c8b8ad9e3fc55f10a1e7a2512fa97
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spshowrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Zeigt Informationen zu einer Zeile in einer Tabelle an, die als ein Artikel in einer Mergereplikation verwendet wird. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@ownername** =] **"***%ownername***"**  
 Der Name des Tabellenbesitzers. *%ownername* ist **Sysname**, hat den Standardwert NULL. Dieser Parameter ist hilfreich für differenzierte Tabellen, wenn eine Datenbank mehrere Tabellen mit dem gleichen Namen enthält, aber jede Tabelle einen unterschiedlichen Besitzer aufweist.  
  
 [  **@tablename =**] **"***Tablename***"**  
 Der Name der Tabelle, die die Zeile enthält, für die die Informationen zurückgegeben werden. *TableName* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@rowguid =**] *Rowguid*  
 Der eindeutige Bezeichner der Zeile. *ROWGUID* ist **"uniqueidentifier"**, hat keinen Standardwert.  
  
 [  **@show** =] **"***anzeigen***"**  
 Bestimmt den Umfang der Informationen, die im Resultset zurückgegeben werden sollen. *anzeigen* ist **nvarchar(20)** hat den Standardwert von beiden. Wenn **Zeile**, nur Zeilenversionsinformationen zurückgegeben. Wenn **Spalten**, nur spaltenversionsinformationen zurückgegeben. Wenn **sowohl**, sowohl Zeilen-als auch spaltenversionsinformationen zurückgegeben.  
  
## <a name="result-sets-for-row-information"></a>Resultsets für Zeileninformationen  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Servername**|**sysname**|Name des Servers mit der Datenbank, in der der Eintrag der Zeilenversion vorgenommen wurde.|  
|**db_name**|**sysname**|Name der Datenbank, in der dieser Eintrag vorgenommen wurde.|  
|**db_nickname**|**Binary(6)**|Spitzname der Datenbank, in der dieser Eintrag vorgenommen wurde.|  
|**version**|**int**|Version des Eintrags.|  
|**current_state**|**vom Datentyp nvarchar(9)**|Gibt Informationen zum aktuellen Status der Zeile zurück.<br /><br /> **y** -Zeilendaten entspricht dem aktuellen Zustand der Zeile.<br /><br /> **n**-Die Zeilendaten stellt nicht den aktuellen Zustand der Zeile dar.<br /><br /> **\<n/v >** – nicht zutreffend.<br /><br /> **\<Unbekannte >** -aktuellen Zustand kann nicht bestimmt werden.|  
|**rowversion_table**|**NCHAR(17)**|Gibt an, ob die Zeilenversionen im rowsetcache der [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) Tabelle oder die [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) Tabelle.|  
|**Kommentar**|**nvarchar(255)**|Zusätzliche Informationen zu diesem Zeilenversionseintrag. Normalerweise ist dieses Feld leer.|  
  
## <a name="result-sets-for-column-information"></a>Resultsets für Spalteninformationen  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Servername**|**sysname**|Name des Servers mit der Datenbank, in der Eintrag der Spaltenversion vorgenommen wurde.|  
|**db_name**|**sysname**|Name der Datenbank, in der dieser Eintrag vorgenommen wurde.|  
|**db_nickname**|**Binary(6)**|Spitzname der Datenbank, in der dieser Eintrag vorgenommen wurde.|  
|**version**|**int**|Version des Eintrags.|  
|**colname**|**sysname**|Name der Artikelspalte, die der Eintrag der Spaltenversion darstellt.|  
|**Kommentar**|**nvarchar(255)**|Zusätzliche Informationen zu diesem Spaltenversionseintrag. Normalerweise ist dieses Feld leer.|  
  
## <a name="result-set-for-both"></a>Resultset für beide  
 Wenn der Wert **sowohl** ist für die ausgewählten *anzeigen*, und klicken Sie dann die Zeilen- und Resultsets zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 **Sp_showrowreplicainfo** wird bei der Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 **Sp_showrowreplicainfo** kann nur ausgeführt werden, von einem Mitglied der **Db_owner** festen Datenbankrolle "" für die Veröffentlichungsdatenbank oder von einem Mitglied der veröffentlichungszugriffsliste (PAL) für die Veröffentlichungsdatenbank.  
  
## <a name="see-also"></a>Siehe auch  
 [Erkennen und Lösen von Konflikten bei der Mergereplikation](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
