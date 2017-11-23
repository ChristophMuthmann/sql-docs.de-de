---
title: Sp_certify_removable (Transact-SQL) | Microsoft Docs
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
- sp_certify_removable_TSQL
- sp_certify_removable
dev_langs: TSQL
helpviewer_keywords: sp_certify_removable
ms.assetid: ca12767f-0ae5-4652-b523-c23473f100a1
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ab84edebdbc4a8775e9ce4a50e3236b1377b3932
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spcertifyremovable-transact-sql"></a>sp_certify_removable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Überprüft, ob eine Datenbank für die Verteilung auf austauschbaren Medien ordnungsgemäß konfiguriert ist, und meldet dem Benutzer alle Probleme.  
  
> **WICHTIG!** [! UMFASSEN[SsNoteDepFutureAvoid](../../t-sql/statements/create-database-sql-server-transact-sql.md) stattdessen.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_certify_removable [ @dbname= ] 'dbname'  
     [ , [ @autofix = ] 'auto' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@dbname=**] **"***Dbname***"**  
 Gibt die Datenbank an, die überprüft werden soll. *Dbname* ist **Sysname**.  
  
 [  **@autofix=**] **"Auto"**  
 Überträgt den Besitz der Datenbank und aller Datenbankobjekte an den Systemadministrator und löscht alle vom Benutzer erstellten Datenbankbenutzer und nicht standardmäßigen Berechtigungen. *automatische* ist **nvarchar(4)**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Datenbank ordnungsgemäß konfiguriert ist, **Sp_certify_removable** führt die folgende:  
  
-   Legt den Offlinemodus für die Datenbank fest, sodass Dateien kopiert werden können.  
  
-   Aktualisiert die Statistik für alle Tabellen und meldet Besitz- oder Benutzerprobleme.  
  
-   Markiert die Datendateigruppen als schreibgeschützt, damit diese Dateien auf schreibgeschützte Medien kopiert werden können.  
  
 Der Systemadministrator muss der Besitzer der Datenbank und aller Datenbankobjekte sein. Der Systemadministrator ist ein bekannter Benutzer, die auf allen Servern vorhanden ist, die ausgeführt werden [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und erwartet werden können, vorhanden sein, wenn die Datenbank später verteilt und installiert wird.  
  
 Wenn das Ausführen **Sp_certify_removable** ohne die **Auto** Wert und gibt Informationen zu allen der folgenden Bedingungen:  
  
-   Der Systemadministrator ist nicht der Datenbankbesitzer.  
  
-   Beliebige vom Benutzer erstellte Benutzer sind bereits vorhanden.  
  
-   Der Systemadministrator besitzt nicht alle Objekte in der Datenbank.  
  
-   Es wurden von den Standardwerten abweichende Berechtigungen erteilt.  
  
 Sie können diese Bedingungen mithilfe der folgenden Möglichkeiten korrigieren:  
  
-   Verwendung [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tools und Prozeduren, und führen Sie **Sp_certify_removable** erneut aus.  
  
-   Führen Sie einfach **Sp_certify_removable** mit der **Auto** Wert.  
  
 Beachten Sie, dass diese gespeicherte Prozedur nur Benutzer und Benutzerberechtigungen überprüft. Sie können der Datenbank Gruppen hinzufügen und diesen Berechtigungen erteilen. Weitere Informationen finden Sie unter [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Führen Sie Berechtigungen werden nur von Mitgliedern der der **Sysadmin** festen Serverrolle "".  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird überprüft, ob die `inventory`-Datenbank für das Entfernen vorbereitet ist.  
  
```  
EXEC sp_certify_removable inventory, AUTO;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Sp_create_removable &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-create-removable-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Sp_dbremove &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbremove-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
