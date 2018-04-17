---
title: Sp_replicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
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
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab96eb1cc914000666bb09e34b38974d1e9b9524
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Legt für die angegebene Datenbank eine Replikationsdatenbankoption fest. Diese gespeicherte Prozedur wird auf dem Verleger oder Abonnenten für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argumente  
 [**@dbname=**] **"***Dbname***"**  
 Die Datenbank, für die die Replikationsdatenbankoption festgelegt wird. *Db_name* ist **Sysname**, hat keinen Standardwert.  
  
 [**@optname=**] **"***Optname***"**  
 Die Replikationsdatenbankoption, die aktiviert oder deaktiviert werden soll. *Optname* ist **Sysname**, und kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Veröffentlichen von Merge**|Die Datenbank kann für die Mergeveröffentlichung verwendet werden.|  
|**Veröffentlichen**|Die Datenbank kann für andere Veröffentlichungstypen verwendet werden.|  
|**Abonnieren**|Die Datenbank ist eine Abonnementdatenbank.|  
|**Synchronisieren Sie mit der Sicherung**|Die Datenbank ist für eine koordinierte Sicherung aktiviert. Weitere Informationen finden Sie unter [aktivieren koordinierter Sicherungen für die Transaktionsreplikation &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).|  
  
 [  **@value=**] **"***Wert***"**  
 Gibt an, ob die angegebene Replikationsdatenbankoption aktiviert oder deaktiviert wird. *Wert* ist **Sysname**, und kann **"true"** oder **"false"**. Wenn dieser Wert ist **"false"** und *Optname* ist **Merge veröffentlichen**, Abonnements für die Veröffentlichungsdatenbank Merge werden ebenfalls gelöscht.  
  
 [  **@ignore_distributor=**] *Ignore_distributor*  
 Gibt an, ob diese gespeicherte Prozedur ausgeführt wird, ohne eine Verbindung mit dem Verteiler herzustellen. *Ignore_distributor* ist **Bit**, hat den Standardwert **0**, d. h. der Verteiler sollte verbunden und mit Ihrem neuen Status der Verlegerdatenbank aktualisiert werden. Der Wert **1** sollte nur angegeben werden, wenn der Verteiler nicht zugegriffen werden kann und **Sp_replicationdboption** wird verwendet, um die Veröffentlichung deaktivieren.  
  
 [  **@from_scripting=**] *From_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_replicationdboption** wird bei der Momentaufnahme-, Transaktions- und Mergereplikation verwendet.  
  
 Diese Prozedur erstellt oder löscht bestimmte Replikationssystemtabellen, Sicherheitskonten usw. in Abhängigkeit von den gegebenen Optionen. Legt das entsprechende in Kategoriebit der **master.sysdatabases** -Systemtabelle und erstellt die erforderlichen Systemtabellen.  
  
 Das Veröffentlichen kann nur deaktiviert werden, wenn die Veröffentlichungsdatenbank online ist. Wenn für die Veröffentlichungsdatenbank eine Datenbankmomentaufnahme vorhanden ist, muss diese vor dem Deaktivieren des Veröffentlichens gelöscht werden. Eine Datenbankmomentaufnahme ist eine schreibgeschützte Offlinekopie einer Datenbank und steht nicht in Verbindung mit einer Replikationsmomentaufnahme. Weitere Informationen finden Sie unter [Datenbankmomentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_replicationdboption**.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Löschen einer Veröffentlichung](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Deaktivieren der Veröffentlichung und Verteilung](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [Sys.sysdatabases &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
