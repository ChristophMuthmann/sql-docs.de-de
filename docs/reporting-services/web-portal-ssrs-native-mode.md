---
title: Webportal (einheitlicher SSRS-Modus) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 7349e626-6ed5-4d21-b05f-cf042ad9ad70
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 68cdac26293a2025a7a2cf8833d2d0f2f4f6ff8c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="web-portal-ssrs-native-mode"></a>Webportal (einheitlicher SSRS-Modus)

[!INCLUDE[ssrs-appliesto-sql2016-preview](../includes/ssrs-appliesto-sql2016-preview.md)]

Die Reporting Services-Web-Portal ist eine webbasierte Erfahrung basismesswerte für mobile Berichte und KPIs, Berichte anzeigen, und navigieren Sie durch die Elemente, die in Ihrer Berichtsserverinstanz befinden. Das Webportal können auch um eine einzelne Berichtsserverinstanz zu verwalten.

![SSRS-Portal](../reporting-services/media/ssrsportal.png)

## <a name="what-is-the-web-portal"></a>Was ist das Webportal

Das Webportal können Sie die folgenden Aufgaben ausführen:

- Anzeigen, Suchen, Drucken und Abonnieren von Berichten.

- Erstellen, Sichern und Warten der Ordnerhierarchie zum Organisieren von Elementen auf dem Server.

- Konfigurieren der rollenbasierten Sicherheit, die den Zugriff auf Elemente und Vorgänge bestimmt.

- Konfigurieren von Berichtsausführungseigenschaften, des Berichtsverlauf und von Berichtsparametern.

- Erstellen freigegebener Zeitpläne und Datenquellen für eine leichtere Verwaltung von Zeitplänen und Datenquellenverbindungen.

- Erstellen datengesteuerter Abonnements, die Berichte an eine lange Empfängerliste verteilen.

- Erstellen verknüpfter Berichte, um einen vorhandenen Bericht wiederzuverwenden und auf verschiedene Weisen dessen Zweck zu ändern.

- Herunterladen von weit verbreiteten Tools wie beispielsweise Berichts-Generator und Publisher für mobile Berichte.

- [Erstellen von KPIs](../reporting-services/working-with-kpis-in-reporting-services.md).

- Senden von Feedback oder Anfragen zu Features.

Das Webportal können den Berichtsserverordner oder suchen Sie nach bestimmten Berichten gesucht. Sie können einen Bericht, seine allgemeinen Eigenschaften und alte Versionen anzeigen, die in einem Berichtsverlauf erfasst sind. Je nach den Ihnen gewährten Berechtigungen können Sie unter Umständen Berichte abonnieren, die an ein E-Mail-Postfach oder einen freigegeben Ordner im Dateisystem übermittelt werden.

> [!NOTE]
> Informationen zu unterstützten Browsern und Versionen finden Sie unter [Browserunterstützung für Reporting Services und Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md).

Das Webportal wird nur für einen Berichtsserver verwendet, der im einheitlichen Modus ausgeführt wird. Er wird nicht für einen Berichtsserver unterstützt, den Sie für den integrierten Modus von SharePoint konfiguriert haben.

