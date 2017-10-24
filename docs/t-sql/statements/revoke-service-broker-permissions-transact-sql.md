---
title: Widerrufen der Berechtigungen von Service Broker (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- routes [Service Broker], permissions
- Service Broker, permissions
- remote service bindings [Service Broker], permissions
- permissions [Service Broker]
- message types [Service Broker], permissions
- contracts [Service Broker], permissions
- services [Service Broker], permissions
- REVOKE statement, Service Broker
ms.assetid: 70f1d938-97e2-48a4-9bc0-8be9f2f2c36d
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cc90d37072e2e081fc358f186e3dc85f0c8c092c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-service-broker-permissions-transact-sql"></a>REVOKE (Berechtigungen von Service Broker) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Hebt Berechtigungen für einen Vertrag, Nachrichtentyp, eine Remotedienstbindung, Route oder einen Dienst von [!INCLUDE[ssSB](../../includes/sssb-md.md)] auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] ON  
    {   
       [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
        }  
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argumente  
 GRANT OPTION FOR  
 Gibt an, dass das Recht zum Erteilen des angegebenen Rechts für andere Prinzipale aufgehoben wird. Die Berechtigung selbst wird nicht widerruft.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für ein sicherbares Element von [!INCLUDE[ssSB](../../includes/sssb-md.md)] aufgehoben werden kann. Eine Liste dieser Berechtigungen finden Sie unter Hinweise weiter unten in diesem Thema.  
  
 Vertrag **::***Contract_name*  
 Gibt den Vertrag an, für den die Berechtigung aufgehoben wird. Der bereichsqualifizierer **::** ist erforderlich.  
  
 NACHRICHTENTYP **::***Message_type_name*  
 Gibt den Nachrichtentyp an, für den die Berechtigung aufgehoben wird. Der bereichsqualifizierer **::** ist erforderlich.  
  
 REMOTE SERVICE BINDING **::***Remote_binding_name*  
 Gibt die Remotedienstbindung an, für die die Berechtigung aufgehoben wird. Der bereichsqualifizierer **::** ist erforderlich.  
  
 ROUTE **::***Route_name*  
 Gibt die Route an, für die die Berechtigung aufgehoben wird. Der bereichsqualifizierer **::** ist erforderlich.  
  
 Dienst **::***Message_type_name*  
 Gibt den Dienst an, für den die Berechtigung aufgehoben wird. Der bereichsqualifizierer **::** ist erforderlich.  
  
 *database_principal*  
 Gibt den Prinzipal an, für den die Berechtigung aufgehoben wird. *Database_principal* kann eines der folgenden sein:  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle  
  
-   Anwendungsrolle  
  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen sie von diesem Prinzipal erteilt oder verweigert wurde.  
  
> [!CAUTION]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 AS *Revoking_principal*  
 Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Aufheben der Berechtigung ableitet. *Revoking_principal* kann eines der folgenden sein:  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle  
  
-   Anwendungsrolle  
  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="service-broker-contracts"></a>Service Broker-Verträge  
 Ein [!INCLUDE[ssSB](../../includes/sssb-md.md)] Vertrag ist eine Datenbankebene sicherungsfähiges Element, das von der Datenbank enthalten ist, das das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die für aufgehoben werden können ein [!INCLUDE[ssSB](../../includes/sssb-md.md)] Vertrag sind aufgeführt, in der folgenden Tabelle die allgemeineren Berechtigungen, die sie implizit enthalten.  
  
|Service Broker-Vertragsberechtigung|Impliziert durch Service Broker-Vertragsberechtigung|Impliziert durch Datenbankberechtigung|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Service Broker-Nachrichtentypen  
 Ein [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Nachrichtentyp ist ein sicherbares Element auf Datenbankebene in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und am meisten beschränkten Berechtigungen, die für einen [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Nachrichtentyp aufgehoben werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Service Broker-Nachrichtentypberechtigung|Impliziert durch Service Broker-Nachrichtentypberechtigung|Impliziert durch Datenbankberechtigung|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Service Broker-Remotedienstbindungen  
 Eine [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Remotedienstbindung ist ein sicherbares Element auf Datenbankebene in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und am meisten beschränkten Berechtigungen, die für eine [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Remotedienstbindung aufgehoben werden können, sind unten aufgeführt. Auch die allgemeineren Berechtigungen sind aufgeführt, die diese implizit enthalten.  
  
|Berechtigung für Service Broker-Remotedienstbindung|Impliziert durch Berechtigung für Service Broker-Remotedienstbindung|Impliziert durch Datenbankberechtigung|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Service Broker-Routen  
 Eine [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Route ist ein sicherbares Element auf Datenbankebene in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die für aufgehoben werden können eine [!INCLUDE[ssSB](../../includes/sssb-md.md)] Route sind aufgeführt, in der folgenden Tabelle die allgemeineren Berechtigungen, die sie implizit enthalten.  
  
|Service Broker-Routenberechtigung|Impliziert durch Service Broker-Routenberechtigung|Impliziert durch Datenbankberechtigung|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Service Broker-Dienste  
 Ein [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Dienst ist ein sicherbares Element auf Datenbankebene in der Datenbank, die das übergeordnete Element in der Berechtigungshierarchie ist. Die spezifischsten und restriktivsten Berechtigungen, die für aufgehoben werden können eine [!INCLUDE[ssSB](../../includes/sssb-md.md)] Dienst sind aufgeführt, in der folgenden Tabelle die allgemeineren Berechtigungen, die sie implizit enthalten.  
  
|Service Broker-Dienstberechtigung|Impliziert durch Service Broker-Dienstberechtigung|Impliziert durch Datenbankberechtigung|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL-Berechtigung für den Vertrag, Nachrichtentyp, die Remotedienstbindung, Route oder den Dienst von [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Berechtigungen von GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)   
 [Verweigern von Berechtigungen von Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

