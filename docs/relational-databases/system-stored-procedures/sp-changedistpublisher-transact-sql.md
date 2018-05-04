---
title: Sp_changedistpublisher (Transact-SQL) | Microsoft Docs
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
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bd51e739e5414fe92177f54aea9a3b602e6c17d0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spchangedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften des Verteilungsverlegers. Diese gespeicherte Prozedur wird auf dem Verteiler für jede Datenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@publisher=** ] **"***Publisher***"**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [  **@property=** ] **"***Eigenschaft***"**  
 Eine Eigenschaft, die für den angegebenen Verleger geändert werden soll. *Eigenschaft* ist **Sysname** und kann einen der folgenden Werte sein.  
  
 [ **@value=** ] **'***Wert***'**  
 Der Wert für die angegebene Eigenschaft. *Wert* ist **nvarchar(255)**, hat den Standardwert NULL.  
  
 Diese Tabelle beschreibt die Eigenschaften von Verlegern und die Werte für diese Eigenschaften.  
  
|Eigenschaft|Werte|Description|  
|--------------|------------|-----------------|  
|**Aktive**|**true**|Aktiviert den Verleger|  
||**false**|Deaktiviert den Verleger|  
|**distribution_db**||Der Name der Verteilungsdatenbank.|  
|**login**||Benutzername|  
|**password**||Sicheres Kennwort für den angegebenen Anmeldenamen.|  
|**security_mode**|**1**|Verwendung der Windows-Authentifizierung für die Verbindung mit dem Verleger. *Dies kann nicht geändert werden, für einen nicht-* [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Verleger.*|  
||**0**|Verwendung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung für die Verbindung mit dem Verleger. *Dies kann nicht geändert werden, für einen nicht-* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Verleger.*|  
|**working_directory**||Das zum Speichern von Daten- und Schemadateien für die Veröffentlichung verwendete Arbeitsverzeichnis|  
|NULL (Standard)||Alle verfügbaren *Eigenschaft* -Optionen werden ausgegeben.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_changedistpublisher** wird für alle Replikationstypen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_changedistpublisher**.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [Sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
