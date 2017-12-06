---
title: Problembehandlung bei Server- und Datenbankverbindungsproblemen mit Reporting Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/28/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8bbb88df-72fd-4c27-91b7-b255afedd345
caps.latest.revision: "6"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 5dd30097deb23e911e43789e10e81685f1ce0743
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="troubleshoot-server-and-database-connection-problems-with-reporting-services"></a>Problembehandlung bei Server- und Datenbankverbindungsproblemen mit Reporting Services
Verwenden Sie dieses Thema, um Probleme zu behandeln, die beim Herstellen einer Verbindung mit einem Berichtsserver auftreten. In diesem Thema werden außerdem Informationen zu "Unerwartete Fehler"-Meldungen bereitgestellt. Weitere Informationen zum Konfigurieren von Datenquellen und Konfigurieren von Verbindungsinformationen des Berichtsservers finden Sie unter [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) und [Konfigurieren einer Berichtsserver-Datenbankverbindung (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="cannot-create-a-connection-to-data-source-datasourcename-rserroropeningconnection"></a>Es kann keine Verbindung mit der 'datasourcename'-Datenquelle hergestellt werden. (rsErrorOpeningConnection)  
Dies ist eine generischer Fehler, der auftritt, wenn vom Berichtsserver keine Verbindung mit einer externen Datenquelle hergestellt werden kann, die Daten für einen Bericht bereitstellt. Dieser Fehler wird mit einer zweiten Fehlermeldung angezeigt, in der die zugrunde liegende Ursache angegeben wird. Bei **rsErrorOpeningConnection**können die folgenden weiteren Fehler angezeigt werden.  
  
### <a name="login-failed-for-user-username"></a>Fehler bei der Anmeldung für den Benutzer 'UserName'  
Der Benutzer verfügt nicht über Berechtigungen zum Zugreifen auf die Datenquelle. Überprüfen Sie, ob der Benutzer über einen gültigen Benutzeranmeldenamen für die Datenbank verfügt, wenn Sie eine SQL Server-Datenbank verwenden. Weitere Informationen zum Erstellen eines Datenbankbenutzers oder einer SQL Server-Anmeldung finden Sie unter [Erstellen eines Datenbankbenutzers](../../relational-databases/security/authentication-access/create-a-database-user.md) und [Erstellen einer SQL Server-Anmeldung](../../relational-databases/security/authentication-access/create-a-login.md).  
  
### <a name="login-failed-for-user-nt-authorityanonymous-logon"></a>Fehler bei der Anmeldung für den Benutzer 'NT AUTHORITY\ANONYMOUS LOGON'  
Dieser Fehler tritt auf, wenn Anmeldeinformationen über mehrere Computerverbindungen weitergeleitet werden. Wenn Sie die Windows-Authentifizierung verwenden und das Kerberos-Protokoll, Version 5, nicht aktiviert ist, tritt dieser Fehler auf, wenn Anmeldeinformationen über mehr als eine Computerverbindung weitergeleitet werden. Verwenden Sie gespeicherte Anmeldeinformationen, oder fordern Sie die Benutzer zur Eingabe ihrer Anmeldeinformationen auf, um diesen Fehler zu umgehen. Weitere Informationen zur Problemumgehung finden Sie unter [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
### <a name="an-error-has-occurred-while-establishing-a-connection-to-the-server"></a>Fehler beim Herstellen einer Verbindung mit dem Server.  
Beim Herstellen einer Verbindung mit SQL Server kann dieser Fehler durch den Umstand verursacht werden, dass die Standardeinstellungen von SQL Server keine Remoteverbindungen zulassen. (Anbieter: Named Pipes-Anbieter, Fehler: 40 – Es konnte keine Verbindung mit SQL Server hergestellt werden). Dieser Fehler wird von der Instanz des Datenbankmoduls zurückgegeben, das die Berichtsserver-Datenbank hostet. In den meisten Fällen tritt dieser Fehler auf, weil der SQL Server-Dienst beendet wird. Wenn Sie SQL Server Express with Advanced Services oder eine benannte Instanz verwenden, tritt dieser Fehler auf, wenn die Berichtsserver-URL oder die Verbindungszeichenfolge für die Berichtsserver-Datenbank falsch ist. Gehen Sie wie folgt vor, um diese Probleme zu beheben:  
  
* Überprüfen Sie, ob der SQL Server-Dienst (**MSSQLSERVER**) gestartet wurde. Klicken Sie auf dem Computer, der die Instanz des Datenbankmoduls hostet, auf „Start“, klicken Sie auf „Verwaltung“, klicken Sie auf „Dienste“, und führen Sie einen Bildlauf zu „SQL Server“ (**MSSQLSERVER**) durch. Wenn der Dienst nicht gestartet wurde, klicken Sie mit der rechten Maustaste auf den Dienst, wählen Sie „Eigenschaften“, wählen Sie unter „Starttyp“ die Option „Automatisch“, klicken Sie auf „Übernehmen“, klicken Sie auf „Start“, und klicken Sie dann auf „OK“.   
* Überprüfen Sie, ob die Berichtsserver-URL und die Verbindungszeichenfolge für die Berichtsserver-Datenbank richtig sind. Wenn Reporting Services oder das Datenbankmodul als benannte Instanz installiert wurde, beinhaltet die bei der Installation erstellte Standard-Verbindungszeichenfolge den Instanznamen. Wenn Sie z. B. eine Standardinstanz von SQL Server Express with Advanced Services auf einem Server mit dem Namen DEVSRV01 installiert haben, lautet die Berichts-Manager-URL „DEVSRV01\Reports$SQLEXPRESS“. Außerdem lautet der Datenbank-Servername in der Verbindungszeichenfolge ähnlich wie DEVSRV01\SQLEXPRESS. Weitere Informationen über URLs und Datenquellen-Verbindungszeichenfolgen für SQL Server Express finden Sie unter [Reporting Services in SQL Server Express with Advanced Services](http://technet.microsoft.com/library/ms365166(v=sql.105).aspx). Starten Sie zum Überprüfen der Verbindungszeichenfolge für die Berichtsserver-Datenbank das Reporting Services-Konfigurationstool, und überprüfen Sie die Seite „Setup der Datenbank“.  
  
### <a name="a-connection-cannot-be-made-ensure-that-the-server-is-running"></a>Es kann keine Verbindung hergestellt werden. Stellen Sie sicher, dass der Server ausgeführt wird.  
Dieser Fehler wird vom ADOMD.NET-Anbieter zurückgegeben. Es gibt verschiedene Gründe für das Auftreten dieses Fehlers. Wenn Sie den Server als "localhost" angegeben haben, versuchen Sie, stattdessen den Servernamen anzugeben. Dieser Fehler kann auch auftreten, wenn der neuen Verbindung kein Arbeitsspeicher zugeordnet werden kann. Weitere Informationen finden Sie unter [Knowledge Base-Artikel 912017 – Fehlermeldung beim Herstellen einer Verbindung mit einer Instanz von SQL Server 2005 Analysis Services](http://support.microsoft.com/kb/912017).  
  
Wenn die Fehlermeldung auch "Der angegebene Host ist unbekannt." enthält, ist dies ein Hinweis darauf, dass der Analysis Services-Server nicht verfügbar ist oder die Verbindung ablehnt. Möglicherweise müssen Sie den SQL Server-Browserdienst ausführen, um die von dieser Instanz verwendete Portnummer abzurufen, wenn der Analysis Services-Server als eine benannte Instanz auf einem Remotecomputer installiert ist.  
  
### <a name="report-services-soap-proxy-source"></a>(SOAP-Proxyquelle für Berichtsdienste)  
Wenn dieser Fehler bei der Berichtsmodellgenerierung auftritt und der Abschnitt mit zusätzlichen Informationen den Text "SQL Server ist nicht vorhanden, oder der Zugriff wurde verweigert" enthält, trifft möglicherweise eine der folgenden Bedingungen zu:  
* Die Verbindungszeichenfolge für die Datenquelle enthält „localhost“.  
* TCP/IP ist für den SQL Server-Dienst deaktiviert.  
  
Um diesen Fehler zu beheben, können Sie entweder die Verbindungszeichenfolge so ändern, dass der Servername verwendet wird, oder Sie können TCP/IP für den Dienst aktivieren. Befolgen Sie diese Schritte, um TCP/IP zu aktivieren:  
  
1. Starten Sie den SQL Server-Konfigurations-Manager.  
2. Erweitern Sie **SQL Server-Netzwerkkonfiguration**.  
3. Wählen Sie **Protokolle für MSSQLSERVER**aus.  
4. Klicken Sie mit der rechten Maustaste auf **TCP/IP**, und wählen Sie dann **Aktivieren**aus.  
5. Wählen Sie **SQL Server-Dienste**aus.  
6. Klicken Sie mit der rechten Maustaste auf **SQL Server (MSSQLSERVER)**, und wählen Sie dann **Neu starten**aus.  
  
## <a name="wmi-error-when-connecting-to-a-report-server-in-management-studio"></a>WMI-Fehler beim Herstellen einer Verbindung mit einem Berichtsserver in Management Studio  
Standardmäßig verwendet Management Studio den Reporting Services-WMI-Anbieter (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation), um eine Verbindung mit dem Berichtsserver herzustellen. Wenn der WMI-Anbieter nicht ordnungsgemäß installiert ist, tritt beim Versuch, eine Verbindung mit dem Berichtsserver herzustellen, der folgende Fehler auf:  
  
Es kann keine Verbindung mit \<dem Namen Ihres Servers> hergestellt werden. Der WMI-Anbieter für Berichtsdienste ist nicht installiert oder falsch konfiguriert (Microsoft.SqlServer.Management.UI.RSClient).  
  
Um diesen Fehler zu beheben, sollten Sie die Software neu installieren. In allen anderen Fällen können Sie das Problem zeitweilig umgehen, indem Sie über den SOAP-Endpunkt eine Verbindung mit dem Berichtsserver herstellen:  
  
* Geben Sie in Management Studio im Dialogfeld **Verbindung mit Server herstellen** unter **Servername**die URL des Berichtsservers ein. Die Standardeinstellung ist `http://<your server name>/reportserver`. Wenn Sie SQL Server 2008 Express with Advanced Services verwenden, ist die Standardeinstellung `http://<your server name>/reportserver$sqlexpress`.  
  
Um den Fehler zu beheben, damit Sie über den WMI-Anbieter eine Verbindung herstellen können, führen Sie das Installationsprogramm aus, um Reporting Services zu reparieren oder neu zu installieren.  
  
## <a name="connection-error-where-login-failed-due-to-unknown-user-name-or-bad-password"></a>Verbindungsfehler, wobei die Anmeldung aufgrund eines unbekannten Benutzernamens oder ungültigen Kennworts einen Fehler erzeugt hat  
Ein **rsReportServerDatabaseLogonFailed** -Fehler kann auftreten, wenn Sie ein Domänenkonto für die Verbindung vom Berichtsserver zur Berichtsserver-Datenbankverbindung verwenden und das Kennwort des Domänenkontos geändert wurde.   
  
Der vollständige Fehlertext lautet: "Der Berichtsserver kann keine Verbindung mit der Berichtsserver-Datenbank herstellen. Fehler bei der Anmeldung (**rsReportServerDatabaseLogonFailed**). Anmeldefehler: unbekannter Benutzername oder falsches Kennwort."  
  
Wenn Sie das Kennwort zurücksetzen, muss die Verbindung aktualisiert werden. Weitere Informationen finden Sie unter [Konfigurieren einer Berichtsserver-Datenbankverbindung (SSRS-Konfigurations-Manager)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="the-report-server-cannot-open-a-connection-to-the-report-server-database-rsreportserverdatabaseunavailable"></a>Der Berichtsserver kann keine Verbindung mit der Berichtsserver-Datenbank herstellen. (rsReportServerDatabaseUnavailable).  
Vollständige Meldung: Der Berichtsserver kann keine Verbindung mit der Berichtsserver-Datenbank herstellen. Für jede Anforderung und Verarbeitung ist eine Verbindung mit der Datenbank erforderlich. (rsReportServerDatabaseUnavailable)  
Dieser Fehler tritt auf, wenn vom Berichtsserver keine Verbindung mit der relationalen SQL Server-Datenbank hergestellt werden kann, die als interner Speicher für den Server dient. Die Verbindung mit der Berichtsserver-Datenbank wird über das Reporting Services-Konfigurationstool verwaltet. Sie können das Tool ausführen, zur Seite Setup der Datenbank wechseln und die Verbindungsinformationen korrigieren. Es ist eine bewährte Methode, die Verbindungsinformationen mithilfe dieses Tools zu aktualisieren. Mit diesem Tool wird sichergestellt, dass abhängige Einstellungen aktualisiert und Dienste neu gestartet werden. Weitere Informationen finden Sie unter [Konfigurieren einer Berichtsserver-Datenbankverbindung](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md) und [Konfigurieren des Berichtsserver-Dienstkontos](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
Dieser Fehler kann auch auftreten, wenn die Datenbankmodul-Instanz, von der die Berichtsserver-Datenbank gehostet wird, nicht für Remoteverbindungen konfiguriert ist. In einigen Editionen von SQL Server sind Remoteverbindungen standardmäßig aktiviert. Führen Sie das SQL Server-Konfigurations-Manager-Tool aus, um zu überprüfen, ob sie bei der von Ihnen verwendeten SQL Server-Datenbankmodulinstanz aktiviert sind. Sie müssen sowohl TCP/IP als auch Named Pipes aktivieren. Ein Berichtsserver verwendet beide Protokolle. Anweisungen zum Aktivieren von Remoteverbindungen finden Sie unter „Konfigurieren von Remoteverbindungen für die Berichtsserver-Datenbank“ im Abschnitt [Konfigurieren eines Berichtsservers für die Remoteverwaltung](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  
  
Wenn die Fehlermeldung folgenden zusätzlichen Text enthält, ist das Kennwort für das zum Ausführen der Datenbankmodulinstanz verwendete Konto abgelaufen: „Fehler beim Herstellen einer Verbindung mit dem Server. Beim Herstellen einer Verbindung mit SQL Server kann dieser Fehler durch den Umstand verursacht werden, dass die Standardeinstellungen von SQL Server keine Remoteverbindungen zulassen. (**Anbieter: SQL Server Network Interfaces, Fehler: 26 – Fehler beim Suchen des angegebenen Servers oder der angegebenen Instanz)**.“ Setzen Sie das Kennwort zurück, um diesen Fehler zu beheben:   
  
## <a name="rpc-server-is-not-listening"></a>"Der RPC-Server ist nicht in Wartestellung"  
Der Berichtsserverdienst verwendet für einige Vorgänge Remoteprozeduraufruf-Server (RPC). Wenn der Fehler "Der RPC-Server ist nicht in Wartestellung" auftritt, überprüfen Sie, ob der Berichtsserverdienst ausgeführt wird.  
  
## <a name="unexpected-error-general-network-error"></a>Unerwarteter Fehler (Allgemeiner Netzwerkfehler)  
Diese Fehlermeldung verweist auf ein Problem bei der Datenquellenverbindung. Sie sollten die Verbindungszeichenfolge prüfen und sicherstellen, dass Sie über die Zugriffsberechtigung für die Datenquelle verfügen. Wenn Sie die Windows-Authentifizierung für den Zugriff auf eine Datenquelle verwenden, benötigen Sie die Zugriffsberechtigung für den Computer, der als Host für die Datenquelle dient.  
  
## <a name="unable-to-grant-database-access-in-sharepoint-central-administration"></a>Gewähren des Datenbankzugriffs in SharePoint-Zentraladministration nicht möglich  
Wenn Sie Reporting Services für die Integration mit einem SharePoint-Produkt oder mit einer -Technologie unter Windows Vista oder Windows Server 2008 konfiguriert haben, erhalten Sie möglicherweise die folgende Fehlermeldung, wenn Sie versuchen, Zugriff auf die Seite **Datenbankzugriff gewähren** in der SharePoint-Zentraladministration zu gewähren: „Verbindung zum Computer kann nicht hergestellt werden.“  
  
Dies geschieht, weil die Benutzerkontensteuerung in Windows Vista und Windows Server 2008 eine explizite Akzeptanz durch einen Administrator für die Erhöhung und Nutzung des Administratortokens bei der Durchführung von Aufgaben erfordert, die Administratorberechtigungen benötigen. In diesem Fall kann der Windows SharePoint Services-Verwaltungsdienst nicht erhöht werden, um dem Reporting Services-Dienstkonto oder den Konten Zugriff auf die SharePoint-Konfiguration und -Inhaltsdatenbanken zu gewähren.  
  
In SQL Server 2008 Reporting Services erfordert nur das Berichtsserver-Dienstkonto Datenbankzugriff. In SQL Server 2005 Reporting Services SP2 erfordern sowohl das Windows-Dienstkonto als auch das Webdienstkonto des Berichtsservers Datenbankzugriff. Weitere Informationen zum Berichtsserver-Dienstkonto in SQL Server 2008 finden Sie unter „Dienstkonto“ (Reporting Services-Konfiguration).  
  
Es gibt zwei Lösungen für dieses Problem:   
1.  In einer Lösung können Sie die Benutzerkontensteuerung temporär deaktivieren und die SharePoint-Zentraladministration nutzen, um den Zugriff zu gewähren.  
> [!IMPORTANT]  
> Gehen Sie bei der Deaktivierung der Benutzerkontensteuerung zur Behebung dieses Problems mit Bedacht vor, und aktivieren Sie die Benutzerkontensteuerung umgehend wieder, nachdem Sie in der SharePoint-Zentraladministration den Datenbankzugriff gewährt haben. Wenn Sie die Benutzerkontensteuerung nicht deaktivieren möchten, nutzen Sie die zweite Lösung, die in diesem Abschnitt angegeben wird. Weitere Informationen über die Benutzerkontensteuerung finden Sie in der Produktdokumentation.  
2. In der zweiten Problemumgehung können Sie Datenbankzugriff auf das Reporting Services-Dienstkonto (bzw. die Reporting Services-Dienstkonten) manuell gewähren. Sie können das folgende Verfahren verwenden, um Zugang zu gewähren, indem Sie das Reporting Services-Dienstkonto (bzw. die Reporting Services-Dienstkonten) zur richtigen Windows-Gruppe und den richtigen Datenbankrollen hinzufügen. Dieses Verfahren gilt für das Berichtsserver-Dienstkonto in SQL Server 2008 Reporting Services. Wenn Sie SQL Server 2005 Reporting Services ausführen, führen Sie das Verfahren für das Windows-Dienstkonto und das Webdienstkonto des Berichtsservers durch.   
  
### <a name="to-manually-grant-database-access"></a>So gewähren Sie manuell Datenbankzugriff  
  
1. Fügen Sie das Berichtsserver-Dienstkonto der Windows-Gruppe WSS_WPG Windows auf dem Reporting Services-Computer hinzu.  
2. Stellen Sie eine Verbindung mit der Datenbankinstanz her, auf der sich die SharePoint-Konfiguration und -Inhaltsdatenbanken befinden, und erstellen Sie eine SQL-Datenbankanmeldung für das Berichtsserver-Dienstkonto.  
3. Fügen Sie die SQL-Datenbankanmeldung den folgenden Datenbankrollen hinzu:  
  
* db_owner-Rolle in der WSS-Inhaltsdatenbank  
* WSS_Content_Application_Pools-Rolle in der Datenbank SharePoint_Config  
  
## <a name="unable-to-connect-to-the-reports-and-reportserver-directories-when-the-report-server-databases-are-created-on-a-virtual-sql-server-that-runs-in-a-microsoft-cluster-services-mscs-cluster"></a>Die Verbindung mit den Verzeichnissen /reports und /reportserver ist nicht möglich, wenn die Berichtsserverdatenbanken auf einem virtuellen SQL Server erstellt werden, der auf einem MSCS-Cluster (Microsoft-Clusterdienste) ausgeführt wird.  
Wenn Sie die Berichtsserverdatenbanken **ReportServer** und **ReportServerTempDB**auf einem virtuellen SQL Server erstellen, der in einem MSCS-Cluster ausgeführt wird, wird der Remotename im Format `<domain>\<computer_name>$` möglicherweise nicht als Anmeldung auf dem SQL Server registriert. Wenn Sie das Berichtsserver-Dienstkonto als ein Konto konfiguriert haben, das diesen Remotenamen für Verbindungen erfordert, können Benutzer keine Verbindung mit den Verzeichnissen „/reports“ und „/reportserver“ in Reporting Services herstellen. Zum Beispiel erfordert das integrierte Windows-Konto NetworkService diesen Remotenamen. Um dieses Problem zu vermeiden, verwenden Sie ein explizites Domänenkonto oder eine SQL Server-Anmeldung, um eine Verbindung mit den Berichtsserverdatenbanken herzustellen.  
    
  ## <a name="see-also"></a>Siehe auch  
[Browserunterstützung für Reporting Services und Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[Fehler und Ereignisse (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Behandlung von Problemen beim Abrufen von Daten in Reporting Services-Berichten](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Behandlung von Problemen bei Abonnements und Übermittlung in Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]

