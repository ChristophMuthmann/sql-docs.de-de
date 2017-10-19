---
title: Installieren von SQLServer Reporting Services | Microsoft Docs
ms.date: 10/10/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 52c2f8fae79884b025e067b7d628cd3154ba93f4
ms.openlocfilehash: 5ce83ff18d6908441a3eaaf05599068ec5876308
ms.contentlocale: de-de
ms.lasthandoff: 10/10/2017

---
# <a name="install-sql-server-reporting-services"></a>Installieren von SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

SQL Server Reporting Services-Installation umfasst Serverkomponenten zum Speichern von Berichtselementen, Rendern von Berichten und Verarbeiten von Abonnements sowie anderen Berichtsdiensten.  Informationen Sie zum Installieren von Power BI-Berichtsserver.

Um Reporting Services in SQL Server 2017 herunterzuladen, wechseln Sie zu der [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55252).

> [!NOTE]
> Suchen Sie für Power BI-Berichtsserver? Finden Sie unter [Installieren des Berichtsservers für Power BI](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).

## <a name="before-you-begin"></a>Vorbereitungen

Überprüfen Sie vor der Installation von Reporting Services die [Hardware und Software-Anforderungen für die Installation von SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).

## <a name="install-your-report-server"></a>Installieren Sie den Berichtsserver

Installieren einen Berichtsserver ist unkompliziert. Es gibt nur wenige Schritte, um die Dateien zu installieren.

> [!NOTE]
> Sie können einen SQL Server-Datenbankmodul-Server zur Verfügung, die zum Zeitpunkt der Installation ist nicht erforderlich. Sie benötigen eine Reporting Services nach der Installation konfiguriert werden.

1. Bestimmen Sie den Speicherort der SQLServerReportingServices.exe, und starten Sie den Installer.

2. Wählen Sie **Installieren von Reporting Services**.

    ![Installieren von Reporting Services](media/install-reporting-services/report-server-install.png)

3. Wählen Sie eine Version zu installieren, und wählen Sie dann **Weiter**.

    ![Wählen Sie die edition](media/install-reporting-services/report-server-install-edition.png)

    Sie können unten Evaluation- oder Developer Edition aus der Dropdownliste auswählen.

    ![Evaluation und Developer-Editionen](media/install-reporting-services/report-server-install-edition-select.png)

    Andernfalls können Sie einen Product Key eingeben.

4. Lesen und akzeptieren Sie die Lizenzbedingungen und die Bedingungen, und wählen Sie dann **Weiter**.

5. Sie benötigen ein Datenbankmodul zum Speichern der Berichtsserver-Datenbank zur Verfügung. Wählen Sie **Weiter** , nur für den Berichtsserver installieren.

    ![Datenbank nicht für die Installation erforderlich.](media/install-reporting-services/report-server-install-db-engine.png)

6. Geben Sie den Installationsspeicherort für den Berichtsserver. Wählen Sie **installieren** um den Vorgang fortzusetzen.

    ![Installationspfad angeben](media/install-reporting-services/report-server-install-file-path.png)

    > [!NOTE]
    > Der Standardpfad lautet c:\Programme\Microsoft c:\Programme\Microsoft SQL Server Reporting Services.

7. Wählen Sie nach einer erfolgreichen Installation **Berichtsserver konfigurieren** um den Reporting Services-Konfigurations-Manager zu starten.

    ![Konfigurieren des Berichtsservers](media/install-reporting-services/report-server-install-configure.png)

## <a name="configuration-your-report-server"></a>Konfiguration der Berichtsserver

Nach der Auswahl **Berichtsserver konfigurieren** im Setup, werden Sie angezeigt mit **Report Server-Konfigurations-Manager**. Weitere Informationen finden Sie unter [Report Server-Konfigurations-Manager](reporting-services-configuration-manager-native-mode.md).

Sie müssen [erstellen eine Berichtsserver-Datenbank](ssrs-report-server-create-a-report-server-database.md) zum Abschließen der ersten Konfiguration von Reporting Services. Ein SQL Server-Datenbankserver ist erforderlich, um diesen Schritt abzuschließen.

### <a name="creating-a-database-on-a-different-server"></a>Erstellen einer Datenbank auf einem anderen server

Wenn Sie die Berichtsserver-Datenbank auf einem Datenbankserver auf einem anderen Computer erstellen, müssen Sie das Dienstkonto für den Berichtsserver zu Anmeldeinformationen zu ändern, die auf dem Datenbankserver erkannt wird.

Standardmäßig verwendet der Berichtsserver die virtuelles Dienstkonto an. Wenn Sie versuchen, eine Datenbank auf einem anderen Server zu erstellen, wird möglicherweise den folgenden Fehler anwenden Verbindung Rechte Schritt angezeigt.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

