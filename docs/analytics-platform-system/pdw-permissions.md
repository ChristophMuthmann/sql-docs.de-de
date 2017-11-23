---
title: PDW-Berechtigungen (SQLServer PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e271980-bec8-424b-9f68-cea11b4e64e8
caps.latest.revision: "23"
ms.openlocfilehash: 135081344fd5eafcf6130d5e251ca5cf34c00434
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="pdw-permissions"></a>PDW-Berechtigungen
Dieses Thema beschreibt die Anforderungen und Optionen für die Verwaltung von Datenbankberechtigungen für SQL Server PDW.  
  
## <a name="BackupRestoreBasics"></a>Grundlagen der Datenbank-Engine-Berechtigung  
Berechtigungen für das Datenbankmodul auf SQL Server PDW werden auf Serverebene über Anmeldungen, und klicken Sie auf der Datenbankebene über Datenbankbenutzer und benutzerdefinierte Datenbankrollen verwaltet.  
  
**Anmeldungen**  
Anmeldungen sind einzelne Benutzerkonten für die Anmeldung an SQL Server-PDW. SQL Server PDW unterstützt Anmeldungen mithilfe der Windows-Authentifizierung und SQL Server-Authentifizierung.  Anmeldenamen für die Windows-Authentifizierung kann Windows-Benutzer oder Windows-Gruppen aus beliebigen Domänen, die vom SQL Server PDW als vertrauenswürdig eingestuft wird. SQL Server-Authentifizierung Anmeldungen definiert und von SQL Server PDW authentifiziert werden und müssen erstellt werden, indem Sie ein Kennwort angeben.  
  
Mitglieder der **Sysadmin** festen Serverrolle (z. B. die **sa** Anmeldung) können mit einer Datenbank verbinden, ohne Sie zu einem Datenbankbenutzer zugeordnet werden. Zugeordnet sind, die **Dbo** Benutzer. Der Besitzer der Datenbank als auch zugeordnet ist die **Dbo** Benutzer.  
  
**Serverrollen**  
Es gibt vier spezielle Serverrollen eine Gruppe vorkonfigurierter Rollen, die geeigneten Gruppe von Berechtigungen auf Serverebene bereitstellen. Die **Sysadmin**, **MediumRC**, **LargeRC**, und **XLargeRCfixed** Serverrollen sind die einzige Server-Rollen, die derzeit in SQL implementiert PDW-Server. Die **sa** Anmeldung ist das einzige Mitglied der **Sysadmin** feste Serverrolle, und zusätzliche Anmeldungen können nicht hinzugefügt werden die **Sysadmin** Rolle. Anmeldenamen, gewährt die **CONTROL SERVER** Berechtigung, die ähnlich, jedoch nicht identisch sein, um die **Sysadmin** festen Serverrolle. Verwendung [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) zum Hinzufügen von Mitgliedern zu den anderen Serverrollen. Benutzerdefinierte Serverrollen werden von SQL Server PDW nicht unterstützt.  
  
**Datenbankbenutzer**  
Anmeldungen werden Zugriff auf eine Datenbank gewährt, indem in einer Datenbank einen Datenbankbenutzer erstellt und dieser Datenbankbenutzer einer einer Anmeldung zugeordnet. Der Datenbank-Benutzername ist in der Regel identisch mit dem Anmeldenamen, obwohl dies nicht so sein muss. Jeder Datenbankbenutzer ist einer einzelnen Anmeldung zugeordnet. Eine Anmeldung kann nur einem Benutzer in einer Datenbank zugeordnet werden, kann aber als Datenbankbenutzer in mehreren unterschiedlichen Datenbanken zugeordnet werden.  
  
**Feste Datenbankrollen**  
Feste Datenbankrollen sind eine Gruppe vorkonfigurierter Rollen, die geeigneten Gruppe von Berechtigungen auf Datenbankebene bereitzustellen. Datenbankbenutzer und benutzerdefinierte Datenbankrollen können mithilfe von festen Datenbankrollen hinzugefügt werden die [Sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) Prozedur. Weitere Informationen zu festen Datenbankrollen finden Sie unter [fester Datenbankrollen](#fixed-database-roles).  
  
**Benutzerdefinierte Datenbankrollen**  
Benutzer mit der **CREATE ROLE** Berechtigung kann neue benutzerdefinierte Datenbankrollen um Gruppen von Benutzern mit gemeinsamen Berechtigungen abzubilden erstellen. In der Regel werden Berechtigungen der gesamten Rolle erteilt oder verweigert, was die Verwaltung und Überwachung von Berechtigungen vereinfacht.  
  
Berechtigungen werden Sicherheitsprinzipalen (Anmeldungen, Benutzer und Rollen) mithilfe von gewährt der **GRANT** Anweisung. Berechtigungen explizit verweigert werden, mithilfe der **DENY** Befehl. Entfernt eine zuvor erteilte oder verweigerte Berechtigung mithilfe der **widerrufen** Anweisung. Berechtigungen sind kumulativ, was heißt, dass der Benutzer alle Berechtigungen erhält, die dem Benutzer, der Anmeldung oder den Gruppe erteilt wurden, denen der Benutzer angehört. Durch jedwede Berechtigungsverweigerung werden alle erteilten Berechtigungen außer Kraft gesetzt. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
Das folgende Beispiel zeigt eine allgemeine und empfohlene Methode zum Konfigurieren von Berechtigungen.  
  
1.  Wenn Windows-Authentifizierung verwenden, erstellen Sie einen Anmeldenamen für jeden Windows-Benutzer oder die Windows-Gruppe, die mit SQL Server PDW verbunden werden. Wenn Sie SQL Server-Authentifizierung verwenden zu können, erstellen Sie einen Anmeldenamen für jede Person, die mit SQL Server PDW verbunden werden.  
  
2.  Für jede Anmeldung einen Datenbankbenutzer in allen erforderlichen Datenbanken zu erstellen.  
  
3.  Erstellen Sie eine oder mehrere benutzerdefinierte Datenbankrollen, jeweils eine ähnliche Funktion darstellen. Beispiele: Finanzanalyst und Vertriebsanalyst.  
  
4.  Fügen Sie eine oder mehrere benutzerdefinierte Datenbankrollen Datenbankbenutzer hinzu.  
  
5.  Erteilen Sie den benutzerdefinierten Datenbankrollen Berechtigungen.  
  
Anmeldungen sind Objekte auf Serverebene und können durch Anzeigen aufgelistet werden [Sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Nur die Berechtigungen auf Serverebene können Serverprinzipale gewährt werden.  
  
Benutzer und Datenbankrollen sind Objekte auf Datenbankebene und können durch Anzeigen aufgelistet werden [Sys. database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Datenbankprinzipale können nur Berechtigungen auf Datenbankebene gewährt werden.  
  
## <a name="BackupTypes"></a>Standardberechtigungen  
Die folgende Liste beschreibt die Standardberechtigungen an:  
  
-   Erstellung ein Anmeldenamens von using-Direktiven **CREATE LOGIN** -Anweisung, die Anmeldung empfängt die **CONNECT SQL** Berechtigung der Anmeldung zur Verbindung mit SQL Server-PDW.  
  
-   Wenn ein Datenbankbenutzer erstellt wird, mithilfe der **CREATE USER** -Anweisung, die der Benutzer erhält die **CONNECT ON DATABASE::***< Database_name >* Berechtigung, ermöglicht die Melden Sie sich mit dieser Datenbank als Benutzer herstellen.  
  
-   Alle Prinzipale, einschließlich der Rolle "PUBLIC" haben keine expliziten oder impliziten Berechtigungen standardmäßig, da die expliziten Berechtigungen und implizite Berechtigungen geerbt werden. Daher, wenn keine explizite Berechtigungen vorhanden sind, treten auch möglicherweise keine implizite Berechtigungen.  
  
-   Wenn ein Anmeldename, der Besitzer eines Objekts oder einer Datenbank wird, verfügt die Anmeldung immer alle Berechtigungen für das Objekt oder die Datenbank. Die Besitzerrechte sind nicht als explizite Berechtigungen sichtbar. Die **GRANT**, **widerrufen**, und **DENY** Anweisungen haben keinen Einfluss auf den von Besitzberechtigungen. Besitz kann geändert werden, indem die [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) Anweisung.  
  
-   Die Anmeldenamens "sa" verfügt über alle Berechtigungen auf dem Gerät. Ähnlich wie bei Besitzerrechte die sa-Berechtigungen können nicht geändert werden und sind nicht sichtbar ist, als explizite Berechtigungen. Die **GRANT**, **widerrufen**, und **DENY** Anweisungen wirken sich nicht für sa-Berechtigungen.  
  
-   Die Serverrolle PUBLIC erhält keine Berechtigungen standardmäßig und keine Berechtigungen aus anderen Serverrollen erbt. Die Serverrolle PUBLIC mit explizite Berechtigungen gewährt werden kann die **GRANT**, **widerrufen**, und **DENY** Anweisungen.  
  
-   Transaktionen sind keine Berechtigungen erforderlich. Alle Prinzipale Ausführungsdauer der **BEGIN TRANSACTION**, **COMMIT**, und **ROLLBACK** Transaktionsbefehle. Ein Prinzipal muss jedoch die entsprechenden Berechtigungen zum Ausführen jeder Anweisung innerhalb der Transaktion haben.  
  
-   Die **verwenden** Anweisung erfordert keine Berechtigungen. Alle Prinzipale Ausführungsdauer der **verwenden** Anweisung für jede Datenbank jedoch den Zugriff auf eine Datenbank sie einen Benutzerprinzipal in der Datenbank benötigen oder der Guest-Benutzer aktiviert sein muss.  
  
### <a name="the-public-role"></a>Die PUBLIC-Rolle  
Alle neuen Appliance Anmeldungen gehören automatisch an die PUBLIC-Rolle. Die Serverrolle PUBLIC weist folgende Merkmale auf:  
  
-   Die Serverrolle PUBLIC verfügt über keine Berechtigungen in der Standardeinstellung.  
  
-   Alle Prinzipale sind Mitglieder der Serverrolle PUBLIC, und die PUBLIC-Serverrolle ist nicht Mitglied einer anderen Serverrolle.  
  
-   Implizite Berechtigungen kann nicht der Serverrolle PUBLIC geerbt werden. Alle Berechtigungen, die PUBLIC-Rolle müssen explizit erteilt werden.  
  
## <a name="BackupProc"></a>Festlegen von Berechtigungen  
Fest, ob eine Anmeldung über die Berechtigung zum Ausführen einer bestimmten Aktion hat, hängt von den Berechtigungen erteilt oder verweigert, Anmeldenamen, Benutzer und Rollen, denen der Benutzer Mitglied ist ab. Berechtigungen auf Serverebene (z. B. **CREATE LOGIN** und **VIEW SERVER STATE**) auf Serverebene Prinzipalen (Anmeldenamen) verfügbar sind. Berechtigungen auf Datenbankebene (z. B. **wählen** aus einer Tabelle oder **EXECUTE** für eine Prozedur) auf Datenbankebene Prinzipale (Benutzer und Rollen) verfügbar sind.  
  
### <a name="implicit-and-explicit-permissions"></a>Implizite und explizite Berechtigungen  
Ein *explizite Berechtigung* ist ein **GRANT** oder **DENY** Berechtigung erhält, die einem Prinzipal durch eine **GRANT** oder **DENY**Anweisung. Auf Datenbankebene Berechtigungen sind aufgeführt, der [database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) anzeigen. Berechtigungen auf Serverebene sind aufgeführt, der [server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) anzeigen.  
  
Ein *implizite Berechtigung* ist ein **GRANT** oder **DENY** Berechtigung, die ein Prinzipal (Anmeldename oder eine Serverrolle) geerbt hat. Eine Berechtigung kann auf folgende Weise geerbt werden.  
  
-   Ein Prinzipal kann eine Berechtigung aus einer Rolle erben, wenn der Prinzipal ein Mitglied der Rolle ist, selbst wenn der Prinzipal eine explizite keinen **GRANT** oder **DENY** Berechtigung.  
  
-   Ein Prinzipal kann eine Berechtigung für ein untergeordnetes Objekt (z. B. eine Tabelle) erben, wenn der Prinzipal eine Berechtigung für eines der Objekte übergeordnete Bereiche (z. B. das Schema der Tabelle oder die Berechtigung für die gesamte Datenbank) verfügt.  
  
-   Ein Prinzipal kann eine Berechtigung erben, durch die Verwendung einer Berechtigung, die eine untergeordnete Berechtigung enthält. Z. B. die **ALTER ANY USER** Berechtigung enthält sowohl die **CREATE USER** und **ALTER ON USER::**  *<name>*  Berechtigungen.  
  
### <a name="determining-permissions-when-performing-actions"></a>Festlegen von Berechtigungen beim Ausführen von Aktionen  
Der Prozess der bestimmen, welche Berechtigung zuweisen, die einem Prinzipal komplex ist. Die Komplexität tritt auf, wenn implizite Berechtigungen bestimmen, da Prinzipale können Mitglied mehrerer Rollen und Berechtigungen über mehrere Ebenen in der Hierarchie Rolle übergeben werden können.  
  
Die folgende Liste beschreibt die allgemeinen Regeln für das Festlegen von Berechtigungen:  
  
-   Ownership impliziert-Berechtigung.  
  
    Ein Objektbesitzer verfügt über alle Berechtigungen für das Objekt. Ein Datenbankbesitzer verfügt ebenso alle Berechtigungen für die Datenbank und alle Berechtigungen für die Objekte in der Datenbank. Diese Berechtigungen können nicht geändert werden.  
  
-   Berechtigungen können über mehrere Ebenen in der Hierarchie der serverrollenmitgliedschaften geerbt werden.  
  
    Nehmen Sie beispielsweise an, dass Sie die folgende Situation verfügen:  
  
    -   David Anmeldung ist Mitglied der Datenbankrolle PerfAnalysts.  
  
    -   PerfAnalysts ist Mitglied der Datenbankrolle "Produktion".  
  
    -   "David" sowie PerfAnalysts verfügen über keine **wählen** -Berechtigung für die Customer-Tabelle. Die Berechtigung wurde widerrufen oder nie explizit erteilt.  
  
    -   Produktion **wählen** -Berechtigung für die Customer-Tabelle.  
  
    In diesem Fall übernimmt PerfAnalysts **GRANT** -Berechtigung für die Customer-Tabelle aus Produktions- und David erben **GRANT** -Berechtigung für die Customer-Tabelle aus der Produktion.  
  
-   **DENY** überschreibt **GRANT** Wenn Berechtigungen in Konflikt stehen.  
  
    Nehmen wir beispielsweise an, die Anmeldung David verfügt über keine Berechtigungen für die Customer-Tabelle und ist Mitglied der beiden Datenbankrollen – dbgroup1, besitzt **DENY** -Berechtigung für die Customer-Tabelle und dbgroup2, besitzt **GRANT** Berechtigung für die Customer-Tabelle. In diesem Fall David erben die **DENY** -Berechtigung für die Customer-Tabelle. Dies ist der Fall, ob die Rollen ihrer Berechtigungen explizit oder implizit erhalten.  
  
### <a name="auditing-permissions"></a>Überwachung von Berechtigungen  
Überprüfen Sie die Berechtigungen eines Benutzers zum Recherchieren Folgendes.  
  
-   Führen Sie die folgende Abfrage aus, um zu bestimmen, welche Anmeldungen Systemadministratoren sind.  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   Führen Sie die folgende Abfrage aus, um zu bestimmen, welche Anmeldungen explizite Berechtigungen gewährt wurden.  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   Führen Sie die folgende Abfrage in einer Benutzerdatenbank aus, um zu bestimmen, welche Datenbankbenutzer Mitglied einer Datenbankrolle sind.  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   Führen Sie die folgende Abfrage in einer Benutzerdatenbank aus, um zu bestimmen, welche Datenbankbenutzern und Rollen erteilt oder bestimmte Berechtigungen verweigert wurde. Sie müssen zusätzliche Abfrageansichten z. B. sys.objects und sys.schemas, um die Elemente beschrieben, mit der Major_id zu identifizieren.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>Best Practices für Datenbanken Berechtigungen  
  
-   Erteilen von Berechtigungen die unterste Ebene, der möglich ist. Erteilen von Berechtigungen auf der Tabelle oder Sicht Berechtigungsstufe können verwaltet werden. Erteilen von Berechtigungen auf Datenbankebene konnte aber werden zu einschränkend sein. Wenn die Datenbank mit Schemas arbeiten Grenzen definiert konzipiert ist, ist das Erteilen von Berechtigungen für das Schema vielleicht einen geeigneten Kompromiss zwischen der Tabellenebene und Datenbankebene.  
  
-   Erteilen Sie Berechtigungen für Rollen statt für Benutzer oder Anmeldenamen ein. Verwalten von Berechtigungen mithilfe von Rollen, sodass Benutzer nicht ganz einfach schnell gewähren oder widerrufen einen Satz von Berechtigungen für einen Benutzer oder eine Anmeldung durch Verschieben in oder aus der Rolle. Wenn eine Funktion von einer Person zu einem anderen übertragen werden, können Berechtigungen auf Rollenebene während der Rolle mitgliedschaftsänderungen intakt bleiben.  
  
-   Erteilen Sie Berechtigungen für Rollen basierend auf den Auftragsfunktion und auf höherer Ebene Gruppe Rollen, die die Funktion tätigkeitsrollen auf Grundlage der Unternehmens-Gruppe, die die Aktionen zu kombinieren.  
  
-   Jeder Benutzer sollte einen eindeutigen Benutzernamen verfügen. Dürfen Sie Benutzer keine Anmeldungen freigeben. Eine Anmeldung für jeden Benutzer bereitgestellt wird sichergestellt, dass einen Audit-Trail, und vereinfacht die berechtigungsverwaltung.  
  
## <a name="fixed-database-roles"></a>Feste Datenbankrollen
SQL Server bietet vorkonfiguriert, dass (feste) auf Datenbankebene-Rollen können Sie die Berechtigungen auf einem Server verwalten. Die vorkonfigurierten Rollen werden so repariert, dass Sie nicht die Berechtigungen, die ihnen zugewiesene ändern können. Benutzerdefinierte Datenbankrollen können auch erstellt werden. Sie können die Berechtigungen für eine benutzerdefinierte Datenbankrollen ändern.  
  
Rollen sind Sicherheitsprinzipale, in denen andere Prinzipale gruppieren. Datenbankrollen werden der gesamten Datenbank im Geltungsbereich der Berechtigungen. Datenbankbenutzer und anderen Datenbankrollen können als Mitglieder der Datenbankrollen hinzugefügt werden. Die festen Datenbankrollen können nicht miteinander hinzugefügt werden. (*Rollen* entsprechen den *Gruppen* im Betriebssystem Windows.)  
  
Es gibt 9 festen Datenbankrollen.  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>Berechtigungen der festen Datenbankrollen  
Das System von festen Serverrollen und feste Datenbankrollen ist ein Legacysystem in der die Prüfung stammt. Feste Rollen werden weiterhin unterstützt und sind hilfreich in Umgebungen, in denen wenige Benutzer vorhanden sind und die sicherheitsanforderungen sind einfach. Ab SQL Server 2005 wurde eine ausführlichere System gewähren der Berechtigung erstellt. Dieses neue System ist eine detailliertere bietet viele weitere Optionen für erteilen und Verweigern von Berechtigungen. Die zusätzliche Komplexität des Systems präziseren erschwert es um zu erfahren, aber die meisten Unternehmenssysteme sollten anstelle der festen Rollen Berechtigungen gewähren. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->Das folgende Diagramm zeigt die Berechtigungen, die jeder festen Datenbankrolle zugeordnet sind. Alle Berechtigungen in dieser SQL Server-Grafik sind nicht verfügbar (oder notwendig) in APS.  
  
![APS-Sicherheit, die festen Datenbankrollen](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>Verwandte Inhalte  
  
-   Zum Erstellen von benutzerdefinierten Rollen finden Sie unter [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md).  
  
  
## <a name="fixed-server-roles"></a>Feste Serverrollen
Feste Serverrollen werden von SQL Server automatisch erstellt. SQL Server PDW ist eine eingeschränkte Implementierung von SQL Server, die festen Serverrollen. Nur die **Sysadmin** und **öffentlichen** Benutzeranmeldenamen als Mitglieder haben. Die **Setupadmin** und **Dbcreator** Rollen werden von SQL Server PDW intern verwendet. Zusätzliche Member können nicht hinzugefügt oder aus keiner Rolle entfernt werden.  
  
### <a name="sysadmin-fixed-server-role"></a>Sysadmin feste Serverrolle  
Mitglieder der festen Serverrolle **sysadmin** können alle Aktivitäten auf dem Server ausführen. Die **sa** Anmeldung ist das einzige Mitglied der **Sysadmin** festen Serverrolle "". Zusätzliche Anmeldungen können nicht hinzugefügt werden, um die **Sysadmin** festen Serverrolle "". Erteilen der **CONTROL SERVER** Berechtigung entspricht in etwa die Mitgliedschaft in der **Sysadmin** festen Serverrolle "". Im folgenden Beispiel wird die **CONTROL SERVER** Berechtigung für einen Anmeldenamen mit dem Namen Fay.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> Die **CONTROL SERVER** Berechtigung ermöglicht nahezu vollständige Kontrolle über SQL Server PDW. Wann immer möglich, geben Sie stattdessen spezifischere Berechtigungen zu Anmeldungen auf. Betrachten Sie beispielsweise das Gewähren der **VIEW SERVER STATE**, **ALTER ANY LOGIN**, **VIEW ANY DATABASE**, oder **CREATE ANY DATABASE** Berechtigungen.  
  
### <a name="public-server-role"></a>Serverrolle Public  
Jede Anmeldung, die eine Verbindung, in SQL Server PDW herstellen kann ist ein Mitglied der **öffentlichen** -Serverrolle. Alle Anmeldungen erben die Berechtigungen für **öffentlichen** für jedes Objekt. Weisen Sie nur **öffentlichen** Berechtigungen für ein Objekt, wenn das Objekt für alle Benutzer verfügbar sein soll. Sie können nicht geändert, Mitgliedschaft in der **öffentlichen** Rolle.  
  
> [!NOTE]  
> **Öffentliche** wird anders implementiert als andere Rollen. Da alle Serverprinzipale Member von öffentlichen, die Mitgliedschaft sind die **öffentlichen** Rolle ist nicht aufgeführt, der **Sys. server_role_members** DMV.  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>Feste Serverrollen im Vergleich zu Erteilen von Berechtigungen  
Das System von festen Serverrollen und feste Datenbankrollen ist ein Legacysystem in der die Prüfung stammt. Feste Rollen werden weiterhin unterstützt und sind hilfreich in Umgebungen, in denen wenige Benutzer vorhanden sind und die sicherheitsanforderungen sind einfach. Ab SQL Server 2005 wurde eine ausführlichere System gewähren der Berechtigung erstellt. Dieses neue System ist eine detailliertere bietet viele weitere Optionen für erteilen und Verweigern von Berechtigungen. Die zusätzliche Komplexität des Systems präziseren erschwert es um zu erfahren, aber die meisten Unternehmenssysteme sollten anstelle der festen Rollen Berechtigungen gewähren. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>Verwandte Themen  
  
- [Erteilen von Berechtigungen](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

