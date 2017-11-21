---
title: "Erste Schritte mit Berechtigungen für das Datenbankmodul | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- permissions [SQL Server], getting started
ms.assetid: 051af34e-bb5b-403e-bd33-007dc02eef7b
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 01f20dd99963b0bb1be86ddc3e173aef6fb3e8b3
ms.openlocfilehash: 376e591e28bbdddbd635392b24c3d6652f3bd94d
ms.contentlocale: de-de
ms.lasthandoff: 08/11/2017

---
# <a name="getting-started-with-database-engine-permissions"></a>Erste Schritte mit Berechtigungen für das Datenbankmodul
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Berechtigungen im [!INCLUDE[ssDE](../../../includes/ssde-md.md)] werden auf Serverebene über Anmeldungen und Serverrollen und auf Datenbankebene über Datenbankbenutzer und Datenbankrollen verwaltet. Das Modell für [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] stellt innerhalb jeder Datenbank dasselbe System zur Verfügung, doch die Berechtigungen auf Serverebene sind nicht verfügbar. In diesem Thema werden verschiedene grundlegende Sicherheitskonzepte untersucht. Anschließend wird eine typische Implementierung der Berechtigungen beschrieben.  
  
## <a name="security-principals"></a>Sicherheitsprinzipale  
 Sicherheitsprinzipal ist der offizielle Name der Identitäten, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nutzen und denen Berechtigungen für die Ausführung von Aktionen zugewiesen werden können. Dies sind in der Regel Personen oder Personengruppen, doch es kann sich auch um andere Entitäten handeln, die vorgeben, Personen zu sein. Die Sicherheitsprinzipale können mithilfe der aufgelisteten [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]erstellt und verwaltet werden.  
  
 Anmeldungen  
 Anmeldungen sind einzelne Benutzerkonten für die Anmeldung beim [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] unterstützen Anmeldungen auf Grundlage der Windows- und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung. Informationen zu den beiden Anmeldungstypen finden Sie unter [Auswählen eines Authentifizierungsmodus](../../../relational-databases/security/choose-an-authentication-mode.md).  
  
 Feste Serverrollen  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]sind feste Serverrollen eine Gruppe vorkonfigurierter Rollen, die das Erteilen von Berechtigungen für eine Gruppe von Servern erleichtern. Anmeldungen können Rollen mit der `ALTER SERVER ROLE ... ADD MEMBER`-Anweisung hinzugefügt werden. Weitere Informationen finden Sie unter [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md). [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] unterstützt nicht die festen Serverrollen, bietet jedoch zwei Rollen in der „master“-Datenbank (`dbmanager` und `loginmanager`), die wie Serverrollen fungieren.  
  
 Benutzerdefinierte Serverrollen  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]können Sie eigene Serverrollen erstellen und ihnen Berechtigungen auf Serverebene zuweisen. Anmeldungen können Serverrollen mit der `ALTER SERVER ROLE ... ADD MEMBER`-Anweisung hinzugefügt werden. Weitere Informationen finden Sie unter [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md). [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] unterstützt die benutzerdefinierten Serverrollen nicht.  
  
 Datenbankbenutzer  
 Anmeldungen wird Zugriff auf eine Datenbank gewährt, indem in einer Datenbank ein Datenbankbenutzer erstellt und dieser Datenbankbenutzer einer Anmeldung zugeordnet wird. Der Datenbank-Benutzername ist in der Regel identisch mit dem Anmeldenamen, obwohl dies nicht so sein muss. Jeder Datenbankbenutzer ist einer einzelnen Anmeldung zugeordnet. Eine Anmeldung kann nur einem Benutzer in einer Datenbank zugeordnet werden, kann aber als Datenbankbenutzer in mehreren unterschiedlichen Datenbanken zugeordnet werden.  
  
 Es können auch Datenbankbenutzer erstellt werden, die keine entsprechende Anmeldung haben. Diese werden als *eigenständige Datenbankbenutzer*bezeichnet. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] empfiehlt die Verwendung eigenständiger Datenbankbenutzer, da dadurch das Verschieben Ihrer Datenbank auf einen anderen Server erleichtert wird. Wie eine Anmeldung kann ein eigenständiger Datenbankbenutzer entweder die Windows- oder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung verwenden. Weitere Informationen finden Sie unter [Eigenständige Datenbankbenutzer - machen Sie Ihre Datenbank portabel](../../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
 Es gibt 12 Typen von Benutzern mit geringfügigen Unterschieden dahingehend, wie sie sich authentifizieren und wen sie darstellen. Eine Liste von Benutzern finden Sie unter [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md).  
  
 Feste Datenbankrollen  
 Feste Datenbankrollen sind eine Gruppe vorkonfigurierter Rollen, die das Erteilen von Berechtigungen für eine Gruppe von Datenbanken erleichtern. Datenbankbenutzer und benutzerdefinierte Datenbankrollen können festen Datenbankrollen mithilfe der `ALTER ROLE ... ADD MEMBER`-Anweisung hinzugefügt werden. Weitere Informationen finden Sie unter [ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md).  
  
 Benutzerdefinierte Datenbankrollen  
 Benutzer mit der Berechtigung `CREATE ROLE` können neue benutzerdefinierte Datenbankrollen erstellen, um Gruppen von Benutzern mit gemeinsamen Berechtigungen abzubilden. In der Regel werden Berechtigungen der gesamten Rolle erteilt oder verweigert, was die Verwaltung und Überwachung von Berechtigungen vereinfacht. Mithilfe der `ALTER ROLE ... ADD MEMBER`-Anweisung können Datenbankbenutzer den Datenbankrollen hinzugefügt werden. Weitere Informationen finden Sie unter [ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md).  
  
 Andere Prinzipale  
 Weitere Sicherheitsprinzipale, die hier nicht behandelt werden, sind u. a. Anwendungsrollen sowie Anmeldungen und Benutzer auf Grundlage von Zertifikaten oder asymmetrischen Schlüsseln.  
  
 Eine Grafik mit den Beziehungen zwischen Windows-Benutzern, Windows-Gruppen, Anmeldungen und Datenbankbenutzern finden Sie unter [Erstellen eines Datenbankbenutzers](../../../relational-databases/security/authentication-access/create-a-database-user.md).  
  
## <a name="typical-scenario"></a>Typisches Szenario  
 Das folgende Beispiel zeigt eine allgemeine und empfohlene Methode zum Konfigurieren von Berechtigungen.  
  
#### <a name="in-active-directory-or-azure-active-directory"></a>In Active Directory oder Azure Active Directory:  
  
1.  Erstellen Sie einen Windows-Benutzer für jede Person.  
  
2.  Erstellen Sie Windows-Gruppen, die die Arbeitseinheiten und Arbeitsfunktionen darstellen.  
  
3.  Fügen Sie Windows-Benutzer den Windows-Gruppen hinzu.  
  
#### <a name="if-the-person-connecting-will-be-connecting-to-many-databases"></a>Wenn die Person eine Verbindung mit mehreren Datenbanken herstellen möchte  
  
1.  Erstellen Sie für die Windows-Gruppen eine Anmeldung. (Wenn Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung verwenden, überspringen Sie die Schritte für Active Directory, und erstellen Sie hier [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierungsanmeldungen.)  
  
2.  Erstellen Sie in der Benutzerdatenbank einen Datenbankbenutzer für die Anmeldung, die die Windows-Gruppen darstellt.  
  
3.  Erstellen Sie in der Benutzerdatenbank eine oder mehrere benutzerdefinierte Datenbankrollen, die jeweils eine ähnliche Funktion darstellen. Beispiele: Finanzanalyst und Vertriebsanalyst.  
  
4.  Fügen Sie die Datenbankbenutzer einer oder mehreren benutzerdefinierten Datenbankrollen hinzu.  
  
5.  Erteilen Sie den benutzerdefinierten Datenbankrollen Berechtigungen.  
  
#### <a name="if-the-person-connecting-will-be-connecting-to-only-one-database"></a>Wenn die Person eine Verbindung mit nur einer Datenbank herstellen möchte  
  
1.  Erstellen Sie für die Windows-Gruppen eine Anmeldung. (Wenn Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung verwenden, überspringen Sie die Schritte für Active Directory, und erstellen Sie hier [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierungsanmeldungen.)  
  
2.  Erstellen Sie in der Benutzerdatenbank für die Windows-Gruppen einen eigenständigen Datenbankbenutzer. (Wenn Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung verwenden, überspringen Sie die Schritte für die Active Directory, und erstellen Sie hier die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung für den eigenständigen Datenbankbenutzer.)  
  
3.  Erstellen Sie in der Benutzerdatenbank eine oder mehrere benutzerdefinierte Datenbankrollen, die jeweils eine ähnliche Funktion darstellen. Beispiele: Finanzanalyst und Vertriebsanalyst.  
  
4.  Fügen Sie die Datenbankbenutzer einer oder mehreren benutzerdefinierten Datenbankrollen hinzu.  
  
5.  Erteilen Sie den benutzerdefinierten Datenbankrollen Berechtigungen.  
  
 Das typische Ergebnis an diesem Punkt ist, dass ein Windows-Benutzer Mitglied einer Windows-Gruppe ist. Die Windows-Gruppe verfügt in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]über eine Anmeldung. Die Anmeldung ist einer Benutzeridentität in der Benutzerdatenbank zugeordnet. Der Benutzer ist Mitglied einer Datenbankrolle. Nun müssen Sie der Rolle Berechtigungen hinzufügen.  
  
## <a name="assigning-permissions"></a>Zuweisen von Berechtigungen  
 Die meisten Berechtigungsanweisungen haben das folgende Format:  
  
```  
AUTHORIZATION  PERMISSION  ON  SECURABLE::NAME  TO  PRINCIPAL;  
```  
  
-   `AUTHORIZATION` muss `GRANT`, `REVOKE` , `DENY`oder sein.  
  
-   `PERMISSION` legt fest, welche Aktion zulässig oder unzulässig ist. [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] In können 230 Berechtigungen angegeben werden. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] bietet weniger Berechtigungen, da einige Aktionen in Azure nicht relevant sind. Die Berechtigungen sind im Thema [Berechtigungen &#40;Datenbankmodul&#41;](../../../relational-databases/security/permissions-database-engine.md) und im nachstehenden Diagramm aufgeführt.  
  
-   `ON SECURABLE::NAME` ist der Typ des sicherungsfähigen Objektes (Server, Serverobjekt, Datenbank oder Datenbankobjekt) und sein Name. Einige Berechtigungen erfordern `ON SECURABLE::NAME` nicht, da diese Angabe unmissverständlich oder im Kontext nicht zulässig ist. Die Berechtigung `CREATE TABLE` erfordert z.B. nicht die `ON SECURABLE::NAME` -Klausel. (Beispiel: `GRANT CREATE TABLE TO Mary;` erlaubt Mary das Erstellen von Tabellen.)  
  
-   `PRINCIPAL` ist der Sicherheitsprinzipal (Anmeldung, Benutzer oder Rolle), der die Berechtigung empfängt oder verliert. Erteilen Sie Berechtigungen nach Möglichkeit stets Rollen.  
  
 Die folgende beispielhafte „Grant“-Anweisung erteilt die Berechtigung `UPDATE` für die Tabelle oder Sicht `Parts` , die im Schema `Production` für die Rolle mit dem Namen `PartsTeam`enthalten ist:  
  
```  
GRANT UPDATE ON OBJECT::Production.Parts TO PartsTeam;  
```  
  
 Berechtigungen werden Sicherheitsprinzipalen (Anmeldungen, Benutzer und Rollen) mithilfe der `GRANT` -Anweisung erteilt. Berechtigungen werden mithilfe des  `DENY` -Befehls explizit verweigert. Eine zuvor erteilte oder verweigerte Berechtigung wird mithilfe der `REVOKE` -Anweisung entfernt. Berechtigungen sind kumulativ, was heißt, dass der Benutzer alle Berechtigungen erhält, die dem Benutzer, der Anmeldung oder den Gruppe erteilt wurden, denen der Benutzer angehört. Durch jedwede Berechtigungsverweigerung werden alle erteilten Berechtigungen außer Kraft gesetzt.  
  
> [!TIP]  
>  Ein häufiger Fehler ist der Versuch, `GRANT` über `DENY` anstatt über `REVOKE`zu entfernen. Dies kann Probleme verursachen, wenn ein Benutzer Berechtigungen aus mehreren Quellen empfängt, was recht häufig vorkommt. Das folgende Beispiel veranschaulicht das Prinzip.  
  
 Die Gruppe „Sales“ erhält `SELECT` -Berechtigungen für die Tabelle „OrderStatus“ über die Anweisung `GRANT SELECT ON OBJECT::OrderStatus TO Sales;`. Der Benutzer Ted ist Mitglied der Rolle „Sales“. Über die Anweisung `SELECT` wurde Ted auch die Berechtigung  `GRANT SELECT ON OBJECT::OrderStatus TO Ted;`für die Tabelle „OrderStatus“ unter seinem eigenen Benutzernamen erteilt. Angenommen, der Administrator möchte die Berechtigung `GRANT` aus der Rolle „Sales“ entfernen.  
  
-   Wenn der Administrator `REVOKE SELECT ON OBJECT::OrderStatus TO Sales;`ordnungsgemäß ausführt, behält Ted über seine individuelle `SELECT` -Anweisung `GRANT` -Zugriff auf die Tabelle „OrderStatus“.  
  
-   Wenn der Administrator `DENY SELECT ON OBJECT::OrderStatus TO Sales;` nicht ordnungsgemäß ausführt, wird Ted als Mitglied der Rolle „Sales“ die `SELECT` -Berechtigung verweigert, da `DENY` für die Rolle „sales“ seine individuelle  `GRANT`-Einstellung überschreibt.  
  
> [!NOTE]  
>  Berechtigungen können mithilfe von [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]konfiguriert werden. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf das sicherungsfähige Objekt, und wählen Sie **Eigenschaften**aus. Wählen Sie die Seite **Berechtigungen** aus. Hilfe zum Verwenden der Seite „Berechtigungen“, finden Sie unter [Seite 'Berechtigungen' oder 'Sicherungsfähige Elemente'](../../../relational-databases/security/permissions-or-securables-page.md).  
  
## <a name="permission-hierarchy"></a>Berechtigungshierarchie  
 Berechtigungen einer Hierarchie aus über- und untergeordneten Elementen. Wenn Sie also die Berechtigung `SELECT` für eine Datenbank erteilen, enthält diese Berechtigung die Berechtigung `SELECT` für alle (untergeordneten) Schemas in der Datenbank. Wenn Sie die Berechtigung `SELECT` für ein Schema erteilen, enthält sie die Berechtigung `SELECT` für alle (untergeordneten) Tabellen und Sichten im Schema. Die Berechtigungen sind transitiv. Das heißt, wenn Sie die Berechtigung `SELECT` für eine Datenbank erteilen, schließt dies die Berechtigung `SELECT` für alle (untergeordneten) Schemas sowie alle (zwei Ebenen untergeordneten) Tabellen und Sichten ein.  
  
 Berechtigungen können auch abdeckende Berechtigungen aufweisen. Die Berechtigung `CONTROL` für ein Objekt erteilt Ihnen normalerweise alle anderen Berechtigungen für das Objekt.  
  
 Da sowohl die Hierarchie über- und untergeordneter Berechtigungen als auch die abdeckende Berechtigungshierarchie für dieselbe Berechtigung gelten können, kann das Berechtigungssystem kompliziert sein. Angenommen, es gibt eine Tabelle (Region) in einem Schema (Customers) in einer Datenbank (SalesDB).  
  
-   `CONTROL` Die Berechtigung für die Tabelle „Region“ umfasst alle anderen Berechtigungen für die Tabelle „Region“, einschließlich `ALTER`, `SELECT`, `INSERT`,  `UPDATE`, `DELETE`und einiger anderer Berechtigungen.  
  
-   `SELECT` für das Schema „Customers“, das Besitzer der Tabelle „Region“ ist, schließt die Berechtigung `SELECT` für die Tabelle „Region“ ein.  
  
 Die Berechtigung `SELECT` für die Tabelle „Region“ kann also mithilfe einer dieser sechs Anweisungen erteilt werden:  
  
```  
GRANT SELECT ON OBJECT::Region TO Ted;   
  
GRANT CONTROL ON OBJECT::Region TO Ted;   
  
GRANT SELECT ON SCHEMA::Customers TO Ted;   
  
GRANT CONTROL ON SCHEMA::Customers TO Ted;   
  
GRANT SELECT ON DATABASE::SalesDB TO Ted;   
  
GRANT CONTROL ON DATABASE::SalesDB TO Ted;  
```  
  
## <a name="grant-the-least-permission"></a>Erteilen der geringstmöglichen Berechtigung  
 Die erste oben aufgeführte Berechtigung (`GRANT SELECT ON OBJECT::Region TO Ted;`) ist die präziseste, d.h., diese Anweisung ist die geringstmögliche Berechtigung, die die Berechtigung `SELECT`erteilt. Zu ihr gehören keine Berechtigungen für untergeordnete Objekte. Es ist ein gutes Prinzip, stets die geringstmögliche Berechtigung zu erteilen. Führen Sie die Erteilung jedoch auf höheren Ebenen aus (eigentlich ein Widerspruch), um das Erteilungssystem zu vereinfachen. Wenn also Ted Berechtigungen für das gesamte Schema braucht, erteilen Sie die Berechtigung `SELECT` einmal auf Schemaebene, anstatt `SELECT` mehrfach auf Tabellen- oder Sichtebene zu erteilen. Der Entwurf der Datenbank hat viel Einfluss den möglichen Erfolg dieser Strategie. Diese Strategie funktioniert am besten, wenn Ihre Datenbank so konzipiert ist, dass Objekte, die identische Berechtigungen benötigen, in einem einzigen Schema enthalten sind.  
  
## <a name="list-of-permissions"></a>Liste der Berechtigungen  
 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] hat 230 Berechtigungen. [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] hat 219 Berechtigungen. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] hat 214 Berechtigungen. [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] hat 195 Berechtigungen. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]Obwohl , [!INCLUDE[ssDW](../../../includes/ssdw-md.md)], und [!INCLUDE[ssAPS](../../../includes/ssaps-md.md)] einige Berechtigungen bereitstellen, die nicht für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]gelten, haben sie insgesamt weniger Berechtigungen, da sie nur einen Teil des Datenbankmoduls verfügbar machen. Die folgende Grafik zeigt die Berechtigungen und ihre Beziehungen zueinander. Einige der Berechtigungen auf höherer Ebene (z.B. `CONTROL SERVER`) sind mehrmals aufgeführt. In diesem Thema ist nicht ausreichend Platz, um das Poster entsprechend darzustellen. Klicken Sie auf das Bild zum Herunterladen der **Poster zu den Datenbankmodulberechtigungen** im PDF-Format.  
  
