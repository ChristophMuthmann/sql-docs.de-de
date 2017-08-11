---
title: Informationen zu URL-Reservierungen und Registrierungen (SSRS-Konfigurations-Manager) | Microsoft Docs
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
- URL reservations
- URL registration
- Report Server service, URL reservations
ms.assetid: c2c460c3-e749-4efd-aa02-0f8a98ddbc76
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: eb1f09f1a23a6e24077357c36a0dbc136a86473f
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="about-url-reservations-and-registration--ssrs-configuration-manager"></a>Informationen zu URL-Reservierungen und Registrierungen (SSRS-Konfigurations-Manager)
  Anwendungen für URLs für Reporting Services werden als URL-Reservierungen in HTTP.SYS definiert. Eine URL-Reservierung definiert die Syntax eines URL-Endpunkts für eine Webanwendung. URL-Reservierungen werden sowohl für den Berichtsserver-Webdienst als auch für den Berichts-Manager beim Konfigurieren der Anwendungen auf dem Berichtsserver definiert. Beim Konfigurieren von URLs mit Setup oder mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool werden URL-Reservierungen automatisch für Sie erstellt:  
  
-   Setup erstellt URL-Reservierungen mit Standardwerten. Im Rahmen der Standardkonfiguration werden zwei URLs von Setup reserviert, eine für den Berichtsserver-Webdienst und eine für den Berichts-Manager. Mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool können Sie weitere URLs hinzufügen oder die von Setup erstellten Standard-URLs ändern.  
  
-   Das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool erstellt eine URL-Reservierung basierend auf der URL, die Sie auf der Seite **Webdienst-URL** oder auf der Seite **Webportal-URL** im Tool angegeben haben.  
  
 Setup und das Tool weisen dem Berichtsserver-Dienst außerdem Berichtigungen für die URL zu, suchen nach doppelten Instanzen und fügen HTTP.SYS die URL-Reservierung hinzu. Erstellen oder ändern Sie URL-Reservierungen für Reporting Services niemals direkt mit HttpCfg.exe oder einem anderen Tool. Wenn Sie einen Schritt überspringen oder einen ungültigen Wert festlegen, kann es zu Problemen kommen, die schwer zu diagnostizieren oder zu beheben sind.  
  
