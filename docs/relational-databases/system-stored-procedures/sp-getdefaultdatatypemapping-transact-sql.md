---
title: Sp_getdefaultdatatypemapping (Transact-SQL) | Microsoft Docs
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
- sp_getdefaultdatatypemapping_TSQL
- sp_getdefaultdatatypemapping
helpviewer_keywords:
- sp_getdefaultdatatypemapping
ms.assetid: b8401de1-f135-41d0-ba79-ce8fe1f48c00
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 398ed7c0cfb5123b649901b91ef95b7c7282ab6e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spgetdefaultdatatypemapping-transact-sql"></a>sp_getdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zur standardzuordnung für den angegebenen Datentyp zwischen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und einem nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbank-Managementsystem (DBMS). Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_getdefaultdatatypemapping [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
        , [ @source_type = ] 'source_type'    
    [ , [ @source_length = ] source_length ]  
    [ , [ @source_precision = ] source_precision ]  
    [ , [ @source_scale = ] source_scale ]  
    [ , [ @source_nullable = ] source_nullable ]  
        , [ @destination_dbms = ] 'destination_dbms'   
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' OUTPUT ]  
    [ , [ @destination_length = ] destination_length OUTPUT ]  
    [ , [ @destination_precision = ] destination_precision OUTPUT ]  
    [ , [ @destination_scale = ] destination_scale OUTPUT ]  
    [ , [ @destination_nullable = ] source_nullable OUTPUT ]  
    [ , [ @dataloss = ] dataloss OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@source_dbms**=] **"***Source_dbms***"**  
 Der Name des Datenbank-Managementsystems (Database Management System, DBMS), aus dem die Datentypen zugeordnet werden. *Source_dbms* ist **Sysname**, und kann einen der folgenden Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|Die Quelle ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|  
|**ORACLE**|Die Quelle ist eine Oracle-Datenbank.|  
  
 Sie müssen diesen Parameter festlegen.  
  
 [  **@source_version=** ] **"***Source_version***"**  
 Die Versionsnummer des Quell-DBMS. *Source_version* ist **varchar(10)**, hat den Standardwert NULL.  
  
 [ **@source_type**=] **"***Source_type***"**  
 Der Datentyp im Quell-DBMS. *Source_type* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@source_length=** ] *Source_length*  
 Die Länge des Datentyps im Quell-DBMS. *Source_length* ist **"bigint"**, hat den Standardwert NULL.  
  
 [  **@source_precision=** ] *Source_precision*  
 Die Genauigkeit des Datentyps im Quell-DBMS. *Source_precision* ist **"bigint"**, hat den Standardwert NULL.  
  
 [  **@source_scale=** ] *Source_scale*  
 Die Dezimalstellen des Datentyps im Quell-DBMS. *Source_scale* ist **Int**, hat den Standardwert NULL.  
  
 [  **@source_nullable=** ] *Source_nullable*  
 Gibt an, ob der Datentyp im Quell-DBMS den Wert NULL unterstützt. *Source_nullable* ist **Bit**, hat den Standardwert des **1**, was bedeutet, dass NULL-Werte unterstützt werden.  
  
 [ **@destination_dbms** =] **"***Destination_dbms***"**  
 Der Name des Ziel-DBMS. *Destination_dbms* ist **Sysname**, und kann einen der folgenden Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|Das Ziel ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|  
|**ORACLE**|Das Ziel ist eine Oracle-Datenbank.|  
|**DB2**|Das Ziel ist eine IBM DB2-Datenbank.|  
|**SYBASE**|Das Ziel ist eine Sybase-Datenbank.|  
  
 Sie müssen diesen Parameter festlegen.  
  
 [ **@destination_version**=] **"***Destination_version***"**  
 Ist die Produktversion des Ziel-DBMS. *Destination_version* ist **varchar(10)**, hat den Standardwert NULL.  
  
 [ **@destination_type**=] **"***Destination_type***"** Ausgabe  
 Der im Ziel-DBMS aufgelistete Datentyp. *Destination_type* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@destination_length=** ] *Destination_length* Ausgabe  
 Die Länge des Datentyps im Ziel-DBMS. *Destination_length* ist **"bigint"**, hat den Standardwert NULL.  
  
 [  **@destination_precision=** ] *Destination_precision* Ausgabe  
 Ist die Genauigkeit des Datentyps im Ziel-DBMS. *Destination_precision* ist **"bigint"**, hat den Standardwert NULL.  
  
 [  **@destination_scale=** ] *Destination_scale *** Ausgabe**  
 Sind keine Dezimalstellen des Datentyps im Ziel-DBMS. *Destination_scale* ist **Int**, hat den Standardwert NULL.  
  
 [  **@destination_nullable=** ] *Destination_nullable *** Ausgabe**  
 Gibt an, ob der Datentyp im Ziel-DBMS den Wert NULL unterstützt. *Destination_nullable* ist **Bit**, hat den Standardwert NULL. **1** bedeutet, dass NULL-Werte unterstützt werden.  
  
 [  **@dataloss=** ] *Products *** Ausgabe**  
 Gibt an, ob bei der Zuordnung Datenverlust auftreten kann. *Products* ist **Bit**, hat den Standardwert NULL. **1** bedeutet, dass es besteht die Gefahr von Datenverlust.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_getdefaultdatatypemapping** wird für alle Replikationstypen zwischen verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und einem nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBMS.  
  
 **Sp_getdefaultdatatypemapping** gibt die Standard-Zieldaten-Typ, die bestmögliche Übereinstimmung mit dem Datentyp der angegebenen Quelle.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_getdefaultdatatypemapping**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [Sp_setdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle-Abonnenten](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
