---
title: DENY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DENY
- DENY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- security [SQL Server], denying access
- DENY statement
- permissions [SQL Server], denying
- server-level securables [SQL Server]
- inherited security settings [SQL Server]
- denying permissions [SQL Server], DENY statement
- principal security [SQL Server]
- database-level securables [SQL Server]
- denying permissions [SQL Server]
ms.assetid: c32d1e01-9ee9-4665-a516-fcfece58078e
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 189e284c23492f87c71d4bc54f0bf313f137effa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="deny-transact-sql"></a>DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Verweigert einem Prinzipal eine Berechtigung. Verhindert, dass der Prinzipal die Berechtigung über seine Gruppen- oder Rollenmitgliedschaften erbt. DENY hat vor allen Berechtigungen Vorrang, gilt jedoch nicht für Objektbesitzer oder Mitglieder der festen Serverrolle „sysadmin“.
  **Sicherheitshinweis:** Mitgliedern der festen Serverrolle „sysadmin“ und Objektbesitzern können keine Berechtigungen verweigert werden.
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for DENY  
DENY   { ALL [ PRIVILEGES ] } 
     | <permission>  [ ( column [ ,...n ] ) ] [ ,...n ]  
    [ ON [ <class> :: ] securable ] 
    TO principal [ ,...n ]   
    [ CASCADE] [ AS principal ]  
[;]

<permission> ::=  
{ see the tables below }  
  
<class> ::=  
{ see the tables below }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class> ::=  
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
 ALL  
 Mit dieser Option werden nicht alle möglichen Berechtigungen verweigert. Das Verweigern mit der ALL-Option ist gleichbedeutend mit dem Verweigern der folgenden Berechtigungen.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Datenbank handelt, schließt ALL die Berechtigungen BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE und CREATE VIEW ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine skalare Funktion handelt, schließt ALL die Berechtigungen EXECUTE und REFERENCES ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Tabellenwertfunktion handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine gespeicherte Prozedur handelt, steht ALL für EXECUTE.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Tabelle handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Sicht handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
> [!NOTE]  
>  Die Syntax DENY ALL ist veraltet. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verweigern Sie stattdessen einzelne Berechtigungen.  
  
 PRIVILEGES  
 Aus Gründen der Kompatibilität mit ISO eingeschlossen. Ändert das Verhalten von ALL nicht.  
  
 *permission*  
 Der Name einer Berechtigung. Die gültigen Zuordnungen von Berechtigungen zu sicherungsfähigen Elementen sind in den im Folgenden aufgeführten untergeordneten Themen beschrieben.  
  
 *column*  
 Gibt den Namen einer Spalte in einer Tabelle an, für die Berechtigungen verweigert werden. Die Klammern () sind erforderlich.  
  
 *class*  
 Gibt die Klasse des sicherungsfähigen Elements an, für das die Berechtigung verweigert wird. Der Bereichsqualifizierer **::** ist erforderlich.  
  
 *securable*  
 Gibt das sicherungsfähige Element an, für das die Berechtigung verweigert wird.  
  
 TO *principal*  
 Der Name eines Prinzipals. Für welche Prinzipale Berechtigungen in einem sicherungsfähigen Element verweigert werden können, hängt von dem sicherungsfähigen Element ab. Gültige Kombinationen finden Sie in den weiter unten aufgeführten Themen zu sicherungsfähigen Elementen.  
  
 CASCADE  
 Gibt an, dass die Berechtigung für den angegebenen Prinzipal und für alle anderen Prinzipale verweigert wird, denen diese Berechtigung von diesem Prinzipal erteilt wurde. Dies ist erforderlich, wenn der Prinzipal die GRANT OPTION-Berechtigung besitzt.  
  
 AS *principal*  
  Verwenden Sie die AS-Prinzipalklausel, um anzugeben, dass der Prinzipal, der die Berechtigung verweigert hat, ein anderer Prinzipal als die Person sein muss, die die Anweisung ausführt. Nehmen Sie beispielsweise an, dass der Benutzer Mary der principal_id 12 und der Benutzer Raul der principal_id 15 entspricht. Mary führt `DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;` aus. Daraufhin gibt die Tabelle „sys.database_permissions“ an, dass die „grantor_prinicpal_id“ der DENY-Anweisung „15“ (Raul) entspricht, obwohl die Anweisung tatsächlich von Benutzer 12 (Mary) ausgeführt wurde.
  
In dieser Anweisung impliziert die Verwendung von AS nicht die Fähigkeit, die Identität eines anderen Benutzers anzunehmen.  
  
