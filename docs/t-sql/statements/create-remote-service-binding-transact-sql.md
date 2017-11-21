---
title: Erstellen der REMOTEDIENSTBINDUNG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- CREATE REMOTE SERVICE BINDING
- SERVICE_BINDING_TSQL
- CREATE REMOTE SERVICE
- REMOTE_TSQL
- CREATE_REMOTE_SERVICE_BINDING_TSQL
- CREATE_REMOTE_SERVICE_TSQL
- BINDING
- SERVICE BINDING
- BINDING_TSQL
- CREATE_REMOTE_TSQL
- REMOTE_SERVICE_TSQL
- CREATE REMOTE
- REMOTE SERVICE
- REMOTE_SERVICE_BINDING_TSQL
- REMOTE
- REMOTE SERVICE BINDING
dev_langs:
- TSQL
helpviewer_keywords:
- binding remote service [Service Broker]
- dialog security [Service Broker]
- end-to-end security [Service Broker]
- security [Service Broker], remote service bindings
- CREATE REMOTE SERVICE BINDING statement
- conversation security [Service Broker]
- remote service bindings [Service Broker], creating
ms.assetid: 4165c404-4d50-4063-9a6e-6e267d309376
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4083cb617d76084719450a6abc49fd76345cc7a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-remote-service-binding-transact-sql"></a>CREATE REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Bindung, mit der die Sicherheitsanmeldeinformationen definiert werden, mit denen eine Konversation mit einem Remotedienst initiiert werden soll.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE REMOTE SERVICE BINDING binding_name   
   [ AUTHORIZATION owner_name ]   
   TO SERVICE 'service_name'   
   WITH  USER = user_name [ , ANONYMOUS = { ON | OFF } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *binding_name*  
 Der Name der zu erstellenden Remotedienstbindung. Server-, Datenbank- und Schemaname können nicht angegeben werden. Die *Binding_name* muss ein gültiger **Sysname**.  
  
 Autorisierung *Owner_name*  
 Legt den Besitzer der Bindung auf den angegebenen Datenbankbenutzer oder die angegebene Datenbankrolle fest. Wenn der aktuelle Benutzer ist **Dbo** oder **sa**, *Owner_name* kann der Name eines beliebigen gültigen Benutzers oder einer Rolle sein. Andernfalls *Owner_name* kann den Namen des aktuellen Benutzers, den Namen eines Benutzers an, die der aktuelle Benutzer IMPERSONATE-Berechtigungen für verfügt oder der Name einer Rolle, zu der der aktuelle Benutzer gehört.  
  
 Dienst '*Service_name*"  
 Gibt den Remotedienst an, der an den in der WITH USER-Klausel identifizierten Benutzer gebunden werden soll.  
  
 Benutzer = *User_name*  
 Gibt den Datenbankprinzipal an, der das Zertifikat besitzt, das dem von der TO SERVICE-Klausel identifizierten Remotedienst zugeordnet wird. Dieses Zertifikat wird für die Verschlüsselung und Authentifizierung von Nachrichten verwendet, die mit dem Remotedienst ausgetauscht werden.  
  
 ANONYMOUS  
 Gibt an, ob die anonyme Authentifizierung bei der Kommunikation mit dem Remotedienst verwendet wird. Wenn ANONYMOUS = ON, anonyme Authentifizierung verwendet und in der Remotedatenbank erfolgen als Mitglied der **öffentlichen** festen Datenbankrolle "". Wenn ANONYMOUS = OFF angegeben ist, finden Vorgänge in der Remotedatenbank als bestimmte Benutzer dieser Datenbank statt. Wird diese Klausel nicht angegeben, ist die Standardeinstellung OFF.  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] verwendet eine Remotedienstbindung, um nach dem für eine neue Konversation zu verwendenden Zertifikat zu suchen. Der öffentliche Schlüssel im Zertifikat zugeordneten *User_name* dient zur Authentifizierung von Nachrichten an den Remotedienst gesendet und zur Verschlüsselung eines Sitzungsschlüssels verwendet, die dann zur Verschlüsselung der Konversation verwendet wird. Das Zertifikat für *User_name* muss das Zertifikat für einen Benutzer in der Datenbank, die den Remotedienst hostet entsprechen.  
  
 Eine Remotedienstbindung wird nur zum Initiieren von Diensten benötigt, die mit Zieldiensten außerhalb der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz kommunizieren. Eine Datenbank, die als Host für einen initiierenden Dienst dient, muss Remotedienstbindungen für alle Zieldienste außerhalb der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz enthalten. Eine Datenbank, die als Host für einen Zieldienst dient, muss keine Remotedienstbindungen für die initiierenden Dienste enthalten, die mit dem Zieldienst kommunizieren. Wenn sich der Initiator- und der Zieldienst in der gleichen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befinden, ist keine Dienstbindung erforderlich. Jedoch, wenn eine Remotedienstbindung vorhanden ist, die *Service_name* angegebene für TO SERVICE dem Namen des lokalen Diensts entspricht [!INCLUDE[ssSB](../../includes/sssb-md.md)] die Bindung.  
  
 Wenn ANONYMOUS = ON, der initiierende Dienst eine Verbindung mit den Zieldienst als Mitglied der **öffentlichen** festen Datenbankrolle "". Standardmäßig haben Mitglieder dieser Rolle keine Berechtigung, eine Verbindung mit einer Datenbank herzustellen. Um eine Nachricht erfolgreich gesendet werden soll, muss die Zieldatenbank gewähren die **öffentlichen** Rolle CONNECT-Berechtigung für die Datenbank und die SEND-Berechtigung für den Zieldienst.  
  
 Besitzt ein Benutzer mehrere Zertifikate, wählt [!INCLUDE[ssSB](../../includes/sssb-md.md)] das Zertifikat mit dem aktuellsten Ablaufzeitpunkt aus den derzeit gültigen und als AVAILABLE FOR BEGIN_DIALOG gekennzeichneten Zertifikaten aus.  
  
