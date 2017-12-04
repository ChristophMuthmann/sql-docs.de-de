---
title: Konfigurieren von Berichtsserver-URLs (SSRS-Konfigurations-Manager) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Server Windows service, virtual directories
- report servers [Reporting Services], virtual directories
- virtual directories [Reporting Services]
- Report Manager [Reporting Services], virtual directories
ms.assetid: a0134ef0-086c-443e-93b9-7213a3d76393
caps.latest.revision: "10"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: 10a3b057521c849fadae8bbe38b54317acf22a81
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="configure-report-server-urls--ssrs-configuration-manager"></a>Konfigurieren von Berichtsserver-URLs (SSRS-Konfigurations-Manager)
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]werden URLs für den Zugriff auf den Report Server-Webdienst und das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]verwendet. Bevor Sie die eine der Anwendungen verwenden können, müssen Sie mindestens je eine URL für den Webdienst und das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]konfigurieren. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bietet Standardwerte für beide Anwendungs-URLs, die in den meisten Bereitstellungsszenarien gut funktionieren, auch in parallelen Bereitstellungen mit anderen Webdiensten und -anwendungen.  
  
-   Wenn Sie die Standardkonfiguration installiert haben, wurden die URLs automatisch anhand der Standardwerte erstellt.  
  
-   Wenn Sie die URLs mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool erstellen oder ändern, können Sie die Standardwerte für eine URL übernehmen oder eigene Werte angeben. Wenn Sie die URL definieren, wird auf der Seite ein Testlink der URL angezeigt, sodass Sie sofort bestätigen können, dass die von Ihnen angegebenen Einstellungen zu einer gültigen Verbindung führen. Schrittanleitungen zum Konfigurieren einer URL finden Sie unter [Konfigurieren einer URL &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)verwendet.  
  
## <a name="defining-a-report-server-url"></a>Definieren einer Berichtsserver-URL  
 Die URL gibt den Ort für die Instanz einer Berichtsserveranwendung genau im Netzwerk an. Wenn Sie eine Berichtsserver-URL erstellen, müssen Sie die folgenden Teile angeben.  
  
|Teil|Beschreibung|  
|----------|-----------------|  
|Hostname|Ein TCP/IP-Netzwerk verwendet eine IP-Adresse, um ein Gerät im Netzwerk eindeutig zu bestimmen. Es gibt eine physische IP-Adresse für jede in einem Computer installierte Netzwerkkarte. Wenn die IP-Adresse in einen Hostheader aufgelöst wird, können Sie den Hostheader angeben. Wenn Sie den Berichtsserver in einem Unternehmensnetzwerk bereitstellen, können Sie den Netzwerknamen des Computers verwenden.|  
|Port|Ein TCP-Port ist ein Endpunkt im Gerät. Der Berichtsserver lauscht Anforderungen auf einem festgelegten Port.|  
|Virtuelles Verzeichnis|Ein Port wird oft von mehreren Webdiensten oder Anwendungen gemeinsam genutzt. Aus diesem Grund hat eine Berichtsserver-URL immer ein virtuelles Verzeichnis, das der Anwendung entspricht, die die Anforderung erhält. Sie müssen für jede [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendung, die auf derselben IP-Adresse und auf demselben Port lauscht, einen eindeutigen Namen für das virtuelle Verzeichnis angeben.|  
|SSL-Einstellungen|URLs in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] können so konfiguriert werden, dass sie ein vorhandenes SSL-Zertifikat verwenden, das bereits vorher auf dem Computer installiert wurde. Weitere Informationen finden Sie unter [Konfigurieren von SSL-Verbindungen auf einem Berichtsserver im einheitlichen Modus](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.|  
  
## <a name="default-urls"></a>Standard-URLs  
 Wenn Sie über eine URL auf einen Berichtsserver oder das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] zugreifen, sollte die URL den Hostnamen enthalten, nicht die IP-Adresse. In einem TCP/IP-Netzwerk wird die IP-Adresse in einen Hostnamen aufgelöst (oder in den Netzwerknamen des Computers). Falls Sie die URLs mithilfe von Standardwerten konfiguriert haben, sollten Sie den Report Server-Webdienst mithilfe der URLs aufrufen können, die den Computernamen oder localhost als Hostnamen angeben:  
  
-   `http://<computername>/reportserver`  
  
-   `http://localhost/reportserver`  
  
 Die Einstellungen, die diese URLs verfügbar machen, werden in der folgenden Tabelle angezeigt. Diese Tabelle zeigt die Standardwerte, die eine Berichtsserver-Verbindung über URLs ermöglichen, die einen Hostnamen enthalten:  
  
