---
title: Sp_replshowcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 74526c46a3758829a89c71d41c071070ec907d5f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Befehle für Transaktionen, die für die Replikation in lesbarem Format markiert sind, zurück. **Sp_replshowcmds** kann nur wenn Clientverbindungen (einschließlich der aktuellen Verbindung) keine lesen Transaktionen aus dem Protokoll replizierte ausgeführt werden. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@maxtrans** =] *Maxtrans*  
 Die Anzahl der Transaktionen, über die Informationen zurückgegeben werden sollen. *Maxtrans* ist **Int**, hat den Standardwert **1**, gibt die maximale Anzahl von Transaktionen mit ausstehender Replikation für die **Sp_replshowcmds** Gibt Informationen zurück.  
  
## <a name="result-sets"></a>Resultsets  
 **Sp_replshowcmds** ist eine Diagnoseprozedur, die Informationen zur Veröffentlichungsdatenbank zurückgibt, von der er ausgeführt wird.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|Sequenznummer des Befehls.|  
|**originator_id**|**int**|ID des befehlsabsenders immer **0**.|  
|**publisher_database_id**|**int**|ID der Verlegerdatenbank immer **0**.|  
|**article_id**|**int**|ID des Artikels.|  
|**type**|**int**|Der Typ des Befehls.|  
|**Befehl**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehl.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_replshowcmds** wird bei der Transaktionsreplikation verwendet.  
  
 Mit **Sp_replshowcmds**, sehen Sie Transaktionen, die zurzeit nicht verteilt (die Transaktionen im Transaktionsprotokoll verbleiben, die nicht an den Verteiler gesendet wurden).  
  
 Clients, auf denen **Sp_replshowcmds** und **Sp_replcmds** innerhalb derselben Datenbank erhalten den Fehler 18752.  
  
 Um diesen Fehler zu vermeiden, muss der erste Client die Verbindung trennen oder die Rolle des Clients als Protokollleser muss freigegeben werden, indem ausführen **Sp_replflush**. Nachdem alle Clients aus der Protokollleser getrennt haben **Sp_replshowcmds** kann erfolgreich ausgeführt werden.  
  
> [!NOTE]  
>  **Sp_replshowcmds** sollte nur zur Problembehandlung bei der Replikation ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_replshowcmds**.  
  
## <a name="see-also"></a>Siehe auch  
 [Fehlermeldungen](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [Sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [Sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