[![Datenbankmodulberechtigungen](../../../relational-databases/security/media/database-engine-permissions.PNG)](http://go.microsoft.com/fwlink/?LinkId=229142)
 
 Eine Grafik mit den Beziehungen zwischen den [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Prinzipalen und Servern und Datenbankobjekten finden Sie unter [Berechtigungshierarchie &#40;Datenbankmodul&#41;](../../../relational-databases/security/permissions-hierarchy-database-engine.md).  
  
## <a name="permissions-vs-fixed-server-and-fixed-database-roles"></a>Berechtigungen im Vergleich mit festen Server- und Datenbankrollen  
 Die Berechtigungen der festen Serverrollen und festen Datenbankrollen sind ähnlich, jedoch nicht genau identisch mit präzisen Berechtigungen. Mitglieder der festen Serverrolle `sysadmin` haben z.B. alle Berechtigungen für die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Gleiches gilt für Anmeldungen mit der Berechtigung `CONTROL SERVER` . Durch Erteilen der Berechtigung `CONTROL SERVER` wird eine Anmeldung jedoch nicht Mitglied der festen Serverrolle „sysadmin“. Und durch Hinzufügen einer Anmeldung zur festen Serverrolle `sysadmin` wird der Anmeldung nicht explizit die Berechtigung `CONTROL SERVER` erteilt. Mitunter überprüft eine gespeicherte Prozedur Berechtigungen, indem die feste Rolle und nicht die präzise Berechtigung überprüft wird. Das Trennen einer Datenbank erfordert z.B. die Mitgliedschaft in der festen Datenbankrolle `db_owner` . Die entsprechende Berechtigung `CONTROL DATABASE` reicht nicht aus. Diese beiden Systeme arbeiten parallel, interagieren allerdings nur selten. Microsoft empfiehlt, nach Möglichkeit das neuere, präzise Berechtigungssystem anstelle der festen Rollen zu verwenden.
  
## <a name="monitoring-permissions"></a>Überwachen von Berechtigungen  
 Die folgenden Sichten geben Sicherheitsinformationen zurück.  
  
-   Die Anmeldungen und benutzerdefinierten Serverrollen auf einem Server können mithilfe der Sicht `sys.server_principals` untersucht werden. Diese Sicht ist in [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]nicht verfügbar.  
  
-   Die Benutzer und benutzerdefinierten Rollen in einer Datenbank können mithilfe der Sicht `sys.database_principals` untersucht werden.  
  
-   Die Anmeldungen erteilten Berechtigungen und benutzerdefinierten festen Serverrollen können mithilfe der Sicht `sys.server_permissions` untersucht werden. Diese Sicht ist in [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]nicht verfügbar.  
  
-   Die Benutzern erteilten Berechtigungen und benutzerdefinierten festen Datenbankrollen können mithilfe der Sicht `sys.database_permissions` untersucht werden.  
  
-   Die Mitgliedschaft in einer Datenbankrolle kann mithilfe der Sicht `sys. sys.database_role_members` untersucht werden.  
  
-   Die Mitgliedschaft in einer Serverrolle kann mithilfe der Sicht `sys.server_role_members` untersucht werden. Diese Sicht ist in [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]nicht verfügbar.  
  
-   Weitere sicherheitsbezogene Sichten finden Sie unter [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md) erstellt und verwaltet werden.  
  
### <a name="useful-transact-sql-statements"></a>Verwenden von Transact-SQL-Anweisungen  
 Die folgenden Anweisungen geben nützliche Informationen zu Berechtigungen zurück.  
  
 Führen Sie die folgende Anweisung in einer Datenbank aus, um die expliziten Berechtigungen zurückzugeben, die in einer Datenbank ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]) erteilt oder verweigert wurden.  
  
```tsql  
SELECT   
    perms.state_desc AS State,   
    permission_name AS [Permission],   
    obj.name AS [on Object],   
    dPrinc.name AS [to User Name]  
FROM sys.database_permissions AS perms  
JOIN sys.database_principals AS dPrinc  
    ON perms.grantee_principal_id = dPrinc.principal_id  
JOIN sys.objects AS obj  
    ON perms.major_id = obj.object_id;  
```  
  
 Um die Mitglieder der Serverrollen zurückgegeben (nur[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), führen Sie die folgende Anweisung aus.  
  
```tsql  
SELECT sRole.name AS [Server Role Name] , sPrinc.name AS [Members]  
FROM sys.server_role_members AS sRo  
JOIN sys.server_principals AS sPrinc  
    ON sRo.member_principal_id = sPrinc.principal_id  
JOIN sys.server_principals AS sRole  
    ON sRo.role_principal_id = sRole.principal_id;  
```  
  
 
 Führen Sie die folgende Anweisung in der Datenbank aus, um die Mitglieder der Datenbankrollen zurückzugeben ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]).  
  
