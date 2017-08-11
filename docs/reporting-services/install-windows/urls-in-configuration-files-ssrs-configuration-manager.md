---
title: URLs in Konfigurationsdateien (SSRS-Konfigurations-Manager) | Microsoft Docs
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- URL configuration [Reporting Services]
ms.assetid: 4f5e7fe0-b5b1-4665-93d4-80dce12d6b14
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c3add6da899bdf6d62134d3df15db35aa5b1b569
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="urls-in-configuration-files--ssrs-configuration-manager"></a>URLs in Konfigurationsdateien (SSRS-Konfigurations-Manager)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] speichert Anwendungseinstellungen in einer RSReportServer.config-Datei. In dieser Datei befinden sich Konfigurationseinstellungen sowohl für URLs als auch für URL-Reservierungen. Diese Konfigurationseinstellungen haben ganz verschiedene Zwecke und Regeln für Änderungen. Wenn Sie es gewohnt sind, Konfigurationsdateien zu ändern, um eine Bereitstellung zu optimieren, finden Sie in diesem Thema hilfreiche Informationen dazu, wie jede URL-Einstellung verwendet wird.  
  
## <a name="url-settings-in-rsreportserverconfig-file"></a>URL-Einstellungen in der RSReportServer.config-Datei  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] speichert URLs für den Anwendungs- und Berichtszugriff und zur Verbindung von Web-Front-End-Komponenten mit einem Back-End-Berichtsserver.  
  
#### <a name="urls-for-application-access"></a>URLs für Anwendungszugriff  
 URLs werden für den Zugriff auf den Report Server-Webdienst und den [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]verwendet. Verwenden Sie zum Konfigurieren der URLs das Reporting Services-Konfigurationstool. Das Tool erstellt die URL-Reservierungen für jede Anwendung in HTTP.SYS und fügt Einträge für die URLs im Abschnitt **URLReservations** der Datei RSReportServer.config hinzu.  
  
