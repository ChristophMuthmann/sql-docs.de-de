---
title: GRANT-Service Broker-Berechtigungen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- granting permissions [SQL Server], Service Broker
- routes [Service Broker], permissions
- Service Broker, permissions
- GRANT statement, Service Broker
- remote service bindings [Service Broker], permissions
- message types [Service Broker], permissions
- contracts [Service Broker], permissions
ms.assetid: c5579976-97c4-4123-be0c-d0b98a9e38fb
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8fc317c36ae0cc14891be3a4f3a9c17c7a41fc3e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="grant-service-broker-permissions-transact-sql"></a>GRANT (Berechtigungen von Service Broker) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erteilt Berechtigungen für einen Vertrag, einen Nachrichtentyp, eine Remotebindung, eine Route oder einen Dienst für einen Service Broker.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GRANT permission  [ ,...n ] ON  
    {    
              [ CONTRACT :: contract_name ]   
       | [ MESSAGE TYPE :: message_type_name ]    
       | [ REMOTE SERVICE BINDING :: remote_binding_name ]    
       | [ ROUTE :: route_name ]   
       | [ SERVICE :: service_name ]      
    }  
    TO database_principal [ ,...n ]   
    [ WITH GRANT OPTION ]  
        [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumente  
 *Berechtigung*  
 Gibt eine Berechtigung an, die für ein sicherungsfähiges Service Broker-Element erteilt werden kann.  Unten aufgeführt.  
  
 Vertrag **::***Contract_name*  
 Gibt den Vertrag an, für den die Berechtigung erteilt wird. Der bereichsqualifizierer "::" ist erforderlich.  
  
 NACHRICHTENTYP **::***Message_type_name*  
 Gibt den Nachrichtentyp an, für den die Berechtigung erteilt wird. Der Bereichsqualifizierer "::" ist erforderlich.  
  
 REMOTE SERVICE BINDING **::***Remote_binding_name*  
 Gibt die Remotedienstbindung an, für die die Berechtigung erteilt wird. Der Bereichsqualifizierer "::" ist erforderlich.  
  
 ROUTE **::***Route_name*  
 Gibt die Route an, für die die Berechtigung erteilt wird. Der Bereichsqualifizierer "::" ist erforderlich.  
  
 Dienst **::***Service_name*  
 Gibt den Dienst an, für den die Berechtigung erteilt wird. Der Bereichsqualifizierer "::" ist erforderlich.  
  
 *database_principal*  
 Gibt den Prinzipal an, für den die Berechtigung erteilt wird. Einer der folgenden Typen:  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle (database role)  
  
-   Anwendungsrolle  
  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
 GRANT OPTION  
 Gibt an, dass der Prinzipal die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
 *granting_principal*  
 Gibt einen Prinzipal an, von dem der Prinzipal, der diese Abfrage ausführt, sein Recht zum Erteilen der Berechtigung ableitet. Einer der folgenden Typen:  
  
-   Datenbankbenutzer  
  
-   Datenbankrolle (database role)  
  
-   Anwendungsrolle  
  
-   Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer  
  
-   Einer Windows-Gruppe zugeordneter Datenbankbenutzer  
  
-   Einem Zertifikat zugeordneter Datenbankbenutzer  
  
-   Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer  
  
-   Keinem Serverprinzipal zugeordneter Datenbankbenutzer.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="service-broker-contracts"></a>Service Broker-Verträge  
 Ein Service Broker-Vertrag ist ein auf der Datenbankebene sicherungsfähiges Element, das in der Datenbank enthalten ist, die das übergeordnete Element in der Berechtigungshierarchie darstellt. Die spezifischsten und restriktivsten Berechtigungen, die für einen Service Broker-Vertrag erteilt werden können, sind im Folgenden aufgeführt, zusammen mit den allgemeineren Berechtigungen, die implizit enthalten sind.  
  
|Service Broker-Vertragsberechtigung|Impliziert durch Service Broker-Vertragsberechtigung|Impliziert durch Datenbankberechtigung|  
|----------------------------------------|---------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY CONTRACT|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-message-types"></a>Service Broker-Nachrichtentypen  
 Ein Service Broker-Nachrichtentyp ist ein auf der Datenbankebene sicherungsfähiges Element, das in der Datenbank enthalten ist, die das übergeordnete Element in der Berechtigungshierarchie darstellt. Die spezifischsten und restriktivsten Berechtigungen, die für einen Service Broker-Nachrichtentyp erteilt werden können, sind im Folgenden aufgeführt, zusammen mit den allgemeineren Berechtigungen, die implizit enthalten sind.  
  
|Service Broker-Nachrichtentypberechtigung|Impliziert durch Service Broker-Nachrichtentypberechtigung|Impliziert durch Datenbankberechtigung|  
|--------------------------------------------|-------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY MESSAGE TYPE|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-remote-service-bindings"></a>Service Broker-Remotedienstbindungen  
 Eine Service Broker-Remotedienstbindung ist ein auf der Datenbankebene sicherungsfähiges Element, das in der Datenbank enthalten ist, die das übergeordnete Element in der Berechtigungshierarchie darstellt. Die spezifischsten und restriktivsten Berechtigungen, die für eine Service Broker-Remotedienstbindung erteilt werden können, sind im Folgenden aufgeführt, zusammen mit den allgemeineren Berechtigungen, die implizit enthalten sind.  
  
|Berechtigung für Service Broker-Remotedienstbindung|Impliziert durch Berechtigung für Service Broker-Remotedienstbindung|Impliziert durch Datenbankberechtigung|  
|------------------------------------------------------|-----------------------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY REMOTE SERVICE BINDING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="service-broker-routes"></a>Service Broker-Routen  
 Eine Service Broker-Route ist ein auf der Datenbankebene sicherungsfähiges Element, das in der Datenbank enthalten ist, die das übergeordnete Element in der Berechtigungshierarchie darstellt. Die spezifischsten und restriktivsten Berechtigungen, die für eine Service Broker-Route erteilt werden können, sind im Folgenden aufgeführt, zusammen mit den allgemeineren Berechtigungen, die implizit enthalten sind.  
  
|Service Broker-Routenberechtigung|Impliziert durch Service Broker-Routenberechtigung|Impliziert durch Datenbankberechtigung|  
|-------------------------------------|------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROUTE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
### <a name="service-broker-services"></a>Service Broker-Dienste  
 Ein Service Broker-Dienst ist ein auf der Datenbankebene sicherungsfähiges Element, das in der Datenbank enthalten ist, die das übergeordnete Element in der Berechtigungshierarchie darstellt. Die spezifischsten und restriktivsten Berechtigungen, die für einen Service Broker-Dienst erteilt werden können, sind im Folgenden aufgeführt, zusammen mit den allgemeineren Berechtigungen, die implizit enthalten sind.  
  
|Service Broker-Dienstberechtigung|Impliziert durch Service Broker-Dienstberechtigung|Impliziert durch Datenbankberechtigung|  
|---------------------------------------|--------------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|SEND|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY SERVICE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Berechtigungen  
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) benötigt entweder die Berechtigung selbst mit GRANT OPTION oder eine höhere Berechtigung, die die erteilte Berechtigung impliziert.  
  
 Wenn Sie die Option AS verwenden, gelten die folgenden zusätzlichen Anforderungen.  
  
