---
title: Installieren von SQL Server Reporting Services | Microsoft-Dokumentation
ms.date: 10/10/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: 3cc3d78c22bbb4b32696692074e2dad2d6809a3a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="install-sql-server-reporting-services"></a>Installieren von SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

Die Installation von SQL Server Reporting Services umfasst Serverkomponenten zum Speichern von Berichtselementen, Rendern von Berichten und Verarbeiten von Abonnements sowie anderen Berichtsdiensten.  Erfahren Sie, wie Sie Power BI-Berichtsserver installieren.

Laden Sie SQL Server 2017 Reporting Services im [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55252) herunter.

> [!NOTE]
> Interessieren Sie sich für Power BI-Berichtsserver? Weitere Informationen finden Sie unter [Install Power BI Report Server (Installieren von Power BI-Berichtsserver)](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).

## <a name="before-you-begin"></a>Vorbereitungen

Prüfen Sie vor der Installation von Reporting Services [Hardware and software requirements for installing SQL Server (Hardware- und Softwareanforderungen für die Installation von SQL Server)](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).

## <a name="install-your-report-server"></a>Installieren Ihres Berichtsservers

Die Installation des Berichtsservers ist unkompliziert. Zum Installieren der Dateien müssen nur wenige Schritte ausgeführt werden.

> [!NOTE]
> Während der Installation muss kein Server für ein SQL Server-Datenbankmodul verfügbar sein. Allerdings benötigen Sie einen verfügbaren Server zur Konfiguration von Reporting Services nach der Installation.

1. Suchen Sie nach dem Speicherort von „SQLServerReportingServices.exe“, und starten Sie das Installationsprogramm.

2. Klicken Sie auf **Reporting Services installieren**.

    ![Installieren von Reporting Services](media/install-reporting-services/report-server-install.png)

3. Wählen Sie eine Edition aus, die Sie installieren möchten, und klicken Sie auf **Weiter**.

    ![Edition auswählen](media/install-reporting-services/report-server-install-edition.png)

    In der Dropdownliste können Sie zwischen den Editionen „Evaluation“ und „Developer“ wählen.

    ![Die Editionen „Evaluation“ und „Developer“](media/install-reporting-services/report-server-install-edition-select.png)

    Ansonsten können Sie auch einen Product Key eingeben.

4. Lesen und akzeptieren Sie die Lizenzbedingungen sowie sonstige weitere Bedingungen, und klicken Sie anschließend auf **Weiter**.

5. Zum Speichern der Berichtsserver-Datenbank muss ein Datenbankmodul verfügbar sein. Klicken Sie auf **Weiter**, um nur den Berichtsserver zu installieren.

    ![Für die Installation wird keine Datenbank benötigt.](media/install-reporting-services/report-server-install-db-engine.png)

6. Geben Sie den Installationsort für den Berichtsserver an. Klicken Sie auf **Installieren**, um den Vorgang fortzusetzen.

    ![Installationspfad angeben](media/install-reporting-services/report-server-install-file-path.png)

    > [!NOTE]
    > Der Standardpfad lautet C:\Program Files\Microsoft SQL Server Reporting Services.

7. Klicken Sie nach dem erfolgreichen Setup auf **Berichtsserver konfigurieren**, um Konfigurations-Manager für Reporting Services zu starten.

    ![Konfigurieren des Berichtsservers](media/install-reporting-services/report-server-install-configure.png)

## <a name="configuration-your-report-server"></a>Konfigurieren Ihres Berichtsservers

Wenn Sie beim Setup auf **Berichtsserver konfigurieren** klicken, wird der **Konfigurations-Manager für Reporting Services** angezeigt. Weitere Informationen finden Sie unter [Report Server Configuration Manager (Konfigurations-Manager des Berichtsservers)](reporting-services-configuration-manager-native-mode.md).

Sie müssen eine [Berichtsserver-Datenbank erstellen](ssrs-report-server-create-a-report-server-database.md), um die erste Konfiguration von Reporting Services abzuschließen. Sie benötigen einen SQL Server-Datenbankserver, um diesen Schritt abzuschließen.

### <a name="creating-a-database-on-a-different-server"></a>Erstellen einer Datenbank auf einem anderen Server

Wenn Sie die Berichtsserver-Datenbank auf einem anderen Datenbankserver auf einem anderen Computer erstellen, müssen Sie die Anmeldeinformationen für das Dienstkonto für den Berichtsserver ändern, sodass diese vom Datenbankserver erkannt werden.

Standardmäßig verwendet der Berichtsserver das virtuelle Dienstkonto. Wenn Sie versuchen, eine Datenbank auf einem anderen Server zu erstellen, wird möglicherweise der folgende Fehler im Schritt „Anwenden von Verbindungsrechten“ ausgelöst:

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

Sie können das Dienstkonto entweder in „Netzwerkdienst“ oder „Domänenkonto“ ändern, um den Fehler zu umgehen. Wenn das Dienstkonto in „Netzwerkdienst“ geändert wird, werden im Kontext des Computerkontos die Rechte für den Berichtsserver übernommen.

