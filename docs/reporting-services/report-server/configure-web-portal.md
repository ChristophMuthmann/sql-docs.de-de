---
title: Konfigurieren Sie das Webportal | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- the web portal [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c0c6cc27711140e96bbf4420e8de596af53ddfcd
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="configure-the-web-portal"></a>Konfigurieren Sie das Webportal

die Web-Portal ist eine Web-front-End-Anwendung verwendet, um Berichte anzeigen, berichtsserverinhalt verwalten und gewähren von Benutzerzugriff auf einem Berichtsserver im einheitlichen Modus. die Web-Portal ist mit der Berichtsserver-Webdienst in derselben Berichtsserverinstanz installiert und kann konfiguriert werden, wenn Sie die Option der **in der Standardkonfiguration im einheitlichen Modus installieren** Option von Setup. Sie können auch im Web-Portal als Task nach der Installation konfigurieren. Dieses Thema enthält Informationen über die folgenden Web-Portal-Konfiguration-Szenarien:

## <a name="prerequisites"></a>Erforderliche Komponenten

Um das Webportal verwenden zu können, müssen die folgenden Voraussetzungen erfüllt sein:

- Sie müssen einen minimal konfigurierten Berichtsserver haben. Weitere Informationen zur minimalen Konfiguration von einem Berichtsserver finden Sie unter [Konfigurieren eines Berichtsservers](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md).

- Der Berichtsserver muss im einheitlichen Modus ausgeführt werden. Verwenden des Webportals mit einem Berichtsserver, der so konfiguriert ist, kann nicht für den integrierten SharePoint-Modus. In SQL Server 2012 kann ein Berichtsserver nicht von einem Modus in den anderen wechseln. Wenn Sie den von der Umgebung verwendeten Berichtsservertyp ändern möchten, müssen Sie den gewünschten Berichtsservermodus installieren und dann die Berichtselemente vom alten Berichtsserver zum neuen Berichtsserver kopieren oder verschieben. Dieser Prozess wird in der Regel als "Migration" bezeichnet. Die für das Migrieren erforderlichen Schritte hängen vom Modus ab, zu dem Sie migrieren, und von der Version, von der Sie migrieren. Weitere Informationen finden Sie unter [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).

- Darüber hinaus benötigen Sie Internet Explorer 11 oder höher mit aktivierter Skripterstellung. Weitere Informationen finden Sie unter [Browserunterstützung für Reporting Services und Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).

## <a name="configure-the-web-portal-to-use-the-default-url"></a>Konfigurieren Sie im Web-Portal, um die Standard-URL zu verwenden.

Die Web-Portal ist eine Webanwendung, die Benutzer in einem Webbrowser zugreifen. Sie müssen auf jeden Fall die URL definieren, die verwendet wird, um die Anwendung in einem Browserfenster zu öffnen. Die URL besteht aus einem Hostnamen, einem Port und einem virtuellem Verzeichnis. Zu den Standardwerten für diese URL gehören der Wert für den Hostnamen und der Wert für den Port, die Sie für die URL des Berichtsserver-Webdiensts definiert haben, sowie der Name des virtuellen Verzeichnisses **reports** . Bei einer benannten Instanz ist das virtuelle Verzeichnis **reports_instance**, wobei **instance** dem Namen der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz entspricht.

In der Standardeinstellung die das Webportal URL besteht aus eindeutigen Verzeichnisnamen, sowie dem Port und Hostname, für die Berichtsserver-Webdienst definiert ist, die in der gleichen Instanz ausgeführt wird. In den meisten Fällen handelt es sich bei dem Hostnamen um den Netzwerknamen des Berichtsservercomputers, aber es kann sich auch im eine IP-Adresse oder einen Hostheader handeln, der den Computer auflöst. Verwenden Sie zum Konfigurieren von Web-Portal, um die Standard-URL verwenden die **Webportal-URL** auf der Seite der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool.

> [!TIP]
> Wenn Sie versuchen, Zugriff auf das Webportal auf einem Remotecomputer befindet, und Sie in Ihrem Browser Meldungen zu Verbindungsfehlern erhalten, ist eine häufige Ursache Firewall-Einstellungen. Anweisungen finden Sie unter [Konfigurieren einer Firewall für den Zugriff auf den Berichtsserver](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).

#### <a name="to-configure-the-default-the-web-portal-url-and-virtual-directory"></a>So konfigurieren Sie die Standardeinstellung im Webportal-URL und eines virtuellen Verzeichnisses

1. Starten Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, und stellen Sie eine Verbindung mit der Berichtsserverinstanz her.

2. In der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, select **Webportal-URL** auf der Seite zum Konfigurieren der URL zu öffnen.

3. Geben Sie einen eindeutigen Namen virtuellen Verzeichnisses für das Webportal.

4. Klicken Sie auf **Anwenden**.

5. Bei Verwendung von [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] oder Windows Server 2008, zusätzliche Schritte möglicherweise erforderlich sein, bevor Sie das Web-Portal verwenden können. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für die lokale Verwaltung &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).

