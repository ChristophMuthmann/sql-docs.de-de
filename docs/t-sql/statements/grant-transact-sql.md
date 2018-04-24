---
title: GRANT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/12/2017
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
- GRANT_TSQL
- GRANT
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], GRANT statement
- schema-level securables [SQL Server]
- GRANT statement
- cross-database permissions
- GRANT statement, about GRANT statement
- server-level securables [SQL Server]
- database-level securables [SQL Server]
- permissions [SQL Server], granting
ms.assetid: a760c16a-4d2d-43f2-be81-ae9315f38185
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3e79af093de18bc2c4456bb23185405079ef533e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="grant-transact-sql"></a>GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erteilt einem Prinzipal Berechtigungen für ein sicherungsfähiges Element.  Das allgemeine Konzept sieht folgendermaßen aus: GRANT \<Berechtigung> ON \<Objekt> TO \<Benutzer, Anmeldename oder Gruppe>. Eine allgemeine Diskussion zu Berechtigungen finden Sie unter [Berechtigungen &#40;Datenbank-Engine&#41;](../../relational-databases/security/permissions-database-engine.md).  
  
 ![Artikellinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Article link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for GRANT  
GRANT { ALL [ PRIVILEGES ] }  
      | permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      [ ON [ class :: ] securable ] TO principal [ ,...n ]   
      [ WITH GRANT OPTION ] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
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
 ALL  
 Diese Option ist als veraltet markiert und wird nur aus Gründen der Abwärtskompatibilität beibehalten. Damit werden nicht alle möglichen Berechtigungen erteilt. Das Erteilen mit ALL entspricht dem Erteilen der folgenden Berechtigungen: 
  
-   Falls es sich beim sicherungsfähigen Element um eine Datenbank handelt, schließt ALL die Berechtigungen BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE und CREATE VIEW ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine skalare Funktion handelt, schließt ALL die Berechtigungen EXECUTE und REFERENCES ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Tabellenwertfunktion handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine gespeicherte Prozedur handelt, steht ALL für EXECUTE.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Tabelle handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Sicht handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
PRIVILEGES  
 Aus Gründen der Kompatibilität mit ISO eingeschlossen. Ändert das Verhalten von ALL nicht.  
  
*permission*  
 Der Name einer Berechtigung. Die gültigen Zuordnungen von Berechtigungen zu sicherungsfähigen Elementen sind in den im Folgenden aufgeführten untergeordneten Themen beschrieben.  
  
*column*  
 Gibt den Namen einer Spalte in einer Tabelle an, für die Berechtigungen erteilt werden. Die Klammern () sind erforderlich.  
  
*class*  
 Gibt die Klasse des sicherungsfähigen Elements an, für das die Berechtigung erteilt wird. Der Bereichsqualifizierer **::** ist erforderlich.  
  
*securable*  
 Gibt das sicherungsfähige Element an, für das die Berechtigung erteilt wird.  
  
TO *principal*  
 Der Name eines Prinzipals. Die Prinzipale, für die Berechtigungen für ein sicherungsfähiges Element erteilt werden können, sind abhängig vom jeweiligen sicherungsfähigen Element unterschiedlich. Gültige Kombinationen finden Sie in den folgenden Unterthemen.  
  
GRANT OPTION  
 Gibt an, dass der Empfänger die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
AS *principal*  
 Verwenden Sie die AS-Prinzipalklausel, um anzugeben, dass der Prinzipal, der die Berechtigung erteilt hat, ein anderer Prinzipal als die Person sein muss, die die Anweisung ausführt. Nehmen Sie beispielsweise an, dass der Benutzer Mary der principal_id 12 und der Benutzer Raul der principal_id 15 entspricht. Mary führt `GRANT SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;` aus. Daraufhin gibt die Tabelle „sys.database_permissions“ an, dass die „grantor_prinicpal_id“ „15“ (Raul) entspricht, obwohl die Anweisung tatsächlich von Benutzer 12 (Mary) ausgeführt wurde.

Das Verwenden der AS-Klausel wird üblicherweise nicht empfohlen, sofern Sie nicht explizit die Berechtigungskette definieren müssen. Weitere Informationen finden Sie im Abschnitt **Zusammenfassung des Algorithmus zur Berechtigungsprüfung** unter [Berechtigungen (Datenbank-Engine)](../../relational-databases/security/permissions-database-engine.md).

In dieser Anweisung impliziert die Verwendung von AS nicht die Fähigkeit, die Identität eines anderen Benutzers anzunehmen. 
  
## <a name="remarks"></a>Remarks  
 Die vollständige Syntax der GRANT-Anweisung ist sehr komplex. Das Syntaxdiagramm oben wurde vereinfacht, um die Struktur hervorzuheben. Die vollständige Syntax für das Erteilen von Berechtigungen für spezifische sicherungsfähige Elemente wird in den unten aufgeführten Artikeln beschrieben.  
  
 Die REVOKE-Anweisung kann zum Entfernen von erteilten Berechtigungen verwendet werden, und mit der DENY-Anweisung kann verhindert werden, dass einem Prinzipal eine spezifische Berechtigung durch eine GRANT-Anweisung erteilt wird.  
  
 Durch das Erteilen einer Berechtigung wird DENY oder REVOKE für diese Berechtigung aus dem angegebenen sicherungsfähigen Element entfernt. Falls dieselbe Berechtigung aus einem höheren Bereich als dem des sicherungsfähigen Elements verweigert wird, hat DENY Vorrang. Das Aufheben der erteilten Berechtigung in einem höheren Bereich hat jedoch keinen Vorrang.  
  
 Berechtigungen auf Datenbankebene werden innerhalb des Bereichs der angegebenen Datenbank erteilt. Wenn ein Benutzer Berechtigungen für Objekte in einer anderen Datenbank benötigt, erstellen Sie das Benutzerkonto in der anderen Datenbank oder erteilen dem Benutzerkonto Zugriff auf die aktuelle Datenbank und auf die andere Datenbank.  
  
> [!CAUTION]  
>  Eine DENY-Anweisung auf Tabellenebene hat keinen Vorrang vor einer GRANT-Anweisung auf Spaltenebene. Diese Inkonsistenz in der Berechtigungshierarchie wurde aus Gründen der Abwärtskompatibilität beibehalten. Dieses Verhalten wird in einer zukünftigen Version entfernt.  
  
 Die gespeicherte Systemprozedur sp_helprotect gibt Informationen zu Berechtigungen für sicherungsfähige Elemente auf Datenbankebene zurück.  
  
## <a name="with-grant-option"></a>WITH GRANT OPTION  
 Die Anweisung **GRANT** **WITH GRANT OPTION** gibt an, dass der Sicherheitsprinzipal, der die Berechtigung erhält, die Fähigkeit erhält, anderen Sicherheitskonten die angegebene Berechtigung zu erteilen. Wenn es sich bei dem Prinzipal, der die Berechtigung erhält, um eine Rolle oder eine Windows-Gruppe handelt, muss die **AS**-Klausel verwendet werden, wenn die Objektberechtigung Benutzern gewährt werden muss, die keine Elemente der Gruppe oder der Rolle sind. Da nur ein Benutzer anstelle einer Gruppe oder Rolle eine **GRANT**-Anweisung ausführen kann, muss ein spezifisches Element der Gruppe oder Rolle die **AS**-Klausel verwenden, um die Rollen- oder Gruppenmitgliedschaft beim Gewähren der Berechtigung explizit aufzurufen. Das folgende Beispiel zeigt, wie die Option **WITH GRANT OPTION** verwendet wird, wenn sie einer Rolle oder einer Windows-Gruppe gewährt wird.  
  
```  
-- Execute the following as a database owner  
GRANT EXECUTE ON TestProc TO TesterRole WITH GRANT OPTION;  
EXEC sp_addrolemember TesterRole, User1;  
-- Execute the following as User1  
-- The following fails because User1 does not have the permission as the User1  
GRANT EXECUTE ON TestMe TO User2;  
-- The following succeeds because User1 invokes the TesterRole membership  
GRANT EXECUTE ON TestMe TO User2 AS TesterRole;  
```  
  
## <a name="chart-of-sql-server-permissions"></a>Diagramm der SQL Server-Berechtigungen  
 Navigieren Sie zu [https://aka.ms/sql-permissions-poster](https://aka.ms/sql-permissions-poster), um ein Diagramm aller [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Berechtigungen im PDF-Format abzurufen.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) benötigt entweder die Berechtigung selbst mit GRANT OPTION oder eine höhere Berechtigung, die die erteilte Berechtigung impliziert. Falls die AS-Option verwendet wird, gelten zusätzliche Anforderungen. Weitere Informationen hierzu finden Sie im Artikel zu sicherungsfähigen Elementen.  
  
 Objektbesitzer können Berechtigungen für die Objekte erteilen, die sie besitzen. Prinzipale mit CONTROL-Berechtigung für ein sicherungsfähiges Element können die Berechtigung für dieses sicherungsfähige Element erteilen.  
  
 Empfänger der CONTROL SERVER-Berechtigung, wie z. B. Mitglieder der festen Serverrolle sysadmin, können jede beliebige Berechtigung für jedes beliebige sicherungsfähige Element auf dem Server erteilen. Empfänger der CONTROL-Berechtigung in einer Datenbank, z. B. Mitglieder der festen Datenbankrolle db_owner, können jede Berechtigung für ein beliebiges sicherungsfähiges Element in der Datenbank erteilen. Empfänger der CONTROL-Berechtigung für ein Schema können jede beliebige Berechtigung für jedes Objekt innerhalb des Schemas erteilen.  
  
## <a name="examples"></a>Beispiele  
 In der folgenden Tabelle sind die sicherungsfähigen Elemente und Artikel aufgeführt, in denen die für sicherungsfähige Elemente spezifische Syntax beschrieben wird.  
  
|||  
|-|-|  
|Anwendungsrolle|[GRANT (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Assembly|[GRANT (Assemblyberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-assembly-permissions-transact-sql.md)|  
|Asymmetrischer Schlüssel|[GRANT (Berechtigungen für asymmetrische Schlüssel) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-asymmetric-key-permissions-transact-sql.md)|  
|Verfügbarkeitsgruppe|[GRANT (Verfügbarkeitsgruppenberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)|  
|Zertifikat|[GRANT (Zertifikatberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)|  
|Vertrag|[GRANT (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Datenbank|[GRANT (Datenbankberechtigungen) &#40;&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)|
|Datenbankweit gültige Anmeldeinformationen|[GRANT (Datenbankweit gültige Anmeldeinformationen) (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)|  
|Endpunkt|[GRANT (Endpunktberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)|  
|Volltextkatalog|[GRANT (Volltextberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Volltext-Stoppliste|[GRANT (Volltextberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Funktion|[GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Anmeldename|[GRANT (Berechtigungen für Serverprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)|  
|Nachrichtentyp|[GRANT (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Objekt|[GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Warteschlange|[GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Remotedienstbindung|[GRANT (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|-Rolle|[GRANT (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Route|[GRANT (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Schema|[GRANT (Schemaberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-schema-permissions-transact-sql.md)|  
|Sucheigenschaftenliste|[GRANT (Berechtigungen für Sucheigenschaftenlisten) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)|  
|Server|[GRANT (Serverberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)|  
|Dienst|[GRANT (Berechtigungen von Service Broker) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Gespeicherte Prozedur|[GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Symmetrischer Schlüssel|[GRANT (Berechtigungen für symmetrische Schlüssel) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)|  
|Synonym|[GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Systemobjekte|[GRANT (Berechtigungen für Systemobjekte) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)|  
|Tabelle|[GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Typ|[GRANT (Typberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)|  
|Benutzer|[GRANT (Berechtigungen für Datenbankprinzipal) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Anzeigen|[GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|XML-Schemasammlung|[GRANT (Berechtigungen für XML-Schemaauflistungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