-   Die Beschreibungen der einzelnen Elemente finden Sie im Abschnitt **URLReservations** des Artikels [RSReportServer-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
-   Weitere Informationen zur Syntax der **UrlString** Element finden Sie unter [URL-Reservierungssyntax &#40; SSRS-Konfigurations-Manager &#41; ](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md).  
  
-   Anweisungen zum Konfigurieren von URLs für den Anwendungszugriff finden Sie unter [Konfigurieren einer URL &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)verwendet.  
  
#### <a name="urls-for-report-access"></a>URLs für Berichtszugriff  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] umfasst eine Berichtsserver-E-Mail-Übermittlungserweiterung, mit der Sie Berichtslinks oder Anlagen senden können. Ein Berichtshyperlink wird erstellt, wenn der Bericht übermittelt wird. Die Berichtsserver-E-Mail-Übermittlungserweiterung erstellt den Link mithilfe der **UrlRoot** -Einstellung in der Konfigurationsdatei. Die**UrlRoot** -Einstellung wird außerdem dazu verwendet, Links in einem gerenderten Bericht, der über die unbeaufsichtigte Berichtsverarbeitung generiert wird, aufzulösen.  
  
 **UrlRoot** wird automatisch in der RSReportServer.config-Datei angegeben, wenn Sie URLs für den Anwendungszugriff konfigurieren. Wenn Sie diesen Wert in der Konfigurationsdatei ändern, müssen Sie eine gültige URL-Adresse für einen Report Server-Webdienst angeben, der mit einer Berichtsserver-Datenbank mit Berichten, die Sie übermitteln möchten, verbunden ist. Sie können nur einen **UrlRoot** -Wert für eine einzelne Berichtsserverinstanz angeben. In der RSReportServer.config-Datei kann nur ein **UrlRoot** -Eintrag für eine bestimmte Berichtsserverinstanz vorhanden sein. Wenn mehrere URLs für den Report Server-Webdienst reserviert sind, müssen Sie einen der verfügbaren Werte für **UrlRoot**auswählen.  
  
 In den meisten Fällen ist es nicht notwendig, **UrlRoot**zu ändern. Wenn der Zugriff auf den Berichtsserver jedoch über eine vollqualifizierte URL erfolgt und Sie keine URL konfiguriert haben, die einen Hostheader zum vollqualifizierten Websitenamen verwendet, müssen Sie die Datei „RSReportServer.config“ manuell bearbeiten, um **UrlRoot** auf die vollqualifizierte URL des Berichtsservers festzulegen, mit der der Bericht gerendert wird (z.B. https://www.adventure-works.com/mywebapp/reportserver).  
  
#### <a name="urls-connecting-the-includessrswebportalincludesssrswebportalmd-and-web-parts-to-the-report-server-web-service"></a>URLs zur Verbindung des [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] und Webparts zum Berichtsserver-Webdienst  
 Der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] und SharePoint 2.0 Webparts für Reporting Services sind Web-Front-End-Komponenten, die eine Verbindung zu einem Berichtsserver herstellen. URLs, die verwendet werden, um eine Verbindung mit einem Back-End-Berichtsserver herzustellen, umfassen Folgendes:  
  
-   **ReportServerUrl** (verwendet von [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)])  
  
-   **ReportServerExternalUrl** (von Webparts verwendet)  
  
> [!NOTE]  
>  Frühere Versionen von Reporting Services beinhalteten das **ReportServerVirtualDirectory** -Element. Dieser Wert ist in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und in höheren Versionen veraltet. Wenn Sie eine vorhandene Installation aktualisiert haben und eine Konfigurationsdatei mit dieser Einstellung verwenden, wird dieser Wert vom Berichtsserver nicht mehr gelesen.  
  
 Die folgende Tabelle bietet einen Überblick über alle URLs, die in einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationsdatei angegeben werden können.  
  
|Einstellung|Verwendung|Beschreibung|  
|-------------|-----------|-----------------|  
|**ReportServerUrl**|Optional. Dieses Element ist nicht in der RSReportServer.config-Datei enthalten, es sei denn, Sie fügen es selbst hinzu.<br /><br /> Legen Sie dieses Element nur fest, wenn Sie eines der folgenden Szenarios konfigurieren:<br /><br /> Der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] stellt einen Web-Front-End-Zugriff auf einen Berichtsserver-Webdienst bereit, der auf einem anderen Computer oder einer anderen Instanz desselben Computers ausgeführt wird.<br /><br /> Wenn Sie mehrere URLs zu einem Berichtsserver haben und der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] eine bestimmte URL verwenden soll.<br /><br /> Sie besitzen eine bestimmte Berichtsserver-URL, die für alle [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] -Verbindungen verwendet werden soll.<br /><br /> Sie aktivieren beispielsweise den [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] -Zugriff für alle Computer im Netzwerk, möchten jedoch, dass sich der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] über eine lokale Verbindung mit dem Berichtsserver verbindet. In diesem Fall können Sie möglicherweise konfigurieren **"ReportServerUrl"** zu "`http://localhost/reportserver`".|Dieser Wert gibt eine URL zum Berichtsserver-Webdienst an. Dieser Wert wird von der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] -Anwendung beim Start gelesen. Wenn dieser Wert festgelegt ist, stellt der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] eine Verbindung zu dem in der URL angegebenen Berichtsserver her.<br /><br /> Der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] stellt standardmäßig einen Web-Front-End-Zugriff auf den Berichtsserver-Webdienst bereit, der innerhalb derselben Berichtsserver-Instanz ausgeführt wird wie der [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. Wenn Sie den [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] jedoch mit einem Berichtsserver-Webdienst verwenden möchten, der zu einer anderen Instanz gehört oder in einer Instanz auf einem anderen Computer ausgeführt wird, können Sie diese URL zur Weiterleitung des [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] festlegen, sodass dieser eine Verbindung mit dem externen Berichtsserver-Webdienst herstellt.<br /><br /> Wenn ein SSL-Zertifikat (Secure Sockets Layer) auf dem Berichtsserver installiert ist, mit dem Sie eine Verbindung herstellen, muss der Wert von **ReportServerUrl** dem Namen des Servers entsprechen, der für das Zertifikat registriert ist. Wenn Sie die Fehlermeldung „Die zugrunde liegende Verbindung wurde geschlossen: Für den geschützten SSL/TLS-Kanal konnte keine Vertrauensstellung hergestellt werden“ erhalten, legen Sie **ReportServerUrl** auf den vollqualifizierten Domänennamen des Servers fest, für den das Zertifikat ausgestellt wurde. Wenn das Zertifikat beispielsweise für **https://adventure-works.com.onlinesales**registriert ist, lautet die URL des Berichtsservers **https://adventure-works.com.onlinesales/reportserver**.|  
|**ReportServerExternalUrl**|Optional. Dieses Element ist nicht in der RSReportServer.config-Datei enthalten, es sei denn, Sie fügen es selbst hinzu.<br /><br /> Legen Sie dieses Element nur fest, wenn Sie SharePoint 2.0 Webparts verwenden und möchten, dass Benutzer einen Bericht abrufen und in einem neuen Browserfenster öffnen können.<br /><br /> Hinzufügen \< **ReportServerExternalUrl**> unterhalb der \< **"ReportServerUrl"**>-Element, und legen ihn auf einem Berichtsserver vollqualifizierten Namen, die aufgelöst wird, um eine Berichtsserverinstanz bei Zugriff in einem separaten Browserfenster. Löschen Sie nicht \< **"ReportServerUrl"**>.<br /><br /> Das folgende Beispiel veranschaulicht die Syntax:<br /><br /> `<ReportServerExternalUrl>http://myserver/reportserver</ReportServerExternalUrl>`|Dieser Wert wird von SharePoint 2.0 Webparts verwendet.<br /><br /> In früheren Versionen wurde empfohlen, diesen Wert festzulegen, um den Berichts-Generator auf einem mit dem Internet verbundenen Berichtsserver bereitzustellen. Dies ist ein ungeprüftes Bereitstellungsszenario. Wenn Sie diese Einstellung in der Vergangenheit verwendet haben, um den Zugriff auf den Berichts-Generator aus dem Internet zu unterstützen, sollten Sie sich eine Alternative überlegen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren des Berichtsserver-URLs &#40; SSRS-Konfigurations-Manager &#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Konfigurieren einer URL &#40; SSRS-Konfigurations-Manager &#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)

