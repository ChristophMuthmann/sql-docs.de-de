---
title: Sp_helpdistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords: sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e01aca1558894f52f575aba642cd4079c22f21f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Eigenschaften der Verleger zurück, die einen Verteiler verwenden. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publisher=** ] **"***Publisher***"**  
 Der Verleger, für den Eigenschaften zurückgegeben werden. *Publisher* ist **Sysname**, hat den Standardwert  **%** .  
  
 [  **@check_user=** ] *Check_user*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Name des Verlegers.|  
|**distribution_db**|**sysname**|Verteilungsdatenbank für den angegebenen Verleger.|  
|**security_mode**|**int**|Sicherheitsmodus, der von Replikations-Agents für die Verbindung mit dem Verleger für Abonnements mit verzögertem Update über eine Warteschlange oder für die Verbindung mit einem Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger verwendet wird.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung<br /><br /> **1** = Windows-Authentifizierung|  
|**Anmeldung**|**sysname**|Anmeldename, der von Replikations-Agents für die Verbindung mit dem Verleger für Abonnements mit verzögertem Update über eine Warteschlange oder für die Verbindung mit einem Nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger verwendet wird.|  
|**Kennwort**|**nvarchar(524)**|Zurückgegebenes Kennwort (in einfacher verschlüsselter Form). Das Kennwort ist NULL außer für Benutzer **Sysadmin**.|  
|**aktive**|**bit**|Gibt an, ob ein Remoteverleger den lokalen Server als Verteiler verwendet:<br /><br /> **0** = Nein<br /><br /> **1** = Ja|  
|**working_directory**|**nvarchar(255)**|Name des Arbeitsverzeichnisses.|  
|**Vertrauenswürdige**|**bit**|Gibt an, ob das Kennwort beim Herstellen der Verbindung des Verlegers mit dem Verteiler erforderlich ist. Für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen sollte immer zurückgegeben **0**, was bedeutet, dass das Kennwort erforderlich ist.|  
|**thirdparty_flag**|**bit**|Gibt an, ob die Veröffentlichung durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder eine Anwendung eines Drittanbieters aktiviert wurde:<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle- oder Oracle Gateway-Verleger.<br /><br /> **1** = Verleger wurde integriert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe einer Anwendung eines Drittanbieters.|  
|**publisher_type**|**sysname**|Typ des Verlegers; kann einer der folgenden sein:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE-GATEWAY**|  
|**publisher_data_source**|**nvarchar(4000)**|Name der OLE DB-Datenquelle auf dem Verleger.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_helpdistpublisher** wird für alle Replikationstypen verwendet.  
  
 **Sp_helpdistpublisher** die verlegeranmeldung wird nicht angezeigt oder Kennwort im Resultset legen Sie für nicht-**Sysadmin** Anmeldungen.  
  
## <a name="permissions"></a>Berechtigungen  
 Mitglieder der **Sysadmin** festen Serverrolle ausgeführt **Sp_helpdistpublisher** für jeden Verleger, auf den lokalen Server als Verteiler verwenden. Mitglieder der **Db_owner** festen Datenbankrolle "" oder die **Replmonitor** Rolle in einer Verteilungsdatenbank ausgeführt **Sp_helpdistpublisher** für jeden Verleger verwenden, Distribution-Datenbank. Benutzer in der veröffentlichungszugriffsliste für eine Veröffentlichung auf der angegebenen Liste *Publisher* führen möglicherweise **Sp_helpdistpublisher**. Wenn *Publisher* nicht angegeben ist, werden Informationen zu allen Verlegern zurückgegeben, dass der Benutzer Zugriffsberechtigungen besitzt.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [Sp_dropdistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
