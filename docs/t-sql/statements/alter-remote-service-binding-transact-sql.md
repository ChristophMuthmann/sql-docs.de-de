---
title: ALTER REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER REMOTE SERVICE BINDING
- ALTER_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote service bindings [Service Broker], modifying
- ALTER REMOTE SERVICE BINDING statement
- modifying remote service bindings
ms.assetid: ee620b4a-9375-4eaa-a016-69916c9e1e68
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5352750b43775b53a508b42de17d33a792a40b1b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert den einer Remotedienstbindung zugeordneten Benutzer oder ändert die Einstellung der Bindung für die anonyme Authentifizierung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER REMOTE SERVICE BINDING binding_name   
   WITH [ USER = <user_name> ] [ , ANONYMOUS = { ON | OFF } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *binding_name*  
 Der Name der zu ändernden Remotedienstbindung. Server-, Datenbank- und Schemaname können nicht angegeben werden.  
  
 MIT der Benutzer = \< *Benutzername >*  
 Gibt den Datenbankbenutzer an, der das Zertifikat besitzt, das dem Remotedienst für diese Bindung zugeordnet ist. Der öffentliche Schlüssel dieses Zertifikats wird für die Verschlüsselung und Authentifizierung von Nachrichten verwendet, die mit dem Remotedienst ausgetauscht werden.  
  
 ANONYMOUS  
 Gibt an, ob die anonyme Authentifizierung bei der Kommunikation mit dem Remotedienst verwendet wird. Ist ANONYMOUS = ON, wird die anonyme Authentifizierung verwendet und die Anmeldeinformationen des lokalen Benutzers werden nicht an den Remotedienst übertragen. Ist ANONYMOUS = OFF, werden Benutzeranmeldeinformationen übertragen. Wird diese Klausel nicht angegeben, ist die Standardeinstellung OFF.  
  
## <a name="remarks"></a>Hinweise  
 Der öffentliche Schlüssel im Zertifikat zugeordneten *User_name* dient zur Authentifizierung von Nachrichten an den Remotedienst gesendet und zur Verschlüsselung eines Sitzungsschlüssels verwendet, die dann zur Verschlüsselung der Konversation verwendet wird. Das Zertifikat für *User_name* muss das Zertifikat für einen Anmeldenamen in der Datenbank, die den Remotedienst hostet entsprechen.  
  
## <a name="permissions"></a>Berechtigungen  
 Berechtigung zum Ändern einer Remotedienstbindung erhalten standardmäßig der Besitzer der Remotedienstbindung, Mitglieder der der **Db_owner** feste Datenbankrolle und Mitglied der **Sysadmin** festen Serverrolle "".  
  
 Der Benutzer, der die ALTER REMOTE SERVICE BINDING-Anweisung ausführt, muss berechtigt sein, die Identität des in der Anweisung angegebenen Benutzers anzunehmen.  
  
 Verwenden Sie die ALTER AUTHORIZATION-Anweisung, wenn Sie AUTHORIZATION für eine Remotedienstbindung ändern möchten.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Remotedienstbindung `APBinding` geändert, sodass Nachrichten mithilfe der Zertifikate aus dem Konto `SecurityAccount` verschlüsselt werden.  
  
```  
ALTER REMOTE SERVICE BINDING APBinding  
    WITH USER = SecurityAccount ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40; Transact-SQL &#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
