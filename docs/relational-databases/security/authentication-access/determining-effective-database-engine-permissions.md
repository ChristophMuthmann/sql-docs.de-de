---
title: Ermitteln effektiver Datenbankmodulberechtigungen | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions, effective
- effective permissions
ms.assetid: 273ea09d-60ee-47f5-8828-8bdc7a3c3529
caps.latest.revision: 5
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d21efb4495f786b6000fe0b8675fa042b4d2ca6e
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="determining-effective-database-engine-permissions"></a>Ermitteln effektiver Datenbankmodulberechtigungen
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

Dieses Thema beschreibt, wie Sie feststellen können, wer über Berechtigungen für verschiedene Objekte im SQL Server-Datenbankmodul verfügt. SQL Server implementiert zwei Berechtigungssysteme für das Datenbankmodul. Ein älteres System fester Datenbankrollen hat vorkonfigurierte Berechtigungen. Ab SQL Server 2005 ist ein flexibleres und präziseres System verfügbar. (Die Informationen in diesem Thema gelten für SQL Server ab Version 2005. Einige Arten von Berechtigungen sind in einigen Versionen von SQL Server nicht verfügbar.)

>  [!IMPORTANT] 
>  * Die effektiven Berechtigungen sind das Aggregat von beiden Berechtigungssystemen. 
>  * Eine DOS-Berechtigung überschreibt eine Gewährung von Berechtigungen. 
>  * Wenn ein Benutzer ein Mitglied der festen Serverrolle „sysadmin“ ist, werden Berechtigungen nicht darüber hinaus überprüft, damit Verweigerungen nicht erzwungen werden. 
>  * Die alten und neuen Systeme sind vergleichbar. Z.B. ist die Mitgliedschaft in der festen `sysadmin`-Serverrolle vergleichbar mit der `CONTROL SERVER`-Berechtigung. Die Systeme sind jedoch nicht identisch. Wenn eine Anmeldung beispielsweise nur über die `CONTROL SERVER`-Berechtigung verfügt und eine gespeicherte Prozedur die Mitgliedschaft in der festen `sysadmin`-Serverrolle überprüft, dann kann die Überprüfung der Berechtigung nicht ausgeführt werden. Das Gegenteil trifft ebenfalls zu. 


## <a name="summary"></a>Zusammenfassung   
* Eine Berechtigung auf Serverebene stammt von einer Mitgliedschaft in der festen Serverrolle oder von benutzerdefinierten Serverrollen. Jeder Benutzer gehört zur festen `public`-Serverrolle und erhält jede dort zugewiesene Berechtigung.   
* Berechtigungen auf Serverebene können von Berechtigungen für Anmeldungen oder benutzerdefinierten Serverrollen stammen.   
* Berechtigungen auf Datenbankebene können aus der Mitgliedschaft in festen Datenbankrollen oder benutzerdefinierten Datenbankrollen in jeder Datenbank stammen. Jeder gehört zu den festen `public`-Datenbankrollen und empfängt jede zugewiesene Berechtigung.   
* Berechtigungen auf Datenbankebene können von Berechtigungen für Benutzer oder benutzerdefinierten Datenbankrollen in jeder Datenbank stammen.   
* Berechtigungen können von der `guest`-Anmeldung oder dem aktivierten `guest`-Datenbankbenutzer empfangen werden. Die `guest`-Anmeldenamen und -Benutzer sind standardmäßig deaktiviert.   
* Windows-Benutzer können Mitglieder der Windows-Gruppen sein, die über Anmeldenamen verfügen können. SQL Server erfährt von der Windows-Gruppenmitgliedschaft, wenn ein Windows-Benutzer eine Verbindung herstellt und ein Windows-Token mit der Sicherheits-ID einer Windows-Gruppe darstellt. Da SQL Server automatische Updates nicht über die Windows-Gruppenmitgliedschaften verwaltet oder erhält, kann SQL Server die Berechtigungen der Windows-Benutzer nicht zuverlässig anzeigen, die von der Windows-Gruppenmitgliedschaft empfangen werden.   
* Berechtigungen können erworben werden, indem zu einer Anwendungsrolle gewechselt und das Kennwort bereitgestellt wird.   
* Berechtigungen können erworben werden, indem eine gespeicherte Prozedur ausgeführt wird, die die `EXECUTE AS`-Klausel einschließt.   
* Berechtigungen können mit der `IMPERSONATE`-Berechtigung durch Anmeldenamen oder Benutzer erworben werden.   
* Mitglieder der Administratorgruppe des lokalen Computers können immer ihre Berechtigungen auf `sysadmin` erhöhen. (Gilt nicht für die SQL-Datenbank.)  
* Mitglieder der festen `securityadmin`-Serverrolle können viele ihrer Berechtigungen und in einigen Fällen auch die Berechtigungen auf `sysadmin` erhöhen. (Gilt nicht für die SQL-Datenbank.)   
* SQL Server-Administratoren können Informationen zu allen Anmeldungen und Benutzern sehen. Weniger privilegierten Benutzern werden in der Regel nur Informationen zu ihren eigenen Identitäten angezeigt.

