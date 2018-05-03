---
title: Erstellen eines Anmeldenamens | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.login.status.f1
- sql13.swb.login.effectivepermissions.f1
- sql13.swb.login.general.f1
- sql13.swb.login.databaseaccess.f1
- sql13.swb.login.serverroles.f1
helpviewer_keywords:
- authentication [SQL Server], logins
- logins [SQL Server], creating
- creating logins with Management Studio
- Create login [SQL Server]
- SQL Server logins
ms.assetid: fb163e47-1546-4682-abaa-8c9494e9ddc7
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 03a4f993deace5c4714e17667b00eee99b4811a3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-login"></a>Erstellen eines Anmeldenamens
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Thema wird beschrieben, wie eine Anmeldung in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] oder [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)] erstellt wird. Ein Anmeldename ist die Identität von Personen oder Prozessen, die eine Verbindung zu einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]herstellen.  
  
##  <a name="Background"></a> Hintergrund  
 Eine Anmeldung ist ein Sicherheitsprinzipal oder eine Entität, die von einem sicheren System authentifiziert werden kann. Benutzer benötigen einen Anmeldenamen, um eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]herstellen zu können. Sie können auf Grundlage eines Windows-Prinzipals (z. B. ein Domänenbenutzer oder eine Windows-Domänengruppe) eine Anmeldung erstellen, oder Sie können eine Anmeldung erstellen, die nicht auf einem Windows-Prinzipal (z. B. eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldung) basiert.  
  
> **HINWEIS:** Für die Verwendung der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung muss [!INCLUDE[ssDE](../../../includes/ssde-md.md)] die Authentifizierung im gemischten Modus verwenden. Weitere Informationen finden Sie unter [Auswählen eines Authentifizierungsmodus](../../../relational-databases/security/choose-an-authentication-mode.md).  
  
 Als Sicherheitsprinzipale können Anmeldenamen Berechtigungen gewährt werden. Der Gültigkeitsbereich eines Anmeldenamens ist das gesamte [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Um eine bestimmte Datenbank mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zu verbinden, muss ein Anmeldename einem Datenbankbenutzer zugeordnet werden. Die Berechtigungen innerhalb der Datenbank werden dem Datenbankbenutzer, nicht dem Anmeldenamen, gewährt bzw. verweigert. Einer Anmeldung können Berechtigungen gewährt werden,bei denen der Gültigkeitsbereich die gesamte Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] abdeckt (z.B. die **CREATE ENDPOINT** -Berechtigung).  
  
> **HINWEIS:** Wenn eine Anmeldung eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herstellt, wird die Identität in der Masterdatenbank überprüft. Verwenden Sie eigenständige Datenbankbenutzer, um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] - und [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] -Verbindungen auf Datenbankebene zu authentifizieren. Eine Anmeldung ist nicht erforderlich, wenn Sie eigenständige Datenbankbenutzer verwenden. Eine eigenständige Datenbank ist eine Datenbank, die von anderen Datenbanken und der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]/[!INCLUDE[ssSDS](../../../includes/sssds-md.md)] (und der Masterdatenbank), der die Datenbank hostet, isoliert ist. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt eigenständige Datenbankbenutzer sowohl für die Windows- als auch für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung. Kombinieren Sie bei Verwendung von [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]eigenständige Datenbankbenutzer mit den Firewallregeln auf Datenbankebene. Weitere Informationen finden Sie unter [Eigenständige Datenbankbenutzer - machen Sie Ihre Datenbank portabel](../../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
##  <a name="Security"></a> Security  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erfordert die **ALTER ANY LOGIN** -Berechtigung oder die **ALTER LOGIN** -Berechtigung für den Server.  
  
 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] erfordert die Mitgliedschaft in der Rolle **loginmanager** .  
  
##  <a name="SSMSProcedure"></a> Erstellen einer Anmeldung mit SSMS  
  
  
1.  Erweitern Sie im Objekt-Explorer den Ordner der Serverinstanz, in dem Sie eine neue Anmeldung erstellen möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Sicherheit** , zeigen Sie auf **Neu**, und wählen Sie dann **Anmeldung**aus.  
  
