---
title: SETUSER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SETUSER_TSQL
- SETUSER
dev_langs:
- TSQL
helpviewer_keywords:
- delegation [SQL Server]
- impersonation [SQL Server]
- SETUSER statement
- user impersonation [SQL Server]
ms.assetid: 7acfac5c-9ad6-4226-b874-7add36c4ea43
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ab9805dda5f5b2b4199cb40ef3c28af1d5b4379f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="setuser-transact-sql"></a>SETUSER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ermöglicht einem Mitglied der **Sysadmin** feste Serverrolle oder den Besitzer einer Datenbank, die Identität eines anderen Benutzers anzunehmen.  
  
> [!IMPORTANT]  
>  SETUSER ist nur aus Gründen der Abwärtskompatibilität enthalten. SETUSER wird in einer künftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise nicht mehr unterstützt. Wir empfehlen die Verwendung [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Benutzername* **"**  
 Dies ist der Name eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- oder Windows-Benutzers in der aktuellen Datenbank, dessen Identität angenommen werden soll. Wenn *Benutzername* nicht angegeben ist, wird die ursprüngliche Identität des vom Systemadministrator oder Datenbankbesitzer beim Identitätswechsel des Benutzers zurückgesetzt.  
  
 WITH NORESET  
 Gibt an, dass bei nachfolgenden SETUSER-Anweisungen (ohne Angabe *Benutzername*) sollten nicht die Identität des Benutzers an den Systemadministrator oder Datenbankbesitzer zurückgesetzt.  
  
## <a name="remarks"></a>Hinweise  
 SETUSER kann verwendet werden, von einem Mitglied der **Sysadmin** feste Serverrolle oder den Besitzer einer Datenbank, die Identität eines anderen Benutzers So testen Sie die Berechtigungen dieses Benutzers zu verwenden. Mitgliedschaft in der festen Datenbankrolle "Db_owner" ist nicht ausreichend.  
  
 Verwenden Sie SETUSER nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer. SETUSER wird nicht für Windows-Benutzer unterstützt. Wenn Sie mit SETUSER die Identität eines anderen Benutzers angenommen haben, gehören alle Objekte, die Sie unter seiner Identität erstellen, diesem Benutzer. Z. B., ob der Datenbankbesitzer die Identität des Benutzers annimmt **Margaret** und erstellt eine Tabelle mit dem Namen **Aufträge**, **Aufträge** Tabelle ist im Besitz **Margaret** , nicht an den Systemadministrator.  
  
 SETUSER bleibt wirksam, bis eine andere SETUSER-Anweisung ausgeführt oder die aktuelle Datenbank mit der USE-Anweisung gewechselt wird.  
  
> [!NOTE]  
>  Falls SETUSER WITH NORESET verwendet wird, muss der Datenbankbesitzer bzw. der Systemadministrator sich ab- und wieder anmelden, um seine ursprünglichen Berechtigungen wiederherzustellen.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Sysadmin** festen Serverrolle oder der Besitzer der Datenbank. Mitgliedschaft in der **Db_owner** festen Datenbankrolle "" ist nicht ausreichend  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie der Datenbankbesitzer die Identität eines anderen Benutzers annehmen kann. Die Benutzerin `mary` hat eine Tabelle namens `computer_types` erstellt. Mithilfe von SETUSER nimmt der Datenbankbesitzer die Identität von `mary` an, um dem Benutzer `joe` den Zugriff auf die `computer_types`-Tabelle zu erteilen. Anschließend nimmt der Benutzer wieder seine eigene Identität an.  
  
```  
SETUSER 'mary';  
GO  
GRANT SELECT ON computer_types TO joe;  
GO  
--To revert to the original user  
SETUSER;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  

