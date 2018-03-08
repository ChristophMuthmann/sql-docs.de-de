---
title: Sp_changereplicationserverpasswords (Transact-SQL) | Microsoft Docs
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
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords: sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fcd1cbfd5532703196e47d06f920ef7cfa81f019
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spchangereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Kennwörter für die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von Replikations-Agents auf Servern in einer Replikationstopologie Herstellen einer Verbindung verwendete Anmeldename. Normalerweise müssten Sie das Kennwort für jeden einzelnen Agent ändern, der auf dem Server ausgeführt wird, und zwar selbst dann, wenn alle Agents den gleichen Anmeldenamen oder das gleiche Konto verwenden. Diese gespeicherte Prozedur ermöglicht Ihnen die Änderung des Kennworts für alle Instanzen eines gegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamens oder Windows-Kontos, der bzw. das von allen auf einem Server ausgeführten Replikations-Agents verwendet wird. Die gespeicherte Prozedur wird auf jedem Server in der Replikationstopologie der master-Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@login_type**  =] *Login_type*  
 Der Authentifizierungstyp für die angegebenen Anmeldeinformationen. *LOGIN_TYPE* ist **"tinyint"**, hat keinen Standardwert.  
  
 **1** = integrierte Windows-Authentifizierung  
  
 **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung  
  
 [  **@login**  =] **"***Anmeldung***"**  
 Der Name des Windows-Kontos oder der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung, das bzw. die geändert wird. *Anmeldung* ist **nvarchar(257)**, hat keinen Standardwert  
  
 [  **@password**  =] **"***Kennwort***"**  
 Das neue Kennwort gespeichert werden für den angegebenen *Anmeldung*. *Kennwort* ist **Sysname**, hat keinen Standardwert.  
  
> [!NOTE]  
>  Nachdem Sie ein Replikationskennwort geändert haben, müssen Sie jeden Agent, der dieses Kennwort verwendet, beenden und neu starten, damit die Änderung für diesen Agent in Kraft tritt.  
  
 [  **@server**  =] **"***Server***"**  
 Die Serververbindung, für die das gespeicherte Kennwort geändert wird. *Server* ist **Sysname**, und kann einen der folgenden Werte:  
  
|Wert|Description|  
|-----------|-----------------|  
|**Verteiler**|Alle Agentverbindungen zum Verteiler|  
|**publisher**|Alle Agentverbindungen zum Verleger|  
|**subscriber**|Alle Agentverbindungen zum Abonnenten|  
|**%**(Standard)|Alle Agentverbindungen zu allen Servern in einer Replikationstopologie|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changereplicationserverpasswords** wird für alle Replikationstypen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_changereplicationserverpasswords**.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern von Replikationssicherheitseinstellungen](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