3.  Geben Sie in das Dialogfeld **Anmeldung - Neu** auf der Seite **Allgemein** einen Benutzernamen in das Feld **Anmeldename** ein. Klicken Sie alternativ auf **Suchen** , um das Dialogfeld **Benutzer oder Gruppe auswählen** zu öffnen.  
  
     Wenn Sie auf **Suchen**klicken:  
  
    1.  Klicken Sie unter **Wählen Sie den Objekttyp aus**auf **Objekttypen** , um das Dialogfeld **Objekttypen** zu öffnen, und wählen Sie eine der folgenden Optionen aus: **Integrierte Sicherheitsprinzipale**, **Gruppen**und **Benutzer**. Die Optionen**Integrierte Sicherheitsprinzipale** und **Benutzer** sind standardmäßig ausgewählt. Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
    2.  Klicken Sie unter **Suchpfad**auf **Speicherorte** , um das Dialogfeld **Speicherorte** zu öffnen, und wählen Sie eine der verfügbaren Serverspeicherorte aus. Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
    3.  Geben Sie unter **Geben Sie die zu verwendenden Objektnamen ein (Beispiele)** den Benutzer- oder Gruppennamen ein, den Sie suchen möchten. Weitere Informationen finden Sie unter [Benutzer, Computer oder Gruppen auswählen (Dialogfeld)](http://technet.microsoft.com/library/cc771712.aspx).  
  
    4.  Klicken Sie auf **Erweitert** für erweiterte Suchoptionen. Weitere Informationen finden Sie unter [Auswählen von Benutzern, Computern oder Gruppen (Dialogfeld) – Erweitert (Seite)](http://technet.microsoft.com/library/cc733110.aspx).  
  
    5.  Klicken Sie auf **OK**.  
  
4.  Um auf Grundlage eines Windows-Prinzipals eine Anmeldung zu erstellen, wählen Sie **Windows-Authentifizierung**aus. Dies ist die Standardauswahl.  
  
5.  Um eine Anmeldung zu erstellen, die auf einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank gespeichert wird, wählen Sie **SQL Server-Authentifizierung**aus.  
  
    1.  Geben Sie im Feld **Kennwort** ein Kennwort für den neuen Benutzer ein. Geben Sie im Feld **Kennwort bestätigen** das Kennwort erneut ein.  
  
    2.  Wenn Sie ein vorhandenes Kennwort ändern, wählen Sie **Altes Kennwort angeben**aus, und geben Sie dann das alte Kennwort im Feld **Altes Kennwort** ein.  
  
    3.  Um Kennwortrichtlinienoptionen für Komplexität und Erzwingung zu erzwingen, wählen Sie **Kennwortrichtlinie erzwingen**aus. Weitere Informationen finden Sie unter [Password Policy](../../../relational-databases/security/password-policy.md). Dies ist eine Standardoption, wenn **SQL Server-Authentifizierung** ausgewählt wird.  
  
    4.  Um den Ablauf von Kennwortrichtlinienoptionen zu erzwingen, wählen Sie **Ablauf des Kennworts erzwingen**aus. **Kennwortrichtlinie erzwingen** muss ausgewählt sein, damit dieses Kontrollkästchen aktiviert werden kann. Dies ist eine Standardoption, wenn **SQL Server-Authentifizierung** ausgewählt wird.  
  
    5.  Wählen Sie **Benutzer muss das Kennwort bei der nächsten Anmeldung ändern**aus, um den Benutzer zu zwingen, nach der ersten Anmeldung ein neues Kennwort zu erstellen. Die Option**Ablauf des Kennworts erzwingen** muss ausgewählt sein, damit dieses Kontrollkästchen aktiviert werden kann. Dies ist eine Standardoption, wenn **SQL Server-Authentifizierung** ausgewählt wird.  
  
6.  Um einem eigenständigen Sicherheitszertifikat die Anmeldung zuzuordnen, wählen Sie **Zugeordnet zu Zertifikat** aus, und wählen Sie anschließend den Namen eines vorhandenen Zertifikats aus der Liste aus.  
  
7.  Um einem eigenständigen asymmetrischen Schlüssel die Anmeldung zuzuordnen, wählen Sie **Zugeordnet zu asymmetrischem Schlüssel** aus, und wählen Sie anschließend den Namen eines vorhandenen Schlüssels aus der Liste aus.  
  
8.  Um Sicherheitsanmeldeinformationen die Anmeldung zuzuordnen, aktivieren Sie das Kontrollkästchen **Zugeordnet zu Anmeldeinformationen** , und wählen Sie anschließend entweder einen vorhandenen Anmeldenamen aus der Liste aus, oder klicken Sie auf **Hinzufügen** , um einen neuen Anmeldenamen zu erstellen. Um eine Zuordnung zu Sicherheitsanmeldeinformationen aus der Anmeldung zu entfernen, wählen Sie die Anmeldeinformationen aus der Liste **Zugeordnete Anmeldeinformationen** aus, und klicken Sie auf **Entfernen**. Weitere Informationen über Anmeldenamen im Allgemeinen finden Sie unter [Anmeldeinformationen &#40;Datenbankmodul&#41;](../../../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
9. Wählen Sie eine Standarddatenbank für die Anmeldung aus der Liste **Standarddatenbank** aus. **Master** ist der Standardwert für diese Option.  
  
10. Wählen Sie eine Standardsprache für die Anmeldung aus der Liste **Standardsprache** aus.  
  
11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Zusätzliche Optionen  
 Im Dialogfeld **Anmeldung – Neu** sind auch Optionen auf vier zusätzlichen Seiten verfügbar: **Serverrollen**, **Benutzerzuordnung**, **Sicherungsfähige Elemente**und **Status**.  
  
### <a name="server-roles"></a>Serverrollen  
 Die Seite **Serverrollen** listet alle möglichen Rollen auf, die der neuen Anmeldung zugewiesen werden können. Die folgenden Optionen stehen zur Verfügung:  
  
 Kontrollkästchen**bulkadmin**   
 Mitglieder der festen Serverrolle **bulkadmin** können die BULK INSERT-Anweisung ausführen.  
  
 Kontrollkästchen**dbcreator**   
 Mitglieder der festen Serverrolle **dbcreator** können beliebige Datenbanken erstellen, ändern, löschen und wiederherstellen.  
  
 Kontrollkästchen**diskadmin**   
 Mitglieder der festen Serverrolle **diskadmin** können Datenträgerdateien verwalten.  
  
 Kontrollkästchen**processadmin**   
 Mitglieder der festen Serverrolle **processadmin** können Prozesse beenden, die in einer Instanz von [!INCLUDE[ssDE](../../../includes/ssde-md.md)]ausgeführt werden.  
  
 Kontrollkästchen**public**   
 Alle SQL Server-Benutzer, -Gruppen und -Rollen gehören standardmäßig zur festen Serverrolle **public** .  
  
 Kontrollkästchen**securityadmin**   
 Mitglieder der festen Serverrolle **securityadmin** können Anmeldungen und deren Eigenschaften verwalten. Sie verfügen für Berechtigungen auf Serverebene über die Berechtigungen GRANT, DENY und REVOKE. Sie verfügen für Berechtigungen auf Datenbankebene ebenfalls über die Berechtigungen GRANT, DENY und REVOKE. Sie können außerdem Kennwörter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldungen zurücksetzen.  
  
 Kontrollkästchen**serveradmin**   
 Mitglieder der festen Serverrolle **serveradmin** können serverweite Konfigurationsoptionen ändern und den Server herunterfahren.  
  
 Kontrollkästchen**setupadmin**   
 Mitglieder der festen Serverrolle **setupadmin** können Verbindungsserver hinzufügen und entfernen, und sie können einige gespeicherte Systemprozeduren ausführen.  
  
 Kontrollkästchen**sysadmin**   
 Mitglieder der festen Serverrolle **sysadmin** können in [!INCLUDE[ssDE](../../../includes/ssde-md.md)]beliebige Aktivitäten ausführen.  
  
### <a name="user-mapping"></a>Benutzerzuordnung  
 Die Seite **Benutzerzuordnung** listet alle möglichen Datenbanken und die Mitgliedschaften in der Datenbankrolle auf jenen Datenbanken auf, die für die Anmeldung übernommen werden können. Die ausgewählten Datenbanken bestimmen die Rollenmitgliedschaften, die für die Anmeldung verfügbar sind. Die folgenden Optionen sind auf dieser Seite verfügbar:  
  
 **Benutzer, die dieser Anmeldung zugeordnet sind**  
 Wählt die Datenbanken aus, auf die von dieser Anmeldung zugegriffen werden kann. Wenn Sie eine Datenbank auswählen, werden die gültigen Datenbankrollen im Bereich **Mitgliedschaft in Datenbankrolle für:** *Datenbankname* angezeigt.  
  
 **Karte**  
 Ermöglicht der Anmeldung den Zugriff auf die nachfolgend aufgeführten Datenbanken.  
  
 **Datenbank**  
 Führt die auf dem Server verfügbaren Datenbanken in einer Liste auf.  
  
 **Benutzer**  
 Geben Sie einen Datenbankbenutzer an, der der Anmeldung zugeordnet werden soll. Standardmäßig ist der Name des Datenbankbenutzers mit dem Anmeldenamen identisch.  
  
 **Standardschema**  
 Gibt das Standardschema des Benutzers an. Wenn ein Benutzer zum ersten Mal erstellt wird, wird als Standardschema **dbo**verwendet. Es kann auch ein Standardschema angegeben werden, das noch nicht vorhanden ist. Für Benutzer, die einer Windows-Gruppe, einem Zertifikat oder einem asymmetrischen Schlüssel zugeordnet sind, kann kein Standardschema angegeben werden.  
  
 **Gastkonto aktiviert für:**  *Datenbankname*  
 Ein Nur-Lese-Attribut, das angibt, ob das Gastkonto für die ausgewählte Datenbank aktiviert ist. Verwenden Sie die Seite **Status** des Dialogfelds **Anmeldungseigenschaften** des Gastkontos, um das Gastkonto zu aktivieren oder zu deaktivieren.  
  
 **Mitgliedschaft in Datenbankrolle für:**  *Datenbankname*  
 Wählen Sie die Rollen für den Benutzer in der angegebenen Datenbank aus. Alle Benutzer sind Mitglieder der **public** -Rolle in allen Datenbanken und können nicht entfernt werden. Weitere Informationen zu Datenbankrollen finden Sie unter [Rollen auf Datenbankebene](../../../relational-databases/security/authentication-access/database-level-roles.md).  
  
### <a name="securables"></a>Sicherungsfähige Elemente  
 Auf der Seite **Sicherungsfähige Elemente** werden alle möglichen sicherungsfähigen Elemente und die Berechtigungen für diese sicherungsfähigen Elemente aufgelistet, die für die Anmeldung gewährt werden können. Die folgenden Optionen sind auf dieser Seite verfügbar:  
  
 **Oberes Raster**  
 Enthält ein oder mehrere Elemente, für die Berechtigungen festgelegt werden können. Die im oberen Raster angezeigten Spalten variieren je nach Prinzipal oder sicherungsfähigem Element.  
  
 So fügen Sie dem oberen Raster Elemente hinzu  
  
1.  Klicken Sie auf **Suchen**.  
  
2.  Wählen Sie im Dialogfeld **Objekte hinzufügen** eine der folgenden Optionen aus: **Bestimmte Objekte...**, **Alle Objekte des Typs...** oder **The server***server_name*. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > **Hinweis:** Wenn Sie die Option **The server***server_name* auswählen, wird das obere Raster automatisch mit allen sicherungsfähigen Objekten des Servers gefüllt.  
  
3.  Bei Auswahl der Option **Bestimmte Objekte**:  
  
    1.  Klicken Sie im Dialogfeld **Objekte auswählen** unter **Wählen Sie Objekttypen aus**auf **Objekttypen**.  
  
    2.  Wählen Sie im Dialogfeld **Objekttypen auswählen** einen der folgenden Objekttypen aus: **Endpunkte**, **Anmeldungen**, **Server**, **Verfügbarkeitsgruppen**und **Serverrollen**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    3.  Klicken Sie unter **Geben Sie die Namen der auszuwählenden Objekte ein (Beispiele)** auf **Durchsuchen**.  
  
    4.  Wählen Sie im Dialogfeld **Nach Objekten suchen** eines der verfügbaren Objekte vom Typ aus, den Sie im Dialogfeld **Objekttypen auswählen** ausgewählt haben, und klicken Sie anschließend auf **OK**.  
  
    5.  Klicken Sie im Dialogfeld **Objekte auswählen** auf **OK**.  
  
4.  Wenn Sie im Dialogfeld **Objekttypen auswählen**die Option **Alle Objekte des Typs** auswählen, dann wählen Sie einen der folgenden Objekttypen aus: **Endpunkte**, **Anmeldungen**, **Server**, **Verfügbarkeitsgruppen**und **Serverrollen**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **Name**  
 Die Namen der Prinzipale oder sicherungsfähigen Elemente, die dem Raster hinzugefügt werden.  
  
 **Typ**  
 Beschreibt den Typ jedes Elements.  
  
 **Registerkarte 'Explizit'**  
 Listet die möglichen Berechtigungen für die im oberen Raster ausgewählten sicherungsfähigen Elemente auf. Für einige explizite Berechtigungen sind nicht alle Optionen verfügbar.  
  
 **Berechtigungen**  
 Der Name der Berechtigung.  
  
 **Grantor**  
 Der Prinzipal, der die Berechtigung erteilt.  
  
 **Erteilen**  
 Aktivieren Sie diese Option, um der Anmeldung diese Berechtigung zu erteilen. Deaktivieren Sie diese Option, um diese Berechtigung aufzuheben.  
  
 **Mit Erteilung**  
 Zeigt den Status der WITH GRANT-Option für die angezeigte Berechtigung an. Dieses Feld ist schreibgeschützt. Verwenden Sie die [GRANT](../../../t-sql/statements/grant-transact-sql.md) -Anweisung, um diese Berechtigung anzuwenden.  
  
 **Verweigern**  
 Aktivieren Sie diese Option, um der Anmeldung diese Berechtigung zu verweigern. Deaktivieren Sie diese Option, um diese Berechtigung aufzuheben.  
  
### <a name="status"></a>Status  
 Die Seite **Status** enthält einige Authentifizierungs- und Autorisierungsoptionen, die auf der ausgewählten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldung konfiguriert werden können.  
  
 Die folgenden Optionen sind auf dieser Seite verfügbar:  
  
 **Serverzugriff**  
 Wenn Sie diese Einstellung verwenden, müssen Sie die ausgewählte Anmeldung als einen Prinzipal betrachten, dem für das sicherungsfähige Element Berechtigungen erteilt oder verweigert werden können.  
  
 Wählen Sie **Erteilen** aus, um der Anmeldung die CONNECT SQL-Berechtigung zu erteilen. Wählen Sie **Verweigern** aus, um der Anmeldung die CONNECT SQL-Berechtigung zu verweigern.  
  
 **Anmeldename**  
 Wenn Sie diese Einstellung verwenden, muss der ausgewählte Anmeldename als Datensatz in einer Tabelle betrachtet werden. Änderungen an den hier aufgeführten Werten werden auf den Datensatz angewendet.  
  
 Ein deaktivierter Anmeldename bleibt weiterhin als Datensatz bestehen. Beim Herstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]wird der Anmeldename jedoch nicht authentifiziert.  
  
 Wählen Sie diese Option aus, um diesen Anmeldenamen zu aktivieren oder zu deaktivieren. Für diese Option wird die ALTER LOGIN-Anweisung mit der Option ENABLE oder DISABLE verwendet.  
  
 **SQL Server Authentication**  
 Das Kontrollkästchen **Anmeldung ist gesperrt** ist nur verfügbar, wenn der ausgewählte Anmeldename die Verbindung mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Authentifizierung herstellt, und wenn der Anmeldename gesperrt ist. Diese Einstellung ist schreibgeschützt. Führen Sie ALTER LOGIN mit der Option UNLOCK aus, wenn Sie die Sperre für eine Anmeldung aufheben möchten.  
  
##  <a name="TsqlProcedure"></a> Erstellen einer Anmeldung mit Windows-Authentifizierung über T-SQL  
  
 
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Create a login for SQL Server by specifying a server name and a Windows domain account name.  
  
    CREATE LOGIN [<domainName>\<loginName>] FROM WINDOWS;  
    GO  
  
    ```  
  
## <a name="create-a-login-using-sql-server-authentication-with-ssms"></a>Erstellen einer Anmeldung mit SQL Server-Authentifizierung mit SSMS  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Creates the user "shcooper" for SQL Server using the security credential "RestrictedFaculty"   
    -- The user login starts with the password "Baz1nga," but that password must be changed after the first login.  
  
    CREATE LOGIN shcooper   
       WITH PASSWORD = 'Baz1nga' MUST_CHANGE,  
       CREDENTIAL = RestrictedFaculty;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md).  
  
##  <a name="FollowUp"></a> Nachverfolgung: Erforderliche Schritte nach Erstellen eines Anmeldenamens  
 Nach der Erstellung eines Anmeldenamens kann dieser zwar eine Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]herstellen, er verfügt jedoch nicht unbedingt über ausreichende Berechtigungen, um damit sinnvolle Aufgaben ausführen zu können. Die folgende Liste enthält Links zu häufigen Anmeldeaktionen.  
  
-   Informationen darüber, wie ein Anmeldename einer Datenbankrolle beitreten kann, finden Sie unter [Verknüpfen einer Rolle](../../../relational-databases/security/authentication-access/join-a-role.md).  
  
-   Informationen zum Autorisieren eines Anmeldenamens für die Verwendung einer Datenbank finden Sie unter [Erstellen eines Datenbankbenutzers](../../../relational-databases/security/authentication-access/create-a-database-user.md).  
  
-   Informationen zum Erteilen einer Berechtigung für einen Anmeldenamen finden Sie unter [Erteilen einer Berechtigung für einen Prinzipal](../../../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
