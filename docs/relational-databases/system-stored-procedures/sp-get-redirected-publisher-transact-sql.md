---
title: Sp_get_redirected_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_get_redirected_publisher_TSQL
- sp_get_redirected_publisher
ms.assetid: d47a9ab5-f2cc-42a8-8be9-a33895ce44f0
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 746f55b0230bf75ac835be901432d0e8eae278d0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spgetredirectedpublisher-transact-sql"></a>sp_get_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Wird von Replikations-Agents verwendet, um einen Verteiler abzufragen und zu bestimmen, ob der ursprüngliche Verleger umgeleitet wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@original_publisher** =] **"***Original_publisher***"**  
 Der Name der zu veröffentlichenden Datenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Der Name der zu veröffentlichenden Datenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@bypass_publisher_validation** = ] [0 | 1 ]  
 Wird verwendet, um die Überprüfung des umgeleiteten Verlegers zu umgehen. Bei 0 wird eine Überprüfung ausgeführt. Bei 1 wird keine Überprüfung durchgeführt. *Bypass_publisher_validation* ist **Bit**, hat den Standardwert 0.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|Der Name des Verlegers nach der Umleitung.|  
|**error_number**|**int**|Die Fehlernummer des Überprüfungsfehlers.|  
|**error_severity**|**int**|Der Schweregrad des Überprüfungsfehlers.|  
|**error_message**|**nvarchar(4000)**|Der Text der Überprüfungsfehlermeldung.|  
  
## <a name="remarks"></a>Hinweise  
 *Redirected_publisher* gibt die Namen des aktuellen Verlegers zurück. Gibt null, wenn der Verleger und veröffentlichte Datenbanken nicht umgeleitet wurden mit **Sp_redirect_publisher**.  
  
 Wenn keine Überprüfung angefordert wird, oder wenn kein Eintrag für den Verleger und die Veröffentlichungsdatenbank vorhanden ist *Error_number* und *Error_severity* geben 0 zurück und *Error_message* Gibt null zurück.  
  
 Wenn eine Überprüfung angefordert wird, wird die gespeicherte Prozedur [Sp_validate_redirected_publisher &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md) wird aufgerufen, um sicherzustellen, dass das Ziel der Umleitung ein geeigneter Host für die Veröffentlichung ist die Datenbank. Bei erfolgreicher Validierung **Sp_get_redirected_publisher** gibt den umgeleiteten Verlegernamen, 0 für die *Error_number* und *Error_severity* Spalten und Null in die *Error_message* Spalte.  
  
 Wenn eine Überprüfung angefordert wird und fehlschlägt, wird der umgeleitete Verlegername zusammen mit Fehlerinformationen zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Aufrufer muss entweder ein Mitglied der **Sysadmin** festen Serverrolle, die **Db_owner** festen Datenbankrolle "" für die Verteilungsdatenbank oder ein Mitglied einer veröffentlichungszugriffsliste für eine definierte Veröffentlichung der Verlegerdatenbank zugeordnet.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Replikationsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [Sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [Sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