## <a name="older-fixed-role-permission-system"></a>Ältere feste Rollenberechtigungssysteme

Feste Serverrollen und feste Datenbankrollen verfügen über vorkonfigurierte Berechtigungen, die nicht geändert werden können. Um zu bestimmen, wer Mitglied der festen Serverrolle ist, führen Sie die folgende Abfrage aus.    
>  [!NOTE] 
>  Dies gilt nicht für SQL-Datenbank oder SQL Data Warehouse, bei denen die Berechtigungen auf Serverebene nicht verfügbar sind. Die `is_fixed_role`-Spalte von `sys.server_principals` wurde zu SQL Server 2012 hinzugefügt. Sie ist für ältere Versionen von SQL Server nicht erforderlich.  
```tsql
SELECT SP1.name AS ServerRoleName, 
 isnull (SP2.name, 'No members') AS LoginName   
 FROM sys.server_role_members AS SRM
 RIGHT OUTER JOIN sys.server_principals AS SP1
   ON SRM.role_principal_id = SP1.principal_id
 LEFT OUTER JOIN sys.server_principals AS SP2
   ON SRM.member_principal_id = SP2.principal_id
 WHERE SP1.is_fixed_role = 1 -- Remove for SQL Server 2008
 ORDER BY SP1.name;
```
>  [!NOTE] 
>  * Alle Anmeldenamen sind Mitglieder der öffentlichen Rollen und können nicht entfernt werden. 
>  * Diese Abfrage überprüft die Tabellen in der Master-Datenbank, sie kann jedoch in jeder Datenbank für das lokale Produkt ausgeführt werden. 

Um zu bestimmen, wer die Mitglieder einer festen Datenbankrolle sind, führen Sie die folgende Abfrage in jeder Datenbank aus.
```tsql
SELECT DP1.name AS DatabaseRoleName, 
   isnull (DP2.name, 'No members') AS DatabaseUserName 
 FROM sys.database_role_members AS DRM
 RIGHT OUTER JOIN sys.database_principals AS DP1
   ON DRM.role_principal_id = DP1.principal_id
 LEFT OUTER JOIN sys.database_principals AS DP2
   ON DRM.member_principal_id = DP2.principal_id
 WHERE DP1.is_fixed_role = 1
 ORDER BY DP1.name;
```
Um die Berechtigungen zu verstehen, die jeder Rolle gewährt werden, finden Sie Rollenbeschreibungen und Illustrationen in der Onlinedokumentation ([Rollen auf Serverebene](../../../relational-databases/security/authentication-access/server-level-roles.md) und [Rollen auf Datenbankebene](../../../relational-databases/security/authentication-access/database-level-roles.md)).

## <a name="newer-granular-permission-system"></a>Neuere präzise Berechtigungssysteme

