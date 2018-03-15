---
title: REVOKE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REVOKE_TSQL
- REVOKE
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- REVOKE statement, Transact-SQL syntax
- removing permissions
- server-level securables [SQL Server]
- deleting permissions
- revoking permissions [SQL Server]
- REVOKE statement
- denying permissions [SQL Server], removing
- database-level securables [SQL Server]
- granting permissions [SQL Server], removing
- permissions [SQL Server], revoking
- dropping permissions
ms.assetid: 9d31d3e7-0883-45cd-bf0e-f0361bbb0956
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3f96892b5671d9616a3c809aa6b83fbcaa071b6d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-transact-sql"></a>REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt eine zuvor erteilte oder verweigerte Berechtigung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for REVOKE  
REVOKE [ GRANT OPTION FOR ]  
      {   
        [ ALL [ PRIVILEGES ] ]  
        |  
                permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      }  
      [ ON [ class :: ] securable ]   
      { TO | FROM } principal [ ,...n ]   
      [ CASCADE] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
REVOKE   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    [ FROM | TO ] principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class_type> ::=  
{  
      LOGIN  
    | DATABASE  
    | OBJECT  
    | ROLE  
    | SCHEMA  
    | USER  
}  
```  
  
## <a name="arguments"></a>Argumente  
 GRANT OPTION FOR  
 Gibt an, dass die Fähigkeit, die angegebene Berechtigung zu erteilen, aufgehoben wird. Dies ist bei Verwendung des CASCADE-Arguments erforderlich.  
  
> [!IMPORTANT]  
>  Falls der Prinzipal die angegebene Berechtigung ohne GRANT OPTION besitzt, wird die Berechtigung selbst aufgehoben.  
  
 ALL  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Mit dieser Option werden nicht alle möglichen Berechtigungen aufgehoben. Das Aufheben mit ALL entspricht dem Aufheben der folgenden Berechtigungen.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Datenbank handelt, schließt ALL die Berechtigungen BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE und CREATE VIEW ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine skalare Funktion handelt, schließt ALL die Berechtigungen EXECUTE und REFERENCES ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Tabellenwertfunktion handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine gespeicherte Prozedur handelt, steht ALL für EXECUTE.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Tabelle handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Sicht handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
> [!NOTE]  
>  Die REVOKE ALL-Syntax ist veraltet. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Widerrufen Sie stattdessen einzelne Berechtigungen.  
  
 PRIVILEGES  
 Aus Gründen der Kompatibilität mit ISO eingeschlossen. Ändert das Verhalten von ALL nicht.  
  
 *permission*  
 Der Name einer Berechtigung. Die gültigen Zuordnungen von Berechtigungen zu sicherungsfähigen Elementen werden in den Artikeln beschrieben, die unter [Für sicherungsfähige Elemente spezifische Syntax](#securable) weiter unten in diesem Thema aufgelistet werden.  
  
 *column*  
 Gibt den Namen einer Spalte in einer Tabelle an, für die Berechtigungen aufgehoben werden. Die Klammern sind erforderlich.  
  
 *class*  
 Gibt die Klasse des sicherungsfähigen Elements an, für das die Berechtigung aufgehoben wird. Der Bereichsqualifizierer **::** ist erforderlich.  
  
 *securable*  
 Gibt das sicherungsfähige Element an, für das die Berechtigung aufgehoben wird.  
  
 TO | FROM *principal*  
 Der Name eines Prinzipals. Die Prinzipale, für die Berechtigungen für ein sicherungsfähiges Element aufgehoben werden können, sind abhängig vom jeweiligen sicherungsfähigen Element unterschiedlich. Weitere Informationen zu gültigen Kombinationen finden Sie in den Themen, die unter [Für sicherungsfähige Elemente spezifische Syntax](#securable) weiter unten in diesem Artikel aufgelistet werden.  
  
 CASCADE  
 Gibt an, dass die aufgehobene Berechtigung auch für andere Prinzipale aufgehoben wird, denen sie von diesem Prinzipal erteilt wurde. Bei Verwendung des CASCADE-Arguments müssen Sie auch das GRANT OPTION FOR-Argument einschließen.  
  
> [!CAUTION]  
>  Durch ein kaskadiertes Aufheben einer Berechtigung, die mit GRANT OPTION erteilt wurde, werden sowohl GRANT als auch DENY für diese Berechtigung aufgehoben.  
  
 AS *principal*  
 Verwenden Sie die Prinzipalklausel AS, um anzugeben, dass Sie eine Berechtigung aufheben, die von einem anderen Prinzipal erteilt wurde. Nehmen Sie beispielsweise an, dass die Benutzerin Mary der principal_id 12 und der Benutzer Raul der principal_id 15 entspricht. Die Benutzer Mary und Raul erteilen dem Benutzer Steven die gleiche Berechtigung. Dann gibt die Tabelle „sys.database_permissions“ die Berechtigungen zweimal an, jedoch mit einem jeweils anderen Wert von „grantor_principal_id“. Mary könnte in diesem Fall die Klausel `AS RAUL` verwenden, um die von Raul erteilten Berechtigungen zu entfernen.
 
In dieser Anweisung impliziert die Verwendung der Anweisung AS nicht die Fähigkeit, die Identität eines anderen Benutzers anzunehmen.  
  
## <a name="remarks"></a>Remarks  
 Die vollständige Syntax der REVOKE-Anweisung ist sehr komplex. Das Syntaxdiagramm oben wurde vereinfacht, um die Struktur hervorzuheben. Die vollständige Syntax zum Aufheben von Berechtigungen für bestimmte sicherungsfähige Elemente wird in den Artikeln beschrieben, die unter [Für sicherungsfähige Elemente spezifische Syntax](#securable) weiter unten in diesem Artikel aufgelistet werden.  
  
 Die REVOKE-Anweisung kann zum Entfernen von erteilten Berechtigungen verwendet werden, und mit der DENY-Anweisung kann verhindert werden, dass einem Prinzipal eine spezifische Berechtigung durch eine GRANT-Anweisung erteilt wird.  
  
 Durch das Erteilen einer Berechtigung wird DENY oder REVOKE für diese Berechtigung aus dem angegebenen sicherungsfähigen Element entfernt. Falls dieselbe Berechtigung aus einem höheren Bereich als dem des sicherungsfähigen Elements verweigert wird, hat DENY Vorrang. Das Aufheben der erteilten Berechtigung in einem höheren Bereich hat jedoch keinen Vorrang.  
  
> [!CAUTION]  
>  Eine DENY-Anweisung auf Tabellenebene hat keinen Vorrang vor einer GRANT-Anweisung auf Spaltenebene. Diese Inkonsistenz in der Berechtigungshierarchie wurde aus Gründen der Abwärtskompatibilität beibehalten. Dieses Verhalten wird in einer zukünftigen Version entfernt.  
  
 Die gespeicherte Systemprozedur sp_helprotect gibt Informationen zu Berechtigungen für ein sicherungsfähiges Element auf Datenbankebene zurück.  
  
 Die REVOKE-Anweisung erzeugt einen Fehler, wenn CASCADE beim Aufheben einer Berechtigung für einen Prinzipal nicht angegeben ist, dem diese Berechtigung mit GRANT OPTION erteilt wurde.  
  
## <a name="permissions"></a>Berechtigungen  
 Prinzipale mit CONTROL-Berechtigung für ein sicherungsfähiges Element können die Berechtigung für dieses sicherungsfähige Element aufheben. Objektbesitzer können Berechtigungen für die Objekte aufheben, die sie besitzen.  
  
 Empfänger der CONTROL SERVER-Berechtigung, z. B. Mitglieder der festen Serverrolle sysadmin, können jede Berechtigung für ein beliebiges sicherungsfähiges Element auf dem Server aufheben. Empfänger der CONTROL SERVER-Berechtigung in einer Datenbank, z. B. Mitglieder der festen Datenbankrolle db_owner, können jede Berechtigung für ein beliebiges sicherungsfähiges Element in der Datenbank aufheben. Empfänger der CONTROL-Berechtigung in einem Schema können jede Berechtigung für jedes Objekt im Schema aufheben.  
  
##  <a name="securable"></a> Für sicherungsfähige Elemente spezifische Syntax  
 In der folgenden Tabelle sind die sicherungsfähigen Elemente und Themen aufgeführt, in denen die für ein sicherungsfähiges Element spezifische Syntax beschrieben wird.  
  
|Sicherungsfähiges Element|Thema|  
|---------------|-----------|  
|Anwendungsrolle|[REVOKE (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Assembly|[REVOKE (Assemblyberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-assembly-permissions-transact-sql.md)|  
|Asymmetrischer Schlüssel|[REVOKE (Berechtigungen für asymmetrische Schlüssel) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-asymmetric-key-permissions-transact-sql.md)|  
|Verfügbarkeitsgruppe|[REVOKE (Verfügbarkeitsgruppenberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)|  
|Zertifikat|[REVOKE (Zertifikatberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-certificate-permissions-transact-sql.md)|  
|Vertrag|[REVOKE (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Datenbank|[REVOKE (Datenbankberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-permissions-transact-sql.md)|  
|Endpunkt|[REVOKE (Endpunktberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)|  
|Datenbankweit gültige Anmeldeinformationen|[REVOKE (Datenbankweit gültige Anmeldeinformationen) (Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)|  
|Volltextkatalog|[REVOKE (Volltextberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|Volltext-Stoppliste|[REVOKE (Volltextberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|Funktion|[REVOKE (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Anmeldename|[REVOKE (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)|  
|Nachrichtentyp|[REVOKE (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Objekt|[REVOKE (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Warteschlange|[REVOKE (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Remotedienstbindung|[REVOKE (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|-Rolle|[REVOKE (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Route|[REVOKE (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Schema|[REVOKE (Schemaberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-schema-permissions-transact-sql.md)|  
|Sucheigenschaftenliste|[REVOKE (Berechtigungen für das Durchsuchen von Eigenschaftenlisten) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-search-property-list-permissions-transact-sql.md)|  
|Server|[REVOKE (Serverberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)|  
|Dienst|[REVOKE (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Gespeicherte Prozedur|[REVOKE (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Symmetrischer Schlüssel|[REVOKE (Berechtigungen für symmetrische Schlüssel) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-symmetric-key-permissions-transact-sql.md)|  
|Synonym|[REVOKE (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Systemobjekte|[REVOKE (Berechtigungen für Systemobjekte) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)|  
|Tabelle|[REVOKE (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|Typ|[REVOKE (Typberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)|  
|Benutzer|[REVOKE (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|Anzeigen|[REVOKE (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|XML-Schemasammlung|[REVOKE (Berechtigungen für XML-Schemaauflistungen) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Berechtigungshierarchie &#40;Datenbankmodul&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
