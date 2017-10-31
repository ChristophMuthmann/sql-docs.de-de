---
title: GRANT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bb9bf548f042a4a6f41322fb789a2cd7e5b6bec9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="grant-transact-sql"></a>GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erteilt einem Prinzipal Berechtigungen für ein sicherungsfähiges Element.  Das allgemeine Konzept entspricht GRANT \<bestimmte Berechtigungen > ON \<ein Objekt > TO \<einige Benutzer, Anmeldenamen oder Gruppe >. Eine allgemeine Beschreibung der Berechtigungen finden Sie unter [Berechtigungen &#40; Datenbankmodul &#41;](../../relational-databases/security/permissions-database-engine.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 Diese Option ist als veraltet markiert und wird nur aus Gründen der Abwärtskompatibilität beibehalten. Damit werden nicht alle möglichen Berechtigungen erteilt. Das Erteilen mit ALL entspricht dem Erteilen der folgenden Berechtigungen.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Datenbank handelt, schließt ALL die Berechtigungen BACKUP DATABASE, BACKUP LOG, CREATE DATABASE, CREATE DEFAULT, CREATE FUNCTION, CREATE PROCEDURE, CREATE RULE, CREATE TABLE und CREATE VIEW ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine skalare Funktion handelt, schließt ALL die Berechtigungen EXECUTE und REFERENCES ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Tabellenwertfunktion handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine gespeicherte Prozedur handelt, steht ALL für EXECUTE.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Tabelle handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
-   Falls es sich beim sicherungsfähigen Element um eine Sicht handelt, schließt ALL die Berechtigungen DELETE, INSERT, REFERENCES, SELECT und UPDATE ein.  
  
PRIVILEGES  
 Aus Gründen der Kompatibilität mit ISO eingeschlossen. Ändert das Verhalten von ALL nicht.  
  
*Berechtigung*  
 Der Name einer Berechtigung. Die gültigen Zuordnungen von Berechtigungen zu sicherungsfähigen Elementen sind in den im Folgenden aufgeführten untergeordneten Themen beschrieben.  
  
*Spalte*  
 Gibt den Namen einer Spalte in einer Tabelle an, für die Berechtigungen erteilt werden. Die Klammern () sind erforderlich.  
  
*Klasse*  
 Gibt die Klasse des sicherungsfähigen Elements an, für das die Berechtigung erteilt wird. Der bereichsqualifizierer **::** ist erforderlich.  
  
*sicherungsfähiges Element*  
 Gibt das sicherungsfähige Element an, für das die Berechtigung erteilt wird.  
  
UM *Prinzipal*  
 Ist der Name eines Prinzipals. Die Prinzipale, für die Berechtigungen für ein sicherungsfähiges Element erteilt werden können, sind abhängig vom jeweiligen sicherungsfähigen Element unterschiedlich. Gültige Kombinationen finden Sie in den folgenden Unterthemen.  
  
GRANT OPTION  
 Gibt an, dass der Empfänger die angegebene Berechtigung auch anderen Prinzipalen erteilen kann.  
  
AS *Prinzipal*  
 Verwenden Sie die Dienstprinzipalname AS-Klausel, um anzugeben, dass der Prinzipal aufgezeichnet, wie der berechtigende (Grantor), der die Berechtigung eines Prinzipals als die Person, die die Anweisung ausgeführt werden soll. Beispielsweise annehmen Sie, dass die Benutzerin Mary Principal_id 12 und Benutzer Raul principal 15. Andrea führt `GRANT SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;` nun die Tabelle database_permissions angezeigt wird, dass die Grantor_prinicpal_id 15 (Raul) wurde, auch wenn die Anweisung tatsächlich vom Benutzer 13 (Mary) ausgeführt wurde.

Mithilfe der AS-Klausel ist in der Regel nicht empfehlenswert, wenn Sie explizit die Berechtigung Kette definieren müssen. Weitere Informationen finden Sie unter der **Statuszusammenfassung der Algorithmus zur Berechtigungsprüfung** Abschnitt [Berechtigungen (Datenbankmodul)](../../relational-databases/security/permissions-database-engine.md).

Die Verwendung eines wie in dieser Anweisung impliziert nicht die Möglichkeit, die Identität eines anderen Benutzers anzunehmen. 
  
## <a name="remarks"></a>Hinweise  
 Die vollständige Syntax der GRANT-Anweisung ist sehr komplex. Das Syntaxdiagramm oben wurde vereinfacht, um die Struktur hervorzuheben. Die vollständige Syntax für das Erteilen von Berechtigungen für spezifische sicherungsfähige Elemente wird in den unten aufgeführten Themen beschrieben.  
  
 Die REVOKE-Anweisung kann zum Entfernen von erteilten Berechtigungen verwendet werden, und mit der DENY-Anweisung kann verhindert werden, dass einem Prinzipal eine spezifische Berechtigung durch eine GRANT-Anweisung erteilt wird.  
  
 Durch das Erteilen einer Berechtigung wird DENY oder REVOKE für diese Berechtigung aus dem angegebenen sicherungsfähigen Element entfernt. Falls dieselbe Berechtigung aus einem höheren Bereich als dem des sicherungsfähigen Elements verweigert wird, hat DENY Vorrang. Das Aufheben der erteilten Berechtigung in einem höheren Bereich hat jedoch keinen Vorrang.  
  
 Berechtigungen auf Datenbankebene werden innerhalb des Bereichs der angegebenen Datenbank erteilt. Wenn ein Benutzer Berechtigungen für Objekte in einer anderen Datenbank benötigt, erstellen Sie das Benutzerkonto in der anderen Datenbank oder erteilen dem Benutzerkonto Zugriff auf die aktuelle Datenbank und auf die andere Datenbank.  
  
> [!CAUTION]  
>  Eine DENY-Anweisung auf Tabellenebene hat keinen Vorrang vor einer GRANT-Anweisung auf Spaltenebene. Diese Inkonsistenz in der Berechtigungshierarchie wurde aus Gründen der Abwärtskompatibilität beibehalten. Dieses Verhalten wird in einer zukünftigen Version entfernt.  
  
 Die gespeicherte Systemprozedur sp_helprotect gibt Informationen zu Berechtigungen für sicherungsfähige Elemente auf Datenbankebene zurück.  
  
## <a name="with-grant-option"></a>WITH GRANT OPTION  
 Die **GRANT** ... **MIT GRANT OPTION** gibt an, dass der Sicherheitsprinzipal, der die Berechtigung erhält anderen Sicherheitskonten die angegebene Berechtigung zu erteilen angegeben wird. Wenn der Prinzipal, der die Berechtigung empfängt eine Rolle oder eine Windows-Gruppe ist die **AS** -Klausel muss verwendet werden, wenn die Objektberechtigung muss, um weiteren Benutzern gewährt werden, die nicht Mitglieder der Gruppe oder Rolle sind. Da nur ein Benutzer anstelle einer Gruppe oder Rolle ausführen kann ein **GRANT** -Anweisung, die ein bestimmtes Mitglied der Gruppe oder Rolle verwenden muss die **AS** -Klausel, um die Rollen- oder Gruppenmitgliedschaft explizit aufrufen, wenn er gewährt die Berechtigung. Das folgende Beispiel zeigt wie die **WITH GRANT OPTION** wird verwendet, wenn eine Rolle oder einen Windows-Gruppe gewährt.  
  
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
 Navigieren Sie zu [http://go.microsoft.com/fwlink/?LinkId=229142](http://go.microsoft.com/fwlink/?LinkId=229142), um ein Diagramm aller [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Berechtigungen in Postergröße im PDF-Format abzurufen.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Berechtigende (oder der mit der AS-Option angegebene Prinzipal) benötigt entweder die Berechtigung selbst mit GRANT OPTION oder eine höhere Berechtigung, die die erteilte Berechtigung impliziert. Falls die AS-Option verwendet wird, gelten zusätzliche Anforderungen. Weitere Informationen hierzu finden Sie in den Themen zu einzelnen sicherungsfähigen Elementen.  
  
 Objektbesitzer können Berechtigungen für die Objekte erteilen, die sie besitzen. Prinzipale mit CONTROL-Berechtigung für ein sicherungsfähiges Element können die Berechtigung für dieses sicherungsfähige Element erteilen.  
  
 Empfänger der CONTROL SERVER-Berechtigung, wie z. B. Mitglieder der festen Serverrolle sysadmin, können jede beliebige Berechtigung für jedes beliebige sicherungsfähige Element auf dem Server erteilen. Empfänger der CONTROL-Berechtigung in einer Datenbank, z. B. Mitglieder der festen Datenbankrolle db_owner, können jede Berechtigung für ein beliebiges sicherungsfähiges Element in der Datenbank erteilen. Empfänger der CONTROL-Berechtigung für ein Schema können jede beliebige Berechtigung für jedes Objekt innerhalb des Schemas erteilen.  
  
## <a name="examples"></a>Beispiele  
 In der folgenden Tabelle sind die sicherungsfähigen Elemente und Themen aufgeführt, in denen die für ein sicherungsfähiges Element spezifische Syntax beschrieben wird.  
  
|||  
|-|-|  
|Anwendungsrolle|[GRANT-Berechtigungen für Datenbankprinzipal &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Assembly|[GRANT-Assemblyberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-assembly-permissions-transact-sql.md)|  
|Asymmetrischer Schlüssel|[Erteilen Sie Berechtigungen für asymmetrische Schlüssel &#40; Transact-SQL &#41;](../../t-sql/statements/grant-asymmetric-key-permissions-transact-sql.md)|  
|Verfügbarkeitsgruppe|[Erteilen von Verfügbarkeitsgruppenberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)|  
|Zertifikat|[GRANT (Zertifikatberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)|  
|Vertrag|[Berechtigungen von GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Datenbank|[Erteilen der Datenbankberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)|
|Datenbankweit gültige Anmeldeinformationen|[GRANT datenbankweit gültige Anmeldeinformationen (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)|  
|Endpunkt|[GRANT (Endpunktberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)|  
|Volltextkatalog|[Berechtigungen GRANT Full-Text &#40; Transact-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Volltext-Stoppliste|[Berechtigungen GRANT Full-Text &#40; Transact-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|Funktion|[Erteilen von Objektberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Anmeldename|[GRANT-Berechtigungen für Serverprinzipal &#40; Transact-SQL &#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)|  
|Nachrichtentyp|[Berechtigungen von GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Objekt|[Erteilen von Objektberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Warteschlange|[Erteilen von Objektberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Remotedienstbindung|[Berechtigungen von GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Rolle|[GRANT-Berechtigungen für Datenbankprinzipal &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Route|[Berechtigungen von GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Schema|[GRANT-Schemaberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-schema-permissions-transact-sql.md)|  
|Sucheigenschaftenliste|[GRANT-Sucheigenschaftenlisten-Berechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)|  
|Server|[GRANT (Serverberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)|  
|Dienst|[Berechtigungen von GRANT Service Broker &#40; Transact-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Gespeicherte Prozedur|[Erteilen von Objektberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Symmetrische Schlüssel|[Erteilen Sie Berechtigungen für symmetrische Schlüssel &#40; Transact-SQL &#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)|  
|Synonym|[Erteilen von Objektberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Systemobjekte anzeigen|[GRANT (Berechtigungen für Systemobjekte) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)|  
|Tabelle|[Erteilen von Objektberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|Typ|[GRANT (Typberechtigungen) &#40; Transact-SQL &#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)|  
|Benutzer|[GRANT-Berechtigungen für Datenbankprinzipal &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|Sicht|[Erteilen von Objektberechtigungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|XML-Schemasammlung|[Erteilen Sie Berechtigungen für XML-Schemaauflistungen &#40; Transact-SQL &#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [Sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [Sp_helprotect &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [Sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  