## <a name="permissions"></a>Berechtigungen  
 Berechtigungen zum Erstellen einer Remotedienstbindung dienstbindung Standardwert für den Benutzer, die mit dem Namen in der USER-Klausel, Mitglied der **Db_owner** festen Datenbankrolle "", die Mitglieder der der **Db_ddladmin** feste Datenbankrolle und Elemente von der **Sysadmin** festen Serverrolle "".  
  
 Der Benutzer, der die CREATE REMOTE SERVICE BINDING-Anweisung ausführt, muss berechtigt sein, die Identität des in der Anweisung angegebenen Prinzipals anzunehmen.  
  
 Eine Remotedienstbindung ist möglicherweise kein temporäres Objekt. Remote Service Binding Namen ab  **#**  zulässig sind, sind jedoch dauerhafte Objekte.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-remote-service-binding"></a>A. Erstellen einer Remotedienstbindung  
 Im folgenden Beispiel wird eine Bindung für den Dienst `//Adventure-Works.com/services/AccountsPayable` erstellt. [!INCLUDE[ssSB](../../includes/sssb-md.md)] führt mit dem Zertifikat, das sich im Besitz des `APUser`-Datenbankprinzipals befindet, eine Authentifizierung gegenüber dem Remotedienst durch und tauscht den Verschlüsselungsschlüssel für die Sitzung mit dem Remotedienst aus.  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser ;  
```  
  
### <a name="b-creating-a-remote-service-binding-using-anonymous-authentication"></a>B. Erstellen einer Remotedienstbindung mit anonymer Authentifizierung  
 Im folgenden Beispiel wird eine Bindung für den Dienst `//Adventure-Works.com/services/AccountsPayable` erstellt. [!INCLUDE[ssSB](../../includes/sssb-md.md)] tauscht mit dem Zertifikat, das sich im Besitz des `APUser`-Datenbankprinzipals befindet, den Verschlüsselungsschlüssel für die Sitzung mit dem Remotedienst aus. Es findet keine Authentifizierung von Service Broker beim Remotedienst statt. In der Datenbank, die den Remotedienst hostet, Nachrichten übermittelt werden, als die **Gast** Benutzer.  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser, ANONYMOUS=ON ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER REMOTE SERVICE BINDING &#40; Transact-SQL &#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40; Transact-SQL &#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

