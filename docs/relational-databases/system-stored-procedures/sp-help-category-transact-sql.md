---
title: Sp_help_category (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
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
- sp_help_category
- sp_help_category_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_category
ms.assetid: 8cad1dcc-b43e-43bd-bea0-cb0055c84169
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efec4c1ef04ef95e74ef13479b5f51cfe2d84bdb
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpcategory-transact-sql"></a>sp_help_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stellt Informationen zu den angegebenen Klassen von Aufträgen, Warnungen oder Operatoren bereit.  
   
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_help_category [ [ @class = ] 'class' ]   
     [ , [ @type = ] 'type' ]   
     [ , [ @name = ] 'name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argumente  
 [  **@class=**] **"***Klasse***"**  
 Die Klasse, zu der Informationen angefordert werden. *Klasse* ist **varchar(8)**, hat den Standardwert des **Auftrag**. *Klasse* kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**AUFTRAG**|Stellt Informationen zu einer Auftragskategorie bereit.|  
|**WARNUNG**|Stellt Informationen zu einer Warnungskategorie bereit.|  
|**OPERATOR**|Stellt Informationen zu einer Operatorkategorie bereit.|  
  
 [  **@type=** ] **"***Typ***"**  
 Der Typ der Kategorie, für die Informationen angefordert werden. *Typ* ist **varchar(12)**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**LOKALE**|Lokale Auftragskategorie|  
|**MULTI-SERVER**|Multiserver-Auftragskategorie|  
|**NONE**|Kategorie für eine andere Klasse als **Auftrag**.|  
  
 [  **@name=** ] **"***Namen***"**  
 Der Name der Kategorie, für die Informationen angefordert werden. *name* ist vom Datentyp **sysname**und hat den Standardwert NULL.  
  
 [  **@suffix=** ] *Suffix*  
 Gibt an, ob die **Category_type** Spalte im Resultset wird eine ID oder einen Namen. *Suffix* ist **Bit**, hat den Standardwert **0**. **1** zeigt die **Category_type** als einen Namen und **0** angezeigt wird, eine ID ein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Wenn  **@suffix**  ist **0**, **Sp_help_category** gibt das folgende Resultset zurück:  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|Kategorie-ID|  
|**category_type**|**tinyint**|Der Typ der Kategorie:<br /><br /> **1** = lokal<br /><br /> **2** = Multiserver<br /><br /> **3** = keine|  
|**name**|**sysname**|Kategoriename|  
  
 Wenn  **@suffix**  ist **1**, **Sp_help_category** gibt das folgende Resultset zurück:  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|Kategorie-ID|  
|**category_type**|**sysname**|Art der Kategorie: Einer der **lokale**, **mit mehreren Servern**, oder **NONE**|  
|**name**|**sysname**|Kategoriename|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_help_category** muss ausgeführt werden, aus der **Msdb** Datenbank.  
  
 Werden keine Parameter angegeben, stellt das Resultset Informationen zu allen Auftragskategorien bereit.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-local-job-information"></a>A. Zurückgeben von Informationen zu lokalen Aufträgen  
 Im folgenden Beispiel werden Informationen zu Aufträgen zurückgegeben, die lokal verwaltet werden.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @type = N'LOCAL' ;  
GO  
```  
  
### <a name="b-returning-alert-information"></a>B. Zurückgeben von Warnungsinformationen  
 Im folgenden Beispiel werden Informationen zur Warnungskategorie für die Replikation zurückgegeben.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @class = N'ALERT',  
    @name = N'Replication' ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_add_category &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [Sp_delete_category &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [Sp_update_category &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
