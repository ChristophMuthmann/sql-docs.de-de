---
title: Sp_xp_cmdshell_proxy_account (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_xp_cmdshell_proxy_account
- sp_xp_cmdshell_proxy_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xp_cmdshell_proxy_account
- xp_cmdshell
ms.assetid: f807c373-7fbc-4108-a2bd-73b48a236003
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3abbb6f6ac82cfba212f168fd4697f8c20c7f9d1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spxpcmdshellproxyaccount-transact-sql"></a>sp_xp_cmdshell_proxy_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt Proxyanmeldeinformationen für **xp_cmdshell**.  
  
> [!NOTE]  
>  **Xp_cmdshell** ist standardmäßig deaktiviert. So aktivieren Sie **Xp_cmdshell**, finden Sie unter [Xp_cmdshell Serverkonfigurationsoption](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_xp_cmdshell_proxy_account [ NULL | { 'account_name' , 'password' } ]  
```  
  
## <a name="arguments"></a>Argumente  
 NULL  
 Gibt an, dass die Proxyanmeldeinformationen gelöscht werden sollen.  
  
 *account_name*  
 Gibt einen Windows-Anmeldenamen an, der als Proxy verwendet wird.  
  
 *password*  
 Gibt das Kennwort des Windows-Kontos an.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Die Proxyanmeldeinformationen besitzen den Namen **##xp_cmdshell_proxy_account##**.  
  
 Bei Ausführung mit der NULL-Option werden die Proxyanmeldeinformationen von **sp_xp_cmdshell_proxy_account** gelöscht.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-the-proxy-credential"></a>A. Erstellen der Proxyanmeldeinformationen  
 Im folgenden Beispiel wird das Erstellen von Proxyanmeldeinformationen für das Windows-Konto `ADVWKS\Max04` mit dem Kennwort `ds35efg##65`gezeigt.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'ADVWKS\Max04', 'ds35efg##65';  
GO  
```  
  
### <a name="b-dropping-the-proxy-credential"></a>B. Löschen der Proxyanmeldeinformationen  
 Im folgenden Beispiel werden die Proxyanmeldeinformationen aus dem Anmeldeinformationenspeicher entfernt.  
  
```  
EXEC sp_xp_cmdshell_proxy_account NULL;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Xp_cmdshell &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Sicherheitsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