## <a name="remarks"></a>Remarks  
 Die vollständige Syntax der DENY-Anweisungen ist komplex. Das Syntaxdiagramm oben wurde vereinfacht, um die Struktur hervorzuheben. Die vollständige Syntax zum Verweigern von Berechtigungen für bestimmte sicherungsfähige Elemente ist in den weiter unten aufgeführten Themen beschrieben.  
  
 Für DENY wird ein Fehler gemeldet, falls CASCADE nicht angegeben wird, wenn einem Prinzipal eine Berechtigung verweigert wird, die zusammen mit GRANT OPTION erteilt wurde.  
  
 Die gespeicherte Systemprozedur sp_helprotect gibt Informationen zu Berechtigungen für sicherungsfähige Elemente auf Datenbankebene zurück.  
  
> [!CAUTION]  
>  Eine DENY-Anweisung auf Tabellenebene hat keinen Vorrang vor einer GRANT-Anweisung auf Spaltenebene. Diese Inkonsistenz in der Berechtigungshierarchie wurde aus Gründen der Abwärtskompatibilität beibehalten. Dieses Verhalten wird in einer zukünftigen Version entfernt.  
  
> [!CAUTION]  
>  Durch das Verweigern der CONTROL-Berechtigung für eine Datenbank wird implizit die CONNECT-Berechtigung für die Datenbank verweigert. Ein Prinzipal, dem die CONTROL-Berechtigung für eine Datenbank verweigert wird, kann keine Verbindung mit dieser Datenbank herstellen.  
  
> [!CAUTION]  
>  Durch das Verweigern der CONTROL SERVER-Berechtigung wird implizit die CONNECT SQL-Berechtigung für den Server verweigert. Ein Prinzipal, dem die CONTROL SERVER-Berechtigung für einen Server verweigert wird, kann keine Verbindung mit diesem Server herstellen.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Aufrufer (oder der mit der Option AS angegebene Prinzipal) benötigt entweder die CONTROL-Berechtigung für das sicherungsfähige Element, oder eine höhere Berechtigung, die die CONTROL-Berechtigung für das sicherungsfähige Element impliziert. Wenn Sie die Option AS verwenden, muss der angegebene Prinzipal Besitzer des sicherungsfähigen Elements sein, für das eine Berechtigung verweigert wird.  
  
 Berechtigte der CONTROL SERVER-Berechtigung, wie z. B. Mitglieder der festen Serverrolle sysadmin, können jede beliebige Berechtigung für jedes beliebige sicherungsfähige Element auf dem Server verweigern. Berechtigte der CONTROL-Berechtigung für die Datenbank, wie z. B. Mitglieder der festen Datenbankrolle db_owner, können jede beliebige Berechtigung für jedes beliebige sicherungsfähige Element in der Datenbank verweigern. Berechtigte der CONTROL-Berechtigung für ein Schema können jede beliebige Berechtigung für jedes Objekt innerhalb des Schemas verweigern. Falls die AS-Klausel verwendet wird, muss der angegebene Prinzipal der Besitzer des sicherbaren Elements sein, für das Berechtigungen verweigert werden.  
  
## <a name="examples"></a>Beispiele  
 In der folgenden Tabelle sind die sicherungsfähigen Elemente und Themen aufgeführt, in denen die für ein sicherungsfähiges Element spezifische Syntax beschrieben wird.  
  
|||  
|-|-|  
|Anwendungsrolle|[DENY (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Assembly|[DENY (Assemblyberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-assembly-permissions-transact-sql.md)|  
|Asymmetrischer Schlüssel|[DENY (Berechtigungen für asymmetrische Schlüssel) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-asymmetric-key-permissions-transact-sql.md)|  
|Verfügbarkeitsgruppe|[DENY (Verfügbarkeitsgruppenberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)|  
|Zertifikat|[DENY (Zertifikatberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-certificate-permissions-transact-sql.md)|  
|Vertrag|[DENY (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Datenbank|[DENY (Datenbankberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-permissions-transact-sql.md)|  
|Datenbankweit gültige Anmeldeinformationen|[DENY (Datenbankweit gültige Anmeldeinformationen) (Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)|  
|Endpunkt|[DENY (Endpunktberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)|  
|Volltextkatalog|[DENY (Volltextberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|Volltext-Stoppliste|[DENY (Volltextberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|Funktion|[DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Anmeldename|[DENY (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)|  
|Nachrichtentyp|[DENY (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Objekt|[DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Warteschlange|[DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Remotedienstbindung|[DENY (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|-Rolle|[DENY (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Route|[DENY (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Schema|[DENY (Schemaberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)|  
|Sucheigenschaftenliste|[DENY (Berechtigungen für Sucheigenschaftenlisten) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)|  
|Server|[DENY (Serverberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)|  
|Dienst|[DENY (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Gespeicherte Prozedur|[DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Symmetrischer Schlüssel|[DENY (Berechtigungen für symmetrische Schlüssel) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)|  
|Synonym|[DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Systemobjekte|[DENY (Berechtigungen für Systemobjekte) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)|  
|Tabelle|[DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|Typ|[DENY (Typberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)|  
|Benutzer|[DENY (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|Anzeigen|[DENY (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|XML-Schemasammlung|[DENY (Berechtigungen für XML-Schemaauflistungen) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