Weitere Informationen finden Sie unter [Configure the report server service account (Konfigurieren des Dienstkontos für den Berichtsserver)](configure-the-report-server-service-account-ssrs-configuration-manager.md).

## <a name="windows-service"></a>Windows-Dienst

Als Teil der Installation wird ein Windows-Dienst erstellt. Dieser Dienst wird als **SQL Server Reporting Services** angezeigt. Der Name des Dienstes lautet **SQLServerReportingServices**.

## <a name="default-url-reservations"></a>Standard-URL-Reservierungen

URL-Reservierungen bestehen aus Präfix, Hostname, Port und virtuellem Verzeichnis:

|Teil|Description|
|----------|-----------------|
|Präfix|Das Standardpräfix ist http. Wenn Sie zuvor ein SSL-Zertifikat (Secure Sockets Layer) installiert haben, versucht das Setup, die URL-Reservierungen mit dem Präfix HTTPS zu erstellen.|
|Hostname|Der Standardhostname ist ein Platzhalter (+). Dieses gibt an, dass der Berichtsserver eine beliebige HTTP-Anforderung an den angegebenen Port für einen beliebigen Hostnamen akzeptiert, der für den Computer steht, einschließlich `http://<computername>/reportserver`, `http://localhost/reportserver` oder `http://<IPAddress>/reportserver.`.|
|Port|Der Standardport ist 80. Wenn Sie einen anderen Port als Port 80 verwenden, müssen Sie diesen explizit der URL hinzufügen, wenn Sie ein Webportal in einem Browserfenster öffnen.|
|Virtuelles Verzeichnis|Standardmäßig werden virtuelle Verzeichnisse im Format „ReportServer“ für den Berichtsserver-Webdienst und im Format „Reports“ für das Webportal erstellt. Beim Berichtsserver-Webdienst lautet der Standardname für das virtuelle Verzeichnis **reportserver**. Für das Webportal ist **reports** das virtuelle Standardverzeichnis.|

Ein Beispiel für die vollständige URL-Zeichenfolge könnte folgendermaßen aussehen:

- `http://+:80/reportserver` bietet Zugriff auf den Berichtsserver.

- `http://+:80/reports` bietet Zugriff auf das Webportal.

## <a name="firewall"></a>Firewall

Wenn Sie von einem Remotecomputer auf den Berichtsserver zugreifen, sollten Sie sicherstellen, dass Firewallregeln konfiguriert sind, wenn es eine Firewall gibt.

Sie müssen den TCP-Port öffnen, den Sie für die URLs Ihres Webdienstes und Ihres Webportals konfiguriert haben. Standardmäßig werden diese auf dem TCP-Port 80 konfiguriert.

## <a name="additional-configuration"></a>Zusätzliche Konfiguration

- Informationen zum Konfigurieren der Integration in den Power BI-Dienst finden Sie unter [Integrate with the Power BI service (Integration in den Power BI-Dienst)](power-bi-report-server-integration-configuration-manager.md). Dort erfahren Sie, wie Sie Berichtselemente an das Power BI-Dashboard heften können.

- Informationen zum Konfigurieren von E-Mails für Abonnementverarbeitungen finden Sie unter [E-Mail settings (E-Mail-Einstellungen)](e-mail-settings-reporting-services-native-mode-configuration-manager.md) und [E-Mail delivery in a report server (Übermitteln von E-Mails an einen Berichtsserver)](../subscriptions/e-mail-delivery-in-reporting-services.md).

- Informationen zum Konfigurieren des Webportals für das Abrufen und Verwalten von Berichten von einem Remotecomputer finden Sie unter [Configure a firewall for report server access (Konfigurieren einer Firewall zum Zugriff auf den Berichtsserver)](../report-server/configure-a-firewall-for-report-server-access.md) und [Configure a report server for remote administration (Konfigurieren eines Berichtsservers zur Remoteverwaltung)](../report-server/configure-a-report-server-for-remote-administration.md).

## <a name="related-information"></a>Verwandte Informationen

Informationen zur Installation von SQL Server 2016 Reporting Services im einheitlichen Modus finden Sie unter [Install Reporting Services native mode report server (Installieren des Reporting Services-Berichtsservers im einheitlichen Modus)](install-reporting-services-native-mode-report-server.md). Informationen zur Installation von SQL Server 2016 Reporting Services im SharePoint-Integrationsmodus finden Sie unter [Install the first Report Server in SharePoint mode (Installieren des ersten Berichtsservers im SharePoint-Modus)](install-the-first-report-server-in-sharepoint-mode.md).

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie den Berichtsserver installiert haben, beginnen Sie mit dem Erstellen von Berichten, und stellen Sie diese anschließend für ihren Berichtsserver bereit. Informationen zum Starten des Berichts-Generators finden Sie unter [Install Report Builder (Installieren des Berichts-Generators)](../../reporting-services/install-windows/install-report-builder.md).

[Laden Sie SQL Server Data Tools herunter](http://go.microsoft.com/fwlink/?LinkID=616714), um Berichte mithilfe von SQL Server Data Tools zu erstellen.

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