Um diesen Fehler zu umgehen, können Sie das Dienstkonto Netzwerkdienst oder ein Domänenkonto ändern. Ändern das Dienstkonto Netzwerkdienst gilt Rechte im Kontext des Computerkontos für den Berichtsserver.

Weitere Informationen finden Sie unter [Konfigurieren der Berichtsserver-Dienstkontos](configure-the-report-server-service-account-ssrs-configuration-manager.md).

## <a name="windows-service"></a>Windows-Dienst

Ein Windows-Dienst wird als Teil der Installation erstellt. Es wird als angezeigt **SQL Server Reporting Services**. Der Name des **SQLServerReportingServices**.

## <a name="default-url-reservations"></a>Standard-URL-Reservierungen

URL-Reservierungen bestehen aus Präfix, Hostname, Port und virtuellem Verzeichnis:

|Teil|Description|
|----------|-----------------|
|Präfix|Das Standardpräfix ist http. Wenn Sie zuvor eine Secure Sockets Layer (SSL)-Zertifikat installiert, versucht Setup, URL-Reservierungen erstellen, die das HTTPS-Präfix verwenden.|
|Hostname|Der Standardhostname ist ein Platzhalter (+). Es gibt an, dass der Berichtsserver jede HTTP-Anforderung auf dem dafür bestimmten Port für jeden Hostnamen akzeptiert, die den Computer, einschließlich `http://<computername>/reportserver`, `http://localhost/reportserver`, oder`http://<IPAddress>/reportserver.`|
|Port|Der Standardport ist 80. Wenn Sie einen anderen Port als Port 80 verwenden, müssen Sie explizit an die URL hinzufügen, wenn Sie eine Web-Portal in einem Browserfenster öffnen.|
|Virtuelles Verzeichnis|Standardmäßig werden virtuelle Verzeichnisse in das Format der Berichtsserver für die Berichtsserver-Webdienst und die Berichte für das Webportal erstellt. Beim Berichtsserver-Webdienst lautet der Standardname für das virtuelle Verzeichnis **reportserver**. Für das Webportal wird das standardmäßige virtuelle Verzeichnis **Berichte**.|

Ein Beispiel für die vollständige URL-Zeichenfolge könnte folgendermaßen aussehen:

- `http://+:80/reportserver`, ermöglicht den Zugriff auf dem Berichtsserver her.

- `http://+:80/reports`, ermöglicht den Zugriff auf das Webportal.

## <a name="firewall"></a>Firewall

Wenn Sie von einem Remotecomputer aus auf den Berichtsserver zugreifen möchten Sie stellen Sie sicher, dass Sie Firewallregeln konfiguriert haben, wenn eine vorhanden Firewall.

Sie müssen den TCP-Port zu öffnen, die Sie für Ihre Webdienst-URL und die Webportal-URL konfiguriert haben. Standardmäßig werden diese auf TCP-Port 80 konfiguriert.

## <a name="additional-configuration"></a>Zusätzliche Konfiguration

- Um die Integration in Power BI-Dienst konfigurieren, damit Sie Berichtselemente an ein Power BI-Dashboard anheften können, finden Sie unter [in Power BI-Dienst integrieren](power-bi-report-server-integration-configuration-manager.md).

- Um e-Mail für die abonnementverarbeitung konfigurieren, finden Sie unter [e-Mail-Einstellungen](e-mail-settings-reporting-services-native-mode-configuration-manager.md) und [e-Mail-Übermittlung auf einem Berichtsserver](../subscriptions/e-mail-delivery-in-reporting-services.md).

- Um das Webportal zu konfigurieren, damit Sie darauf zugreifen können, auf einem Remotecomputer anzeigen und Verwalten von Berichten finden Sie [Konfigurieren einer Firewall für den berichtsserverzugriff](../report-server/configure-a-firewall-for-report-server-access.md) und [Konfigurieren eines Berichtsservers für die Remoteverwaltung](../report-server/configure-a-report-server-for-remote-administration.md) .

## <a name="related-information"></a>Verwandte Informationen

Informationen zum Installieren von SQL Server 2016 Reporting Services im einheitlichen Modus finden Sie unter [Installieren von Reporting Services im einheitlichen Modus-Berichtsserver](install-reporting-services-native-mode-report-server.md). Informationen zum Installieren von SQL Server 2016 Reporting Services im integrierten SharePoint-Modus finden Sie unter [Installieren des ersten Berichtsservers im SharePoint-Modus](install-the-first-report-server-in-sharepoint-mode.md).

## <a name="next-steps"></a>Nächste Schritte

Beginnen Sie mit dem Berichtsserver installiert Berichte zu erstellen und diese auf den Berichtsserver bereitstellen. Informationen zum Starten mit Berichts-Generator finden Sie unter [installieren Sie Berichts-Generator](../../reporting-services/install-windows/install-report-builder.md).

Zum Erstellen von Berichten, die mit SQL Server-Datentools [Herunterladen von SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714).

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