```tsql  
SELECT dRole.name AS [Database Role Name], dPrinc.name AS [Members]  
FROM sys.database_role_members AS dRo  
JOIN sys.database_principals AS dPrinc  
    ON dRo.member_principal_id = dPrinc.principal_id  
JOIN sys.database_principals AS dRole  
    ON dRo.role_principal_id = dRole.principal_id;  
```  
  
## <a name="next-steps"></a>Nächste Schritte  
 Weitere Themen, die Ihnen den Einstieg erleichtern, finden Sie unter:  
  
-   [Tutorial: Erste Schritte mit dem Datenbankmodul](../../../relational-databases/tutorial-getting-started-with-the-database-engine.md) [Erstellen einer Datenbank &#40;Tutorial&#41;](../../../t-sql/lesson-1-1-creating-a-database.md)  
  
-   [Lernprogramm: SQL Server Management Studio](../../../tools/sql-server-management-studio/tutorial-sql-server-management-studio.md)  
  
-   [Lernprogramm: Schreiben von Transact-SQL-Anweisungen](../../../t-sql/tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)   
 [Sicherheitsbezogene dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Sicherheitskatalogsichten &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Ermitteln effektiver Datenbankmodulberechtigungen](../../../relational-databases/security/authentication-access/determining-effective-database-engine-permissions.md)
  
  