|Teil|Wert|Erklärung|  
|----------|-----------|-----------------|  
|IP-Adresse|Alle zugewiesenen|Der Domänennamendienst in Ihrem Netzwerk löst den Hostnamen in der URL in die IP-Adresse des Computers auf. Solange die IP-Adresse in der von Ihnen definierten URL angegeben ist, erreicht eine Anforderung, die an einen bestimmten Host gesandt wird, stets ihr angegebenes Ziel.|  
|Port|80|Port 80 ist der Standardport für TCP/IP-Verbindungen auf einem Computer. Da der Berichtsserver die Überwachung an Port 80 durchführt, können Sie die Portnummer der URL weglassen. Wenn Sie einen anderen Port angeben, müssen Sie diesen in der URL angeben.|  
|Virtuelles Verzeichnis|ReportServer|Beachten Sie, dass beide Beispiel-URLs den Namen des virtuellen Verzeichnisses enthalten. Wenn Sie die URL-Definition nicht anpassen, müssen Sie stets den Namen des virtuellen Verzeichnisses der Anwendung in der URL angeben.|  
  
> [!NOTE]  
>  Eine zugrunde liegende URL-Reservierung macht es möglich, dass jeder gültige Hostname in einer URL verwendet werden kann. Das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool erstellt eine URL-Reservierung in HTTP.SYS und verwendet eine Syntax, die Variationen des Hostnamens zulässt, damit dieser in eine bestimmte Berichtsserverinstanz aufgelöst werden kann. Weitere Informationen zu URL-Reservierungen finden Sie unter [Informationen zu URL-Reservierungen und -Registrierungen &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)verwendet.  
  
## <a name="server-side-permissions-on-a-report-server-url"></a>Serverseitige Berechtigungen für eine Berichtsserver-URL  
 Die Berechtigungen für jeden URL-Endpunkt gelten ausschließlich für das Berichtsserver-Dienstkonto. Nur dieses Konto ist berechtigt, Anforderungen zu akzeptieren, die an die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -URLs geleitet werden. Es werden freigegebene Zugriffssteuerungslisten (Discretionary Access Control List, DACL) für das Konto erstellt und verwaltet, wenn Sie die Dienst-ID über Setup oder das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool konfigurieren. Wenn Sie das Dienstkonto ändern, aktualisiert das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool alle von Ihnen erstellten URL-Reservierungen, um die neuen Kontodaten aufzunehmen. Weitere Informationen finden Sie unter [URL-Reservierungssyntax &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)verwendet.  
  
## <a name="authenticating-client-requests-sent-to-a-report-server-url"></a>Authentifizieren von Clientanforderungen, die an eine Berichtsserver-URL gesendet wurden  
 Als Standardwert für die in den URL-Endpunkten unterstützte Authentifizierung wird die Windows-Authentifizierung vorgegeben. Dies ist die Standardsicherheitserweiterung. Wenn Sie einen Anbieter für eine benutzerdefinierte oder eine Formularauthentifizierung implementieren, müssen Sie die Authentifizierungseinstellungen auf dem Berichtsserver ändern. Optional können Sie auch die Windows-Authentifizierungseinstellungen ändern, sodass sie dem in Ihrem Netzwerk verwendeten Authentifizierungssubsystem entsprechen. Weitere Informationen finden Sie in der [unter](../../reporting-services/security/authentication-with-the-report-server.md) Authentifizierung beim Berichtsserver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Konfigurieren einer URL &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 Dieses Thema enthält Anweisungen für das Einstellen und Ändern einer URL-Reservierung im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool.  
  
 [Informationen zu URL-Reservierungen und -Registrierungen &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md)  
 Mithilfe von URLs greifen Sie auf Anwendungen und Berichte zu. Dieses Thema behandelt Anwendungs-URLs, Standard-URLs und die Funktionsweise der URL-Reservierung und -Registrierung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [URL-Reservierungssyntax &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
 Die Standard-URL-Reservierungen, die von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet werden, sind für die meisten Szenarien gültig. Wenn Sie jedoch den Zugriff einschränken oder die Verwendung auf Internet- oder Extranetzugang erweitern möchten, müssen Sie die Einstellungen möglicherweise an Ihre Anforderungen anpassen. Diese Thema behandelt die Syntax einer URL-Reservierung und gibt Empfehlungen zur Erstellung eigener Reservierungen, die Ihrer Verwendung entsprechen.  
  
 [URLs in Konfigurationsdateien &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)  
 Die Datei RSReportServer.config enthält mehrere Einträge für URL-Reservierungen und die URLs, die vom [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] und der Berichtsserver-E-Mail-Übermittlung verwendet werden. Dieses Thema fasst die URL-Konfigurationseinstellungen zusammen, damit Sie verstehen können, wie sich diese unterscheiden.  
  
 [URL-Reservierungen für Berichtsserver-Bereitstellungen mit mehreren Instanzen &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md)  
 Wenn Sie mehrere Instanzen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf einem Computer installieren, erhöht sich die Wahrscheinlichkeit, dass beim Registrieren einer URL doppelte URLs auftreten. Um diese Fehler zu vermeiden, befolgen Sie in diesem Thema die Empfehlungen zum Erstellen von instanzenspezifischen URL-Reservierungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren einer URL &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 
