---
title: SETUSER (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a511e0337201c9b4501b5274fa8270fbebf7da50
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="setuser-transact-sql"></a>SETUSER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ermöglicht einem Mitglied der festen Serverrolle **sysadmin** oder dem Besitzer einer Datenbank die Identität eines anderen Benutzers anzunehmen.  
  
> [!IMPORTANT]  
>  SETUSER ist nur aus Gründen der Abwärtskompatibilität enthalten. SETUSER wird in einer künftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise nicht mehr unterstützt. Es empfiehlt sich, stattdessen [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) zu verwenden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
## <a name="arguments"></a>Argumente  
 **'** *username* **'**  
 Dies ist der Name eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]- oder Windows-Benutzers in der aktuellen Datenbank, dessen Identität angenommen werden soll. Wird *username* nicht angegeben, so wird die ursprüngliche Identität des Systemadministrators oder des Datenbankbesitzers, der eine fremde Identität angenommen hat, wiederhergestellt.  
  
 WITH NORESET  
 Gibt an, dass bei nachfolgenden SETUSER-Anweisungen (ohne Angabe von *username*) die ursprüngliche Identität des Systemadministrators bzw. Datenbankbesitzers nicht wiederhergestellt werden soll.  
  
## <a name="remarks"></a>Remarks  
 SETUSER kann von einem Mitglied der festen Serverrolle **sysadmin** oder dem Besitzer einer Datenbank verwendet werden, um die Identität eines anderen Benutzers zum Testen der Berechtigungen dieses Benutzers anzunehmen. Die Mitgliedschaft in der festen Datenbankrolle db_owner reicht nicht aus.  
  
 Verwenden Sie SETUSER nur für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer. SETUSER wird nicht für Windows-Benutzer unterstützt. Wenn Sie mit SETUSER die Identität eines anderen Benutzers angenommen haben, gehören alle Objekte, die Sie unter seiner Identität erstellen, diesem Benutzer. Wenn der Datenbankbesitzer beispielsweise die Identität der Benutzerin **Margaret** annimmt und eine Tabelle namens **orders** erstellt, gehört diese **orders**-Tabelle der Benutzerin **Margaret** und nicht dem Systemadministrator.  
  
 SETUSER bleibt wirksam, bis eine andere SETUSER-Anweisung ausgeführt oder die aktuelle Datenbank mit der USE-Anweisung gewechselt wird.  
  
> [!NOTE]  
>  Falls SETUSER WITH NORESET verwendet wird, muss der Datenbankbesitzer bzw. der Systemadministrator sich ab- und wieder anmelden, um seine ursprünglichen Berechtigungen wiederherzustellen.  
  
## <a name="permissions"></a>Berechtigungen  
 Setzt die Mitgliedschaft in der festen Serverrolle **sysadmin** oder den Besitz der Datenbank voraus. Die Mitgliedschaft in der festen Datenbankrolle **db_owner** reicht nicht aus.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  