Dieses System ist sehr flexibel, was bedeutet, dass es kompliziert sein kann, wenn die Personen, die es einrichten, sehr präzise sein möchten. Das ist nicht unbedingt schlecht. Ich hoffe, dass meine Bank präzise ist. Zur Vereinfachung könnten Sie Rollen erstellen, Rollen Berechtigungen zuweisen und dann Personengruppen zu den Rollen hinzufügen. Und es ist einfacher, wenn das Entwicklungsteam für die Datenbank die Aktivitäten nach Schema trennt und dann die Rollenberechtigungen für ein ganzes Schema statt für einzelne Tabellen oder Prozeduren erteilt. Aber die reale Welt ist komplex, und wir müssen davon ausgehen, dass Unternehmen unerwartete Sicherheitsanforderungen erstellen müssen.   

Die folgende Grafik zeigt die Berechtigungen und ihre Beziehungen zueinander. Einige der Berechtigungen auf höherer Ebene (z.B. `CONTROL SERVER`) sind mehrmals aufgeführt. In diesem Thema ist nicht ausreichend Platz, um das Poster entsprechend darzustellen. Klicken Sie auf das Bild zum Herunterladen der **Poster zu den Datenbankmodulberechtigungen** im PDF-Format.  
  
 [![Datenbankmodulberechtigungen](../../../relational-databases/security/media/database-engine-permissions.PNG)](http://go.microsoft.com/fwlink/?LinkId=229142)

### <a name="security-classes"></a>Sicherheitsklassen

Berechtigungen können auf Serverebene, Datenbankebene, Schemaebene oder Objektebene usw. erteilt werden. Es gibt 26 Ebenen (genannt Klassen). Die vollständige Liste der Klassen in alphabetischer Reihenfolge lautet: `APPLICATION ROLE`, `ASSEMBLY`, `ASYMMETRIC KEY`, `AVAILABILITY GROUP`, `CERTIFICATE`, `CONTRACT`, `DATABASE`, `DATABASE` `SCOPED CREDENTIAL`, `ENDPOINT`, `FULLTEXT CATALOG`, `FULLTEXT STOPLIST`, `LOGIN`, `MESSAGE TYPE`, `OBJECT`, `REMOTE SERVICE BINDING`, `ROLE`, `ROUTE`, `SCHEMA`, `SEARCH PROPERTY LIST`, `SERVER`, `SERVER ROLE`, `SERVICE`, `SYMMETRIC KEY`, `TYPE`, `USER` und `XML SCHEMA COLLECTION`. (Einige Klassen sind für bestimmte Typen von SQL Server nicht verfügbar.) Vollständige Informationen zu jeder Klasse erfordern eine andere Abfrage.

### <a name="principals"></a>Prinzipale

Dateiberechtigungen werden an Prinzipale erteilt. Prinzipale können Serverrollen, Anmeldenamen, Datenbankrollen oder Benutzer sein. Anmeldungen können Windows-Gruppen darstellen, die viele Windows-Benutzer enthalten. Da Windows-Gruppen nicht von SQL Server verwaltet werden, weiß SQL Server nicht immer, wer Mitglied einer Windows-Gruppe ist. Wenn ein Windows-Benutzer mit SQL Server verbunden ist, enthält das Anmeldungspaket das Token der Windows-Gruppenmitgliedschaft für den Benutzer.

Wenn ein Windows-Benutzer eine Verbindung mithilfe einer Anmeldung auf Basis einer Windows-Gruppe herstellt, könnten einige Aktivitäten SQL Server benötigen. Dieser würde eine Anmeldung oder einen Benutzer erstellen, der die einzelnen Windows-Benutzer darstellt. Z.B. enthält eine Windows-Gruppe (Techniker) Benutzer (Mary, Todd, Pat) und die Techniker-Gruppe verfügt über ein Datenbankbenutzerkonto. Wenn Mary über eine Berechtigung verfügt und eine Tabelle erstellt kann ein Benutzer (nämlich Mary) als Besitzer der Tabelle erstellt werden. Wenn Todd eine Berechtigung verweigert wird, über die der Rest der Techniker-Gruppe verfügt, dann muss der Benutzer Todd die Möglichkeit erhalten, die Berechtigungsverweigerung nachverfolgen zu können.

Denken Sie daran, dass ein Windows-Benutzer Mitglied von mehr als einer Windows-Gruppe (z.B. sowohl Techniker und Manager) sein könnte. Berechtigungen, die der Techniker- oder Manager-Anmeldung, den individuellen Benutzern oder Rollen, in denen der Benutzer Mitglied ist, gewährt oder verweigert werden, werden alle aggregiert und für die effektiven Berechtigungen ausgewertet. Die `HAS_PERMS_BY_NAME`-Funktion kann anzeigen, ob ein Benutzer oder Anmeldename über eine bestimmte Berechtigung verfügt. Es gibt jedoch keine offensichtliche Möglichkeit zur Bestimmung der Quelle der Erteilung oder Verweigerung der Berechtigung. Sie müssen die Liste der Berechtigungen durchsuchen und vielleicht auch ausprobieren.

## <a name="useful-queries"></a>Nützliche Abfragen

### <a name="server-permissions"></a>Serverberechtigungen

Die folgende Abfrage gibt eine Liste der Berechtigungen zurück, die auf Serverebene erteilt oder verweigert wurden. Diese Abfrage sollte in der Master-Datenbank ausgeführt werden.   
>  [!NOTE] 
>  Berechtigungen auf Serverebene können nicht auf SQL-Datenbank oder SQL Data Warehouse abgefragt oder erteilt werden.   
```tsql
SELECT pr.type_desc, pr.name, 
 isnull (pe.state_desc, 'No permission statements') AS state_desc, 
 isnull (pe.permission_name, 'No permission statements') AS permission_name 
 FROM sys.server_principals AS pr
 LEFT OUTER JOIN sys.server_permissions AS pe
   ON pr.principal_id = pe.grantee_principal_id
 WHERE is_fixed_role = 0 -- Remove for SQL Server 2008
 ORDER BY pr.name, type_desc;
```

### <a name="database-permissions"></a>Datenbankberechtigungen

Die folgende Abfrage gibt eine Liste der Berechtigungen zurück, die auf Datenbankebene erteilt oder verweigert wurden. Diese Abfrage sollte in jeder Datenbank ausgeführt werden.   
```tsql
SELECT pr.type_desc, pr.name, 
 isnull (pe.state_desc, 'No permission statements') AS state_desc, 
 isnull (pe.permission_name, 'No permission statements') AS permission_name 
FROM sys.database_principals AS pr
LEFT OUTER JOIN sys.database_permissions AS pe
    ON pr.principal_id = pe.grantee_principal_id
WHERE pr.is_fixed_role = 0 
ORDER BY pr.name, type_desc;
```

Jede Klasse der Berechtigungstabelle kann mit anderen Systemansichten verknüpft werden, die verwandte Informationen über die Klasse des sicherungsfähigen Elements bereitstellen. Die folgende Abfrage enthält z.B. den Namen des Datenbankobjekts, das von der Berechtigung betroffen ist.    
```tsql
SELECT pr.type_desc, pr.name, pe.state_desc, 
 pe.permission_name, s.name + '.' + oj.name AS Object, major_id
 FROM sys.database_principals AS pr
 JOIN sys.database_permissions AS pe
   ON pr.principal_id = pe.grantee_principal_id
 JOIN sys.objects AS oj
   ON oj.object_id = pe.major_id
 JOIN sys.schemas AS s
   ON oj.schema_id = s.schema_id
 WHERE class_desc = 'OBJECT_OR_COLUMN';
```
Verwenden Sie die `HAS_PERMS_BY_NAME`-Funktion, um zu bestimmen, ob ein bestimmter Benutzer (in diesem Fall `TestUser`) über eine Berechtigung verfügt. Beispiel:   
```tsql
EXECUTE AS USER = 'TestUser';
SELECT HAS_PERMS_BY_NAME ('dbo.T1', 'OBJECT', 'SELECT');
REVERT;
```
Die Details der Syntax finden Sie unter [HAS_PERMS_BY_NAME](../../../t-sql/functions/has-perms-by-name-transact-sql.md).

## <a name="see-also"></a>Siehe auch:

[Erste Schritte mit Berechtigungen für das Datenbankmodul](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)    
[Tutorial: Erste Schritte mit dem Datenbankmodul](Tutorial:%20Getting%20Started%20with%20the%20Database%20Engine.md) 