> [!NOTE]  
>  HTTP.SYS ist eine Komponente des Betriebssystems, die nach Netzwerkanforderungen lauscht und diese an eine Warteschlange für Anforderungen weiterleitet. In dieser Version von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]erstellt HTTP.SYS die Warteschlange für Anforderungen für den Berichtsserver-Webdienst und für den Berichts-Manager und verwaltet diese. Internetinformationsdienste (IIS) wird nicht mehr zum Hosten von oder Zugreifen auf [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungen verwendet. Weitere Informationen über HTTP.SYS-Funktionen finden Sie unter [HTTP-Server-API](http://go.microsoft.com/fwlink/?LinkId=92652) auf MSDN.  
  
##  <a name="ReportingServicesURLs"></a> URLs in Reporting Services  
 In einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation können Sie über URLs auf die folgenden Tools, Anwendungen und Elemente zugreifen:  
  
-   Report Server-Webdienst  
  
-   Webportal  
  
-   Berichte, die auf einem Berichtsserver veröffentlicht wurden  
  
 Andere veröffentlichte Elemente wie z.B. freigegebene Datenquellen, die via URL adressierbar sind, sollten nicht über URLs in Form von eigenständigen Elementen zugreifbar sein. Diese Elemente werden vom Berichtsserver bei der Anzeige in einem Browserfenster nicht in einem aussagekräftigen Format dargestellt.  
  
> [!NOTE]  
>  Dieses Thema beschreibt nicht den URL-Zugriff auf bestimmte Berichte, die auf dem Berichtsserver gespeichert sind. Weitere Informationen zum URL-Zugriff auf diese Elemente finden Sie in der [-Onlinedokumentation unter](../../reporting-services/access-report-server-items-using-url-access.md) Zugreifen auf Berichtsserverelemente über den URL-Zugriff [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="URLreservation"></a> Registrierung und Reservierung für URLs  
 Eine URL-Reservierung definiert die URLs, über die auf eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendung zugegriffen werden kann. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] reserviert mindestens eine URL für den Berichtsserver-Webdienst und für das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] in HTTP.SYS und registriert diese, wenn der Dienst gestartet wird. Sie können Berichte über den Webdienst öffnen, indem Sie Parameter an die URL anfügen. Reservierungen und Registrierungen werden von HTTP.SYS bereitgestellt. Weitere Informationen finden Sie unter [Namespacereservierungen, Registrierung und Routing](http://go.microsoft.com/fwlink/?LinkId=92653) auf MSDN.  
  
 Bei der*URL-Reservierung* wird ein URL-Endpunkt für eine Webanwendung erstellt und in HTTP.SYS gespeichert. HTTP.SYS ist das allgemeine Repository für alle URL-Reservierungen, die auf einem Computer definiert wurden, und definiert eine Reihe allgemeiner Regeln für eindeutige URL-Reservierungen.  
  
 Die*URL-Registrierung* wird bei Dienststart vorgenommen. Die Anforderungswarteschlange wird erstellt, und HTTP.SYS beginnt mit dem Weiterleiten von Anforderungen an diese Warteschlange. URL-Endpunkte müssen registriert werden, bevor Anforderungen an diese Endpunkte der Warteschlange hinzugefügt werden. Beim Start des Berichtsserver-Diensts werden alle URLs registriert, die für die entsprechenden Anwendungen reserviert wurden. Dies bedeutet, dass der Webdienst für eine Registrierung aktiviert sein muss. Wenn Sie die **WebServiceAndHTTPAccessEnabled** -Eigenschaft im Facet „Oberflächenkonfiguration für Reporting Services“ der richtlinienbasierten Verwaltung auf **False** festgelegt haben, wird die URL für den Webdienst bei Dienststart nicht registriert.  
  
 Wenn Sie den Dienst anhalten oder den Webdienst oder die [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] -Anwendungsdomäne beenden und neu starten, wird die Registrierung der URLs aufgehoben. Wenn Sie eine URL-Reservierung ändern, während der Dienst ausgeführt wird, wird die Anwendungsdomäne  vom Berichtsserver unmittelbar wiederverwendet, um die Registrierung der alten URL aufzuheben und die Verwendung einer neuen URL zu ermöglichen.  
  
 Mit einigen einfachen Beispielen werden das Konzept der URL-Reservierung und der Zusammenhang mit URL-Adressen für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungen veranschaulicht. Beachten Sie, dass die URL-Reservierung eine andere Syntax aufweist als die URL, mit der Sie auf die Anwendung zugreifen:  
  
|URL-Reservierung in HTTP.SYS|URL|Erklärung|  
|---------------------------------|---------|-----------------|  
|`http://+:80/reportserver`|`http://<computername>/reportserver`<br /><br /> `http://<IPAddress>/reportserver`<br /><br /> `http://localhost/reportserver`|Die URL-Reservierung gibt ein Platzhalterzeichen (+) für Port 80 an. Dadurch werden alle eingehenden Anforderungen, die einen Host für die Auflösung zum Berichtsservercomputer auf Port 80 angeben, in der Berichtsserverwarteschlange abgelegt. Mit dieser URL-Reservierung kann eine beliebige Anzahl von URLs für den Zugriff auf den Berichtsserver verwendet werden.<br /><br /> Dies ist die Standard-URL-Reservierung für einen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver für die meisten Betriebssysteme.|  
|`http://123.45.67.0:80/reportserver`|`http://123.45.67.0/reportserver`|Diese URL-Reservierung gibt eine IP-Adresse an und ist viel restriktiver als die Platzhalter-URL-Reservierung. Nur mit URLs, die eine IP-Adresse enthalten, kann eine Verbindung mit dem Berichtsserver hergestellt werden. Erhält eine Anforderung an einen Berichtsserver unter dieser URL-Reservierung `http://<computername>/reportserver` oder `http://localhost/reportserver` fehlschlagen.|  
  
##  <a name="DefaultURLs"></a> Standard-URLs  
 Wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in der Standardkonfiguration installieren, reserviert Setup URLs für den Berichtsserver-Webdienst und das [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. Sie können diese Standardwerte auch für URL-Reservierungen im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool verwenden. Wenn Sie [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] installieren oder wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] als benannte Instanz installieren, enthalten Standard-URLs einen Instanznamen.  
  
> [!IMPORTANT]  
>  Das Instanzzeichen ist ein Unterstrich (**_**).  
  
 URL-Reservierungen enthalten eine Portnummer. In den folgenden Betriebssystemen kann ein Port von mehreren Webanwendungen verwendet werden:  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2  
  
-   [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
-   [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
-   [!INCLUDE[win7](../../includes/win7-md.md)]  
  
-   [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]  
  
|Instanztyp|Application|Standard-URL|Tatsächliche URL-Reservierung in HTTP.SYS|  
|-------------------|-----------------|-----------------|----------------------------------------|  
|Standardinstanz|Report Server-Webdienst|`http://\<servername>/reportserver`|`http://<servername>:80/reportserver`|  
|Standardinstanz|Webportal|`http://<servername>/reportserver`|`http://<servername>:80/reportserver`|  
|Benannte Instanz|Report Server-Webdienst|`http://<servername>/reportserver_<instancename>`|`http://<servername>:80/reportserver_<instancename>`|  
|Benannte Instanz|Webportal|`http://<servername>/reports_<instancename>`|`http://<servername>:80/reports_<instancename>`|  
|SQL Server Express|Report Server-Webdienst|`http://<servername>/reportserver_SQLExpress`|`http://<servername>:80/reportserver_SQLExpress`|  
|SQL Server Express|Webportal|`http://<servername>/reports_SQLExpress`|`http://<servername>:80/reports_SQLExpress`|  
  
##  <a name="URLPermissionsAccounts"></a> Authentifizierung und Dienstidentität für Reporting Services-URLs  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]URL-Reservierungen geben das Dienstkonto des Report Server-Dienst. Das Konto, unter dem der Dienst ausgeführt wird, wird für alle URLs verwendet, die für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Anwendungen erstellt werden, die in der gleichen Instanz ausgeführt werden. Die Dienstidentität der Berichtsserverinstanz wird in der Datei RSReportServer.config gespeichert.  
  
 Das Dienstkonto hat keinen Standardwert. Beim Setup ist jedoch die Angabe eines Dienstkontos unter **URLReservation** in RSReportServer.config erforderlich. Dies gilt auch, wenn der Server im reinen Dateimodus installiert wird. Gültige Werte für das Dienstkonto enthalten ein Domänenbenutzerkonto, ein **LocalSystem**oder einen **NetworkService**.  
  
 Der anonyme Zugriff ist aufgrund der Standardsicherheitseinstellung **RSWindowsNegotiate**deaktiviert. Berichtsserver-URLs verwenden Netzwerkcomputernamen für den Intranetzugriff. Wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] für Internetverbindungen konfigurieren möchten, müssen Sie andere Einstellungen verwenden. Weitere Informationen finden Sie in der [-Onlinedokumentation unter](../../reporting-services/security/authentication-with-the-report-server.md) Authentifizierung beim Berichtsserver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="URLlocalAdmin"></a> URLs für die lokale Verwaltung  
 Sie können `http://localhost/reportserver` oder `http://localhost/reports` , wenn Sie ein starkes oder schwaches Platzhalterzeichen für die URL-Reservierung angegeben.  
  
 Die `http://localhost` URL wird als interpretiert `http://127.0.0.1`. Wenn Sie die URL-Reservierung mit einem Computernamen oder einer einzelnen IP-Adresse verbunden haben, können Sie localhost nicht verwenden, es sei denn, Sie erstellen eine zusätzliche Reservierung für 127.0.0.1 auf dem lokalen Computer. Analog dazu gilt, dass Sie die URL nicht verwenden können, wenn Sie localhost oder 127.0.0.1 auf Ihrem Computer deaktiviert haben.  
  
 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)], [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] und höher enthalten neue Sicherheitsfunktionen, um das Risiko einer versehentlichen Ausführung von Programmen mit erweiterten Berechtigungen zu minimieren. Zur Aktivierung der lokalen Verwaltung für diese Betriebssysteme müssen zusätzliche Schritte ausgeführt werden. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für die lokale Verwaltung &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren einer URL &#40; SSRS-Konfigurations-Manager &#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [URL-Reservierungssyntax &#40; SSRS-Konfigurations-Manager &#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)  
  
  