|AS *Granting_principal*|Zusätzliche Berechtigung erforderlich|  
|------------------------------|------------------------------------|  
|Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einem Windows-Anmeldenamen zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einer Windows-Gruppe zugeordneter Datenbankbenutzer|Mitgliedschaft in der Windows-Gruppe, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin**festen Serverrolle "".|  
|Einem Zertifikat zugeordneter Datenbankbenutzer|Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einem asymmetrischen Schlüssel zugeordneter Datenbankbenutzer|Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Einem Serverprinzipal zugeordneter Datenbankbenutzer|IMPERSONATE-Berechtigung für den Benutzer, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin** festen Serverrolle "".|  
|Datenbankrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin**festen Serverrolle "".|  
|Anwendungsrolle|ALTER-Berechtigung für die Rolle, Mitgliedschaft in der **Db_securityadmin** festen Datenbankrolle, Mitgliedschaft in der **Db_owner** feste Datenbankrolle oder die Mitgliedschaft in der **Sysadmin**festen Serverrolle "".|  
  
 Objektbesitzer können Berechtigungen für die Objekte erteilen, die sie besitzen. Prinzipale mit CONTROL-Berechtigung für ein sicherungsfähiges Element können die Berechtigung für dieses sicherungsfähige Element erteilen.  
  
 Empfänger der CONTROL SERVER-Berechtigung, z. B. Mitglieder der der **Sysadmin** feste Serverrolle, können beliebige Berechtigungen für ein beliebiges erteilen sicherungsfähige Element auf dem Server. Berechtigte der CONTROL-Berechtigung für eine Datenbank, z. B. Mitglieder der der **Db_owner** festen Datenbankrolle können beliebige Berechtigungen für ein beliebiges erteilen sicherungsfähiges Element in der Datenbank. Empfänger der CONTROL-Berechtigung für ein Schema können jede beliebige Berechtigung für jedes Objekt innerhalb des Schemas erteilen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Berechtigungen &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Prinzipale &#40;Datenbankmodul&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
