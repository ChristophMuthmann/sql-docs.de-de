---
title: Sp_vupgrade_mergeobjects (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_vupgrade_mergeobjects
- sp_vupgrade_mergeobjects_TSQL
helpviewer_keywords:
- sp_vupgrade_mergeobjects
ms.assetid: 73257c2e-cc4c-48e7-9d66-7ef045bdd4f5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 83c761ec8e22321e1d46a3b9aacaf5c619c45599
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spvupgrademergeobjects-transact-sql"></a>sp_vupgrade_mergeobjects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Generiert die artikelspezifischen Trigger, die gespeicherten Prozeduren und Sichten erneut, die zum Nachverfolgen und Anwenden von Datenänderungen für die Mergereplikation verwendet werden. Führen Sie diese Prozedur in den folgenden Situationen aus:  
  
-   Wenn ein Objekt, das für die Replikation erforderlich ist, versehentlich gelöscht wird.  
  
-   Wenn Sie ein Update (beispielsweise ein Hotfix) anwenden, für das Änderungen an einem oder mehreren Replikationsobjekten erforderlich sind. Führen Sie die Prozedur für jeden Knoten aus, nachdem Sie das Update angewendet haben.  
  
 Für das Ausführen dieser gespeicherten Prozedur ist keine erneute Initialisierung der Abonnements erforderlich. Diese Prozedur ist nicht erforderlich, wenn Sie ein Service Pack installieren oder auf eine neue Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisieren.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_vupgrade_mergeobjects [ [@login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @security_mode = ] security_mode ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@login=**] **"***Anmeldung***"**  
 Wird die systemadministratoranmeldung zu verwenden, wenn neue Systemobjekte in der Verteilungsdatenbank zu erstellen. *login* ist vom Datentyp **sysname**und hat den Standardwert NULL. Dieser Parameter ist nicht erforderlich, wenn *Security_mode* festgelegt ist, um **1**, d. h. auf Windows-Authentifizierung.  
  
 [  **@password=**] **"***Kennwort***"**  
 Gibt das Kennwort des Systemadministrators an, das verwendet werden soll, wenn neue Systemobjekte in der Verteilungsdatenbank erstellt werden. *Kennwort* ist **Sysname**, hat den Standardwert **''** (leere Zeichenfolge). Dieser Parameter ist nicht erforderlich, wenn *Security_mode* festgelegt ist, um **1**, d. h. auf Windows-Authentifizierung.  
  
 [  **@security_mode=**] **"***Security_mode***"**  
 Ist der Anmeldungssicherheitsmodus an verwenden, wenn neue Systemobjekte in der Verteilungsdatenbank zu erstellen. *Security_mode* ist **Bit** hat den Standardwert des **1**. Wenn **0**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwendet. Wenn **1**, Windows-Authentifizierung verwendet werden. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_vupgrade_mergeobjects** wird nur für die Mergereplikation verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Replikationsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Aktualisieren von replizierten Datenbanken](../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