## <a name="configure-the-web-portal-to-use-a-specific-report-server-url"></a>Konfigurieren Sie die Webportal so eine bestimmte Berichtsserver-URL verwendet

Standardmäßig verbindet sich im Web-Portal mit der Berichtsserver-Webdienst, der in der gleichen Berichtsserver-Dienst ausgeführt wird. Das Webportal verwendet die Berichtsserver-Webdienst-URL zum Herstellen die Verbindung. Wenn Sie mehrere URLs für den Berichtsserver-Webdienst definieren, verwendet das Webportal das letzte Lesezeichen, das Sie definiert. Allerdings für einige Bereitstellungen empfiehlt im Web-Portal für die Verbindung immer den Webdienst über eine statische URL. Dies kann z. B. der Fall sein, wenn Sie für einen bestimmten Port oder eine bestimmte IP-Adresse die Paketfilterung konfiguriert haben und alle Verbindungen mit dem Berichtsserver die definierten Filterregeln passieren sollen.

Beim Konfigurieren von URLs in der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, im Webportal erkennt und verwendet automatisch neue und aktualisierte URLs für den Berichtsserver, der in der gleichen Serverinstanz ausgeführt wird. Wenn Ihre Bereitstellung die Verwendung einer einzelnen, statischen URL für alle Berichtsserveranforderungen erfordert, können Sie diese URL in der Datei RSReportServer.config angeben.

#### <a name="to-configure-a-static-report-server-url"></a>So konfigurieren Sie eine statische Berichtsserver-URL

1. Öffnen Sie die Datei **RSReportServer.config** in einem Text-Editor. Standardmäßig befindet sich im Ordner \Programme\Microsoft SQL Server\MSRS12. \< *Instancename*> \reporting.  

2. Suchen Sie **ReportServerURL**.

3. Ersetzen Sie die URL durch die URL der Berichtsserverinstanz.

4. Speichern Sie die Änderungen, und schließen Sie die Datei.

Weitere Informationen zum Bearbeiten von Konfigurationsdateien finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) und [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).

## <a name="customize-styles-or-application-title"></a>Anpassen von Formaten und Anwendungstitel

Sie können ein benutzerdefiniertes markenpaket zum Ändern der Farben für das Webportal erstellen. Weitere Informationen finden Sie unter [Branding des Webportals](../branding-the-web-portal.md)

#### <a name="to-modify-application-title"></a>So ändern Sie den Anwendungstitel

1. Melden Sie sich mit einem Konto an, dem auf dem Berichtsserver **Systemadministrator** -Berechtigungen zugewiesen sind.

2. Öffnen Sie Internet Explorer.

3. Geben Sie im Webportal URL. Standardmäßig lautet sie http://\<**Server Name-Ihrer-**> / Reports, aber wenn Sie Reporting Services als eine benannte Instanz, die Standard-URL installiert ist http:// be\<**Server Name-Ihrer-**> / reports\<**_instancename**>.

4. Wählen Sie **Siteeinstellungen**aus.

5. Ersetzen Sie auf der Registerkarte **Allgemein** unter **Name** **SQL Server Reporting Services** durch einen anderen Namen.

6. Wählen Sie **Anwenden**aus.

## <a name="next-steps"></a>Nächste Schritte

[Webportal](../../reporting-services/web-portal-ssrs-native-mode.md)  
[Browserunterstützung für Reporting Services](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
[Konfigurieren einer URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Überprüfen einer Installation von Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Aktivieren von Reporting Services-Funktionen ein- oder ausschalten](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
[Verwalten eines Berichtsservers von Reporting Services im einheitlichen Modus](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Konfigurieren Sie einen Berichtsserver im einheitlichen Modus für die lokale Verwaltung](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)

 Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)

