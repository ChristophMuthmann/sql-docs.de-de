---
title: Sp_changemergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_changemergesubscription_TSQL
- sp_changemergesubscription
helpviewer_keywords: sp_changemergesubscription
ms.assetid: fd820f35-c189-4e2d-884d-b60c1c469f58
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3fef5efe16fbc6a3684e077ef8dfca38b839753
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spchangemergesubscription-transact-sql"></a>sp_changemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert ausgewählte Eigenschaften eines Mergepushabonnements. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
> [!IMPORTANT]  
>  Beim Konfigurieren eines Verlegers mit einem Remoteverteiler werden die Werte, die für alle Parameter, einschließlich *job_login* und *job_password*, bereitgestellt werden, als Nur-Text an den Verteiler gesendet. Sie sollten die Verbindung zwischen dem Verleger und dem zugehörigen Remoteverteiler verschlüsseln, bevor Sie diese gespeicherte Prozedur ausführen. Weitere Informationen finden Sie unter [Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changemergesubscription [ [ @publication= ] 'publication' ]  
    [ , [ @subscriber= ] 'subscriber'  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publication=**] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, die geändert werden soll. *Veröffentlichung* ist **Sysname**, hat den Standardwert NULL. Die Veröffentlichung muss bereits vorhanden sein und den Regeln für Bezeichner entsprechen.  
  
 [  **@subscriber=**] **"***Abonnenten***"**  
 Der Name des Abonnenten. *Abonnenten* ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@subscriber_db=**] **"***Subscriber_db***"**  
 Ist der Name der Abonnementdatenbank. *Subscriber_db*ist **Sysname**, hat den Standardwert NULL.  
  
 [  **@property=**] **"***Eigenschaft***"**  
 Ist die Eigenschaft, die für die angegebene Veröffentlichung geändert. *Eigenschaft* ist **Sysname**, und kann einen der Werte in der Tabelle.  
  
 [  **@value=**] **"***Wert***"**  
 Der neue Wert für den angegebenen *Eigenschaft*. *Wert* ist **nvarchar(255)**, und kann einen der Werte in der Tabelle.  
  
|Eigenschaft|Wert|Description|  
|--------------|-----------|-----------------|  
|**Beschreibung**||Die Beschreibung dieses Mergeabonnements.|  
|**Priorität**||Die Abonnementpriorität. Die Priorität wird vom Standardresolver verwendet, um einen Gewinner zu ermitteln, wenn Konflikte erkannt werden.|  
|**merge_job_login**||Anmeldename für das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**merge_job_password**||Kennwort für das Windows-Konto, unter dem der Agent ausgeführt wird.|  
|**publisher_security_mode**|**1**|Verwendung der Windows-Authentifizierung für die Verbindung mit dem Verleger.|  
||**0**|Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung für die Verbindung mit dem Verleger.|  
|**publisher_login**||Anmeldename auf dem Verleger.|  
|**publisher_password**||Sicheres Kennwort für den angegebenen Anmeldenamen auf dem Verleger.|  
|**subscriber_security_mode**|**1**|Verwendung der Windows-Authentifizierung für die Verbindung mit dem Abonnenten.|  
||**0**|Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung für die Verbindung mit dem Abonnenten.|  
|**subscriber_login**||Anmeldename auf dem Abonnenten.|  
|**subscriber_password**||Sicheres Kennwort für den angegebenen Anmeldenamen auf dem Abonnenten.|  
|**sync_type-Typ**|**Automatisch**|Das Schema und die Ausgangsdaten für veröffentlichte Tabellen werden zuerst an den Abonnenten übertragen.|  
||**keine**|Der Abonnent verfügt bereits über das Schema und die Ausgangsdaten für veröffentlichte Tabellen; Systemtabellen und Daten werden immer übertragen.|  
|**use_interactive_resolver**|**true**|Ermöglicht das interaktive Lösen von Konflikten für alle Artikel, die eine interaktive Auflösung zulassen.|  
||**false**|Konflikte werden automatisch mithilfe eines Standardkonfliktlösers oder eines benutzerdefinierten Konfliktlösers gelöst.|  
|NULL (Standard)|NULL (Standard)||  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changemergesubscription** wird bei der Mergereplikation verwendet.  
  
 Nach dem Ändern des Anmeldenamens oder Kennworts eines Agents müssen Sie den Agent beenden und neu starten, damit die Änderungen in Kraft treten.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der der **Sysadmin** feste Serverrolle oder **Db_owner** feste Datenbankrolle können ausführen **Sp_changemergesubscription**.  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_addmergesubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [Sp_dropmergesubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Sp_helpmergesubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