Einige webportalfunktionen sind nur in bestimmten Editionen von verfügbar [!INCLUDE[ssNoVersion](../includes/ssnoversion.md)]. Weitere Informationen finden Sie unter [Reporting Services-Funktionen von den SQL Server 2016-Editionen unterstützte](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

In einer neuen Installation verfügen nur lokale Administratoren über ausreichende Berechtigungen zum Verwenden des Inhalts und der Einstellungen. Wenn Sie anderen Benutzern Berechtigungen erteilen möchten, muss ein lokaler Administrator Rollenzuweisungen erstellen, die den Zugriff auf den Berichtsserver ermöglichen. Die Anwendungsseiten und Aufgaben, auf die ein Benutzer anschließend Zugriff erhält, sind von den Rollenzuweisungen für den Benutzer abhängig. Weitere Informationen finden Sie unter [Gewähren von Benutzerzugriff auf einem Berichtsserver](security/grant-user-access-to-a-report-server-report-manager.md)

> [!NOTE]
> Falls Sie auf dem lokalen Computer, auf dem der Server läuft, zum Webportal navigieren, wird Ihnen möglicherweise eine Meldung angezeigt, die besagt, dass Sie nicht berechtigt sind, diesen Ordner anzuzeigen. Das liegt an der Benutzerkontensteuerung (User Account Control; UAC) und daran, dass Sie den Browser nicht als Administrator ausführen. Sie können Edge nicht als Administrator ausführen. Sie werden Internet Explorer verwenden müssen. Sie können entweder remote zum Server navigieren oder Internet Explorer als Administrator starten und zum Webportal gehen. Falls Sie das Webportal remote verwenden möchten, ist es erforderlich, dass Sie Ihrem Kontoinhalts-Manager Berechtigungen für den Ordner erteilen.  

## <a name="start-and-use-the-web-portal"></a>Starten und verwenden des Webportals

Die Web-Portal ist eine Webanwendung, die Sie, indem Sie eingeben Öffnen der [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] URL in der Adressleiste des Browserfensters. Wenn Sie das [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]starten, variieren die angezeigten Seiten, Links und Optionen je nach den Berechtigungen, über die Sie auf dem Berichtsserver verfügen. Um einen Task auszuführen, müssen Sie einer Rolle zugewiesen sein, die den Task einschließt.  Ein Benutzer, dem eine Rolle mit vollen Berechtigungen zugewiesen wurde, hat Zugriff auf sämtliche Anwendungsmenüs und Seiten zum Verwalten eines Berichtsservers. Einem Benutzer, dem eine Rolle mit der Berechtigung zum Anzeigen und Ausführen von Berichten zugewiesen wurde, werden dagegen nur die Menüs und Seiten angezeigt, die diese Aktivitäten unterstützen. Jeder Benutzer kann über verschiedene Rollenzuweisungen für verschiedene Berichtsserver oder sogar für die verschiedenen Berichte und Ordner auf einem einzigen Berichtsserver verfügen.

Weitere Informationen zu den Rollen finden Sie unter [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).

### <a name="start-the-web-portal"></a>Starten Sie das Webportal

Um die Web-Portal in einem Browser zu starten, führen Sie folgende Schritte aus:

1. Öffnen Sie Ihren Webbrowser. Eine Liste der unterstützten Webbrowser finden Sie unter [Planen der Unterstützung für Reporting Services und Power View-Browser (Reporting Services 2014)](../reporting-services/browser-support-for-reporting-services-and-power-view.md).

2. Geben Sie in der Adressleiste des Webbrowsers, im Webportal URL.

    Standardmäßig lautet die URL *http://[ComputerName]/reports*.

    Der Berichtsserver ist möglicherweise für die Verwendung eines bestimmten Ports konfiguriert. Beispielsweise *http://[ComputerName]:80/reports* oder *http://[ComputerName]:8080/reports*.

## <a name="grouping-by-categories"></a>Gruppieren nach Kategorien

Das Webportal werden Elemente in verschiedene Kategorien zu gruppieren. Die folgenden Kategorien sind verfügbar.

- KPIs (Key Performance Indicators)
- Mobile Berichte
- Paginierte Berichte
- Power BI Desktop-Berichte
- Excel-Arbeitsmappen
- Datasets
- Datenquellen
- Ressourcen

Sie können steuern, was angezeigt werden soll, indem Sie oben rechts **View** (Ansicht) auswählen. Wenn Sie „Show Hidden“ (Ausgeblendete anzeigen) auswählen, werden diese Elemente in einer helleren Farbe angezeigt.

![SSRS-WebPortal-Ansicht](../reporting-services/media/ssrswebportal-view.png)

![SSRS-WebPortal-ausgeblendet](../reporting-services/media/ssrswebportal-hidden.png)

### <a name="power-bi-desktop-reports-and-excel-workbooks"></a>Power BI Desktop-Berichte und Excel-Arbeitsmappen

Sie können Berechtigungen für Power BI Desktop-Berichte und Excel-Arbeitsmappen hochladen, organisieren und verwalten. Sie werden innerhalb des Webportals gruppiert.

![SSRS-WebPortal-Ansicht-PBI-und-Excel](../reporting-services/media/ssrswebportal-view-pbi-and-excel.png)

Die Dateien werden innerhalb von Reporting Services gespeichert, ähnlich wie andere Ressourcendateien. Wenn Sie eines dieser Elemente auswählen, wird es lokal auf Ihrem Desktop heruntergeladen. Sie können Ihre Änderungen speichern, indem Sie sie erneut auf den Berichtsserver hochladen.

## <a name="search-for-items"></a>Suche nach Elementen

Sie können einen Suchbegriff eingeben, und es werden Ihnen alle Elemente angezeigt auf die Sie Zugriff haben. Die Ergebnisse werden in KPIs, Berichte, Datasets und andere Elemente kategorisiert. Sie können dann mit den Ergebnissen interagieren und diese zu Ihren Favoriten hinzufügen.

![SSRS-WebPortal-Suche](../reporting-services/media/ssrswebportal-search.png)

## <a name="web-portal-tasks"></a>Webportal-Aufgaben

[Branding the web portal (Branding des Webportals)](../reporting-services/branding-the-web-portal.md)

[Arbeiten mit KPIs](../reporting-services/working-with-kpis-in-reporting-services.md)

[Working with shared datasets (Arbeiten mit freigegebenen Datasets)](../reporting-services/work-with-shared-datasets-web-portal.md)

## <a name="see-also"></a>Siehe auch

[Erstellen und Veröffentlichen von mobilen Berichten mit dem Publisher für mobile Berichte von SQL Server](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
[Konfigurieren einer URL (SSRS-Konfigurations-Manager)](../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
[Reporting Services-Tools](../reporting-services/tools/reporting-services-tools.md)  
[Browserunterstützung für Reporting Services und Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[Reporting Services-Funktionen, die von den SQL Server 2016-Editionen unterstützt](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)  

Weiteren Fragen wenden? [Wiederholen Sie den Reporting Services-forum](http://go.microsoft.com/fwlink/?LinkId=620231)
