---
title: Sp_helpdatatypemap (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ac4661f7a7ae18487c63a3e4576fde06501a3fce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu den definierten datentypzuordnungen zwischen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank-Managementsystemen (DBMS). Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpdatatypemap [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @defaults_only = ] defaults_only ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@source_dbms**=] **"***Source_dbms***"**  
 Der Name des Datenbank-Managementsystems (Database Management System, DBMS), aus dem die Datentypen zugeordnet werden. *Source_dbms* ist **Sysname**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|Die Quelle ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|  
|**ORACLE**|Die Quelle ist eine Oracle-Datenbank.|  
  
 [ **@source_version**=] **"***Source_version***"**  
 Die Produktversion des Quell-DBMS. *Source_version*ist **varchar(10)**, und wenn nicht angegeben, die datentypzuordnungen für alle Versionen des Quell-DBMS zurückgegeben. Ermöglicht das Filtern des Resultsets nach der Quellversion des DBMS.  
  
 [ **@source_type**=] **"***Source_type***"**  
 Der im Quell-DBMS aufgelistete Datentyp. *Source_type* ist **Sysname**, und wenn nicht angegeben, werden die Zuordnungen für alle Datentypen im Quell-DBMS zurückgegeben. Ermöglicht das Filtern des Resultsets nach dem Datentyp im Quell-DBMS.  
  
 [ **@destination_dbms** =] **"***Destination_dbms***"**  
 Der Name des Ziel-DBMS. *Destination_dbms* ist **Sysname**, und kann einen der folgenden Werte.  
  
|Wert|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|Das Ziel ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|  
|**ORACLE**|Das Ziel ist eine Oracle-Datenbank.|  
|**DB2**|Das Ziel ist eine IBM DB2-Datenbank.|  
|**SYBASE**|Das Ziel ist eine Sybase-Datenbank.|  
  
 [ **@destination_version**=] **"***Destination_version***"**  
 Ist die Produktversion des Ziel-DBMS. *Destination_version*ist **varchar(10)**, und wenn nicht angegeben, werden die Zuordnungen für alle Versionen des Ziel-DBMS zurückgegeben. Ermöglicht das Filtern des Resultsets nach der Zielversion des DBMS.  
  
 [ **@destination_type**=] **"***Destination_type***"**  
 Der im Ziel-DBMS aufgelistete Datentyp. *Destination_type*ist **Sysname**, und wenn nicht angegeben, werden die Zuordnungen für alle Datentypen im Ziel-DBMS zurückgegeben. Ermöglicht das Filtern des Resultsets nach dem Datentyp im Ziel-DBMS.  
  
 [ **@defaults_only**=] *Defaults_only*  
 Gibt an, ob die Standard-Datentypzuordnungen zurückgegeben werden. *Defaults_only* ist **Bit**, hat den Standardwert **0**. **1** bedeutet, dass nur die standardmäßigen datentypzuordnungen zurückgegeben werden. **0** bedeutet, dass die Standardwebsite und benutzerdefinierte Daten datentypzuordnungen zurückgegeben werden.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**mapping_id**|Identifiziert eine Datentypzuordnung.|  
|**source_dbms**|Der Name und die Versionsnummer des Quell-DBMS.|  
|**source_type**|Der Datentyp im Quell-DBMS.|  
|**destination_dbms**|Der Name des Ziel-DBMS.|  
|**destination_type**|Der Datentyp im Ziel-DBMS.|  
|**is_default**|Gibt an, ob die Zuordnung eine Standardzuordnung oder eine alternative Zuordnung ist. Der Wert **0** gibt an, dass diese Zuordnung Benutzerdefiniert ist.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpdatatypemap** definiert datentypzuordnungen von nicht - SQL Server-Verlegern und von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verlegern zu nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Abonnenten.  
  
 Wenn die angegebene Kombination aus Quelle und Ziel-DBMS nicht unterstützt wird, **Sp_helpdatatypemap** gibt ein leeres Resultset zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** auf dem Verteiler oder Mitglieder der festen Serverrolle die **Db_owner** festen Datenbankrolle "" für die Verteilungsdatenbank kann ausführen **Sp_helpdatatypemap**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_getdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [Sp_setdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
