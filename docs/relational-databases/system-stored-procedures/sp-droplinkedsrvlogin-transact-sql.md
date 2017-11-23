---
title: Sp_droplinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs: TSQL
helpviewer_keywords: sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78ac85a6aff22b4c925a4635ab57805fab0a83c3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spdroplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt eine vorhandene Zuordnung zwischen einem Anmeldenamen auf dem lokalen Server, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, und einem Anmeldenamen auf dem Verbindungsserver.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@rmtsrvname =** ] **"***Rmtsrvname***"**  
 Der Name eines Verbindungsservers, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -anmeldenamenzuordnung gilt. *Rmtsrvname* ist **Sysname**, hat keinen Standardwert. *Rmtsrvname* muss bereits vorhanden sein.  
  
 [  **@locallogin =** ] **"***Locallogin***"**  
 Ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung auf dem lokalen Server, die eine Zuordnung zum Verbindungsserver hat *Rmtsrvname*. *Locallogin* ist **Sysname**, hat keinen Standardwert. Eine Zuordnung für *Locallogin* auf *Rmtsrvname* muss bereits vorhanden sein. Wenn der Wert NULL ist, erstellt die standardzuordnung von **Sp_addlinkedserver**, die alle Anmeldenamen auf dem lokalen Server Anmeldenamen auf dem Verbindungsserver zuordnet, gelöscht.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wenn die vorhandene Zuordnung für einen Anmeldenamen gelöscht wird, der lokale Server verwendet die standardzuordnung erstellt, indem **Sp_addlinkedserver** beim Herstellen einer Verbindung mit dem Verbindungsserver für diesen Anmeldenamen. Um die standardzuordnung zu ändern, verwenden **Sp_addlinkedsrvlogin**.  
  
 Wenn die standardzuordnung auch gelöscht wird, nur Anmeldungen, die explizit eine anmeldenamenzuordnung mit dem Verbindungsserver mithilfe von Erhalt haben **Sp_addlinkedsrvlogin**, können Zugriff auf den Verbindungsserver.  
  
 **Sp_droplinkedsrvlogin** kann nicht innerhalb einer benutzerdefinierten Transaktion ausgeführt werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY LOGIN-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-removing-the-login-mapping-for-an-existing-user"></a>A. Entfernen der Anmeldenamenzuordnung für einen vorhandenen Benutzer  
 Im folgenden Beispiel wird die Zuordnung für den Anmeldenamen `Mary` vom lokalen Server zum Verbindungsserver `Accounts` entfernt. Daher verwendet der Anmeldename `Mary` die standardmäßige Anmeldenamenzuordnung.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### <a name="b-removing-the-default-login-mapping"></a>B. Entfernen der Standardanmeldenamenzuordnung  
 Im folgenden Beispiel wird die standardmäßige Anmeldenamenzuordnung entfernt, die durch das Ausführen von `sp_addlinkedserver` auf dem Verbindungsserver `Accounts` erstellt wurde.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Sp_addlinkedsrvlogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
