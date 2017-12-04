---
title: Reporting Services-Berichtsserver | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b71d0f313c853e53572fcee71c0b29cd4cb3ca47
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="reporting-services-report-server"></a>Reporting Services-Berichtsserver

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Erfahren Sie mehr über den Hauptteil der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Reporting Services-Installation. Es besteht aus einem Verarbeitungsmodul in Verbindung mit Erweiterungen, die zusätzliche Funktionalität bereitstellen.

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

Ein Reporting Services-Berichtsserver wird in einem von zwei Bereitstellungsmodi ausgeführt: dem einheitlichen Modus oder dem SharePoint-Modus. Einen Vergleich der Features finden Sie im Abschnitt [Funktionsvergleich zwischen SharePoint und einheitlichem Modus](#bkmk_featuresupport) .  
  
 **Installation:** Informationen zur Installation von Reporting Services finden Sie im Artikel zur [Reporting Services-Installation](../install-windows/install-reporting-services.md).

## <a name="overview-of-report-server-modes"></a>Übersicht über Berichtsservermodi

 Verarbeitungsmodule (Prozessoren) sind das Kernstück des Berichtsservers. Die Prozessoren unterstützen die Integrität des Berichtssystems und können weder geändert noch erweitert werden. Erweiterungen sind auch Prozessoren, aber sie führen spezifische Funktionen aus. Reporting Services enthält mindestens eine Standarderweiterung für jeden unterstützten Erweiterungstyp. Sie können einem Berichtsserver benutzerdefinierte Erweiterungen hinzufügen. Dadurch können Sie einen Berichtsserver für die Unterstützung von Funktionen erweitern, die nicht ohne Anpassungen unterstützt werden. Beispiele für benutzerdefinierte Funktionen sind u.&nbsp;a. die Unterstützung von Technologien für einmaliges Anmelden (SSO, Single Sign-On), der Berichtsausgabe in Anwendungsformaten, die nicht bereits von den Standardrenderingerweiterungen verarbeitet werden, und der Berichtsübermittlung an einen Drucker oder eine Anwendung.  
  
 Eine einzelne Berichtsserverinstanz wird von der vollständigen Auflistung von Prozessoren und Erweiterungen definiert, die eine End-to-End-Verarbeitung bieten, von der Bearbeitung der ursprünglichen Anforderung bis hin zur Präsentation eines fertigen Berichts. Mithilfe seiner Unterkomponenten verarbeitet der Berichtsserver Berichtsanforderungen und macht Berichte für einen Zugriff bei Bedarf oder eine geplante Verteilung verfügbar.  
  
 Ein Berichtsserver stellt Funktionen zum Erstellen, Rendern und Übermitteln von Berichten für eine Vielzahl von Datenquellen sowie erweiterbare Authentifizierungs- und Autorisierungsschemas bereit. Darüber hinaus enthält ein Berichtsserver Berichtsserver-Datenbanken, in denen veröffentlichte Berichte, freigegebene Datenquellen, freigegebene Datasets, Berichtsteile, freigegebene Zeitpläne und Abonnements, Berichtsdefinitionsquelldateien, Modelldefinitionen, kompilierte Berichte, Momentaufnahmen, Parameter und andere Ressourcen gespeichert sind. Außerdem bietet der Berichtsserver dem Systemadministrator die Möglichkeit, die Verarbeitung von Berichtsanforderungen sowie die Verwaltung von Momentaufnahmeverläufen und Berechtigungen für Berichte, Datenquellen, Datasets und Abonnements zu konfigurieren.  
  
 Ein Reporting Services-Berichtsserver unterstützt zwei Bereitstellungsmodi für Berichtsserverinstanzen:  
  
-   **Einheitlicher Modus:** Umfasst den einheitlichen Modus mit SharePoint-Webparts, bei dem ein Berichtsserver als Anwendungsserver ausgeführt wird, der alle Verarbeitungs- und Verwaltungsfunktionen ausschließlich über Reporting Services-Komponenten bietet. Sie konfigurieren einen Berichtsserver im einheitlichen Modus mit Konfigurations-Manager für Reporting Services und SQL Server Management Studio.  
  
-   **SharePoint-Modus**: Bei diesem Modus wird ein Berichtsserver als Teil einer SharePoint-Serverfarm installiert.  Verwenden Sie PowerShell-Befehle oder SharePoint-Inhaltsverwaltungsseiten, um den SharePoint-Modus bereitzustellen und zu konfigurieren.  
  
 In SQL Server Reporting Services kann ein Berichtsserver nicht von einem Modus in den anderen wechseln. Wenn Sie den in Ihrer Umgebung verwendeten Berichtsservertyp ändern möchten, müssen Sie den gewünschten Berichtsservermodus installieren und dann die Berichtselemente oder Berichtsserver-Datenbank vom Berichtsserver der älteren Version auf den neuen Berichtsserver kopieren oder verschieben. Dieser Prozess wird in der Regel als "Migration" bezeichnet. Die für das Migrieren erforderlichen Schritte hängen vom Modus ab, zu dem Sie migrieren, und von der Version, von der Sie migrieren. Weitere Informationen finden Sie unter [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
## <a name="feature-comparison-of-sharepoint-and-native-mode"></a>Funktionsvergleich zwischen SharePoint und einheitlichem Modus
  
|Funktion oder Komponente|Einheitlicher Modus|SharePoint-Modus|  
|--------------------------|-----------------|---------------------|  
|**URL-Adressierung**|Ja|Im integrierten SharePoint-Modus wird eine andere URL-Adressierung verwendet. SharePoint-URLs werden verwendet, um auf Berichte, Berichtsmodelle, freigegebene Datenquellen und Ressourcen zu verweisen. Die Ordnerhierarchie des Berichtsservers wird nicht verwendet. Falls Sie über benutzerdefinierte Anwendungen verfügen, die vom URL-Zugriff abhängig sind, wie auf einem Berichtsserver im einheitlichen Modus unterstützt, funktionieren diese Funktionen nicht mehr, wenn der Berichtsserver für die SharePoint-Integration konfiguriert ist.<br /><br /> Weitere Informationen zum URL-Zugriff finden Sie unter [URL-Zugriffsparameterverweis](../../reporting-services/url-access-parameter-reference.md).|  
|**Benutzerdefinierte Sicherheitserweiterungen**|ja|Benutzerdefinierte Sicherheitserweiterungen mit Reporting Services können auf dem Berichtsserver nicht bereitgestellt oder verwendet werden. Der Berichtsserver schließt eine spezielle Sicherheitserweiterung ein, die verwendet wird, sobald Sie einen Berichtsserver für die Ausführung im integrierten SharePoint-Modus konfigurieren. Diese Sicherheitserweiterung ist eine interne Komponente, die für integrierte Vorgänge erforderlich ist.|  
|**Konfigurations-Manager**|Ja|**\*\* Wichtig \*\*** Mit dem Konfigurations-Manager lässt sich ein Berichtsserver im SharePoint-Modus nicht verwalten. Verwenden Sie stattdessen die SharePoint-Zentraladministration.|  
|**Berichts-Manager**|Ja|Der Berichts-Manager kann nicht zum Verwalten des SharePoint-Modus verwendet werden. Verwenden Sie die SharePoint-Anwendungsseiten. Weitere Informationen finden Sie unter [Reporting Services-SharePoint-Dienst und -Dienstanwendungen](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).|  
|**Verknüpfte Berichte**|Ja|Nein.|  
|**Meine Berichte**|Ja|Nein|  
|**Meine Abonnements** und Batchverarbeitungsmethoden.|Ja|Nein|  
|**Datenwarnungen**|Nein|Ja|  
|**Power View**|Nein|Ja<br /><br /> Erfordert Silverlight im Clientbrowser. Weitere Informationen zu den Browseranforderungen von finden Sie unter [Browserunterstützung für Reporting Services und Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).|  
|**.RDL-Berichte**|Ja|ja<br /><br /> RDL-Berichte können für Reporting Services-Berichtsserver im einheitlichen Modus oder im SharePoint-Modus ausgeführt werden.|  
|**.RDLX-Berichte**|Nein|ja<br /><br /> Power View-RDLX-Berichte können nur für Reporting Services-Berichtsserver im SharePoint-Modus ausgeführt werden.|  
|**Anmeldeinformationen für das SharePoint-Benutzertoken für die SharePoint-Listenerweiterung**|Nein|Ja|  
|**AAM-Zonen für Bereitstellungen mit Internetzugriff**|Nein|Ja|  
|**SharePoint-Sicherung und -Wiederherstellung**|Nein|Ja|  
|**ULS-Protokollunterstützung**|Nein|Ja|  
  
## <a name="native-mode"></a>Einheitlicher Modus

 Im einheitlichen Modus ist ein Berichtsserver ein eigenständiger Anwendungsserver, der das Anzeigen, Verwalten, Verarbeiten und Übermitteln von Berichten und Berichtsmodellen ermöglicht. Dies ist der Standardmodus für Berichtsserverinstanzen. Sie können einen Berichtsserver im einheitlichen Modus installieren, der während des Setups konfiguriert wird, oder Sie können ihn für Vorgänge im einheitlichen Modus konfigurieren, nachdem das Setup abgeschlossen ist.  
  
 Im nachfolgenden Diagramm ist die Drei-Ebenen-Architektur einer Reporting Services-Bereitstellung im einheitlichen Modus dargestellt. Hieraus gehen die Berichtsserverdatenbank und die Datenquellen auf der Datenebene, die Berichtsserverkomponenten auf der mittleren Ebene sowie die Clientanwendungen und integrierten bzw. benutzerdefinierten Tools auf der Präsentationsebene hervor. Daneben zeigt es den Fluss von Anforderungen und Daten zwischen den Serverkomponenten sowie welche Komponenten Inhalte an einen Datenspeicher senden bzw. aus einem Datenspeicher abrufen.  
  
 ![Reporting Services-Architektur](../../reporting-services/report-server-sharepoint/media/reporting-serv-arch.gif "Reporting Services architecture")  
  
 Der Berichtsserver wird als [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Windows-Dienst implementiert, der so genannte "Berichtsserverdienst", der einen Webdienst, die Hintergrundverarbeitung und andere Vorgänge hostet. In der Dienste-Konsolenanwendung wird der Dienst als SQL Server Reporting Services (MSSQLSERVER) aufgelistet.  
  
 Entwickler von Drittanbietern können zusätzliche Erweiterungen erstellen, um die Verarbeitungsfunktionen des Berichtsservers zu ersetzen oder zu erweitern. Weitere Informationen zu befehlsorientierten Benutzerschnittstellen, die Anwendungsentwicklern zur Verfügung stehen, finden Sie in der [Technischen Referenz](../../reporting-services/technical-reference-ssrs.md).  
  
### <a name="native-mode-with-sharepoint-web-parts"></a>Einheitlicher Modus mit SharePoint-Webparts

 Reporting Services stellt zwei Webparts bereit, die Sie auf einer Instanz von [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 2.0 oder höher bzw. [!INCLUDE[spPortalServ](../../includes/spportalserv-md.md)] 2003 oder höher installieren und registrieren können. Sie können die Webparts von einer SharePoint-Website aus verwenden, um Berichte zu suchen und anzuzeigen, die auf einem Berichtsserver im einheitlichen Modus gespeichert und verarbeitet werden. Diese Webparts wurden in früheren Releases von Reporting Services eingeführt.  
  
## <a name="sharepoint-mode"></a>SharePoint-Modus

 Im SharePoint-Modus muss ein Berichtsserver als Teil einer SharePoint-Serverfarm ausgeführt werden. Die Verarbeitungs-, Rendering- und Verwaltungsfunktionen des Berichtsservers werden durch einen SharePoint-Anwendungsserver dargestellt, der den gemeinsamen Reporting Services-SharePoint-Dienst und mindestens eine Reporting Services-Dienstanwendung ausführt. Eine SharePoint-Website stellt den Front-End-Zugriff auf Berichtsserverinhalt und -vorgänge bereit.  
  
 Der SharePoint-Modus erfordert:  
  
-   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] oder [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
-   Eine angemessene Version des Reporting Services-Add-Ins für SharePoint 2010-Produkte.  
  
-   Ein SharePoint-Anwendungsserver, auf dem der gemeinsame Reporting Services-Dienst installiert ist, und mindestens eine Reporting Services-Dienstanwendung.  
  
 Im Folgende wird eine Reporting Services-Umgebung im SharePoint-Modus abgebildet:  
  
 ![Funktionale SSRS Sharepoint-Architektur](../../reporting-services/report-server-sharepoint/media/rs-sharepoint-architecture.gif "SSRS SharePoint Functional Architecture")  
  
||Description|  
|-|-----------------|  
|**(1)**|Webserver oder Web-Front-Ends (WFE). Das Reporting Services-Add-In muss auf jedem Webserver installiert sein, von dem aus Sie die Webanwendungsfunktionen nutzen möchten, beispielsweise Berichte oder Reporting Services-Verwaltungsseiten für Tasks (z.B. das Verwalten von Datenquellen oder Abonnements) anzeigen.|  
|**(2)**|Mit dem Add-In werden URL- und SOAP-Endpunkte für die Kommunikation der Clients mit den Anwendungsservern über den Reporting Services-Dienstproxy installiert.|  
|**(3)**|Anwendungsserver, auf denen der gemeinsame Reporting Services-Dienst ausgeführt wird. Die horizontale Skalierung der Berichtsverarbeitung wird im Rahmen der SharePoint-Farm und durch das Hinzufügen des Reporting Services-Dienstes zu zusätzlichen Anwendungsservern verwaltet.|  
|**(4)**|Sie können mehrere Reporting Services-Dienstanwendungen mit unterschiedlichen Konfigurationen erstellen, einschließlich Berechtigungen, E-Mails, Proxy und Abonnements.|  
|**(5)**|Berichte, Datenquellen und andere Elemente werden in den SharePoint-Inhaltsdatenbanken gespeichert.|  
|**(6)**|Reporting Services-Dienstanwendungen erstellen drei Datenbanken für Berichtsserver-, Temp- und Datenwarnungsfunktionen. Konfigurationseinstellungen, die für alle SSRS-Dienstanwendungen gelten, werden in der Datei **RSReportserver.config** gespeichert.|  
  
## <a name="report-process-and-schedule-and-delivery-process"></a>Berichtsprozess und Zeitplanungs- und Übermittlungsprozess

 Der Berichtsserver enthält zwei Verarbeitungsmodule, die die vorbereitende Berichtsverarbeitung und die Zwischenberichtsverarbeitung sowie Zeitplanungs- und Übermittlungsvorgänge ausführen. Der Berichtsprozessor ruft die Berichtsdefinition oder das Berichtsmodell ab, kombiniert die Layoutinformation mit Daten der Datenverarbeitungserweiterung und rendert sie im gewünschten Format. Der Zeitplanungs- und Übermittlungsprozess verarbeitet Berichte, die durch einen Zeitplan ausgelöst werden, und übermittelt Berichte an Ziele.  
  
## <a name="report-server-database"></a>Berichtsserver-Datenbank

 Der Berichtsserver ist ein statusloser Server, der alle Eigenschaften, Objekte und Metadaten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank speichert. Zu den gespeicherten Daten gehören veröffentlichte Berichte, kompilierte Berichte, Berichtsmodelle und die Ordnerhierarchie, die die Adressierung für alle vom Berichtsserver verwalteten Elemente bereitstellt. Eine Berichtsserver-Datenbank kann internen Speicher für eine einzelne Reporting Services-Installation oder für mehrere Berichtsserver bereitstellen, die Teil einer Bereitstellung für horizontales Skalieren sind. Wenn Sie einen Berichtsserver für die Ausführung in einer großen Bereitstellung eines SharePoint-Produkts oder einer SharePoint-Technologie konfigurieren, verwendet der Berichtsserver die SharePoint-Datenbanken zusätzlich zur Berichtsserver-Datenbank. Weitere Informationen zu Datenspeichern in einer Reporting Services-Installation finden Sie unter [Report Server Database &#40;SSRS Native Mode&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md).  
  
## <a name="authentication-rendering-data-and-delivery-extensions"></a>Authentifizierungs-, Rendering-, Daten- und Übermittlungserweiterungen

 Der Berichtsserver unterstützt die folgenden Erweiterungsarten: Authentifizierungserweiterungen, Datenverarbeitungserweiterungen, Berichtsverarbeitungserweiterungen, Renderingerweiterungen und Übermittlungserweiterungen. Ein Berichtsserver erfordert mindestens eine Authentifizierungserweiterung, Datenverarbeitungserweiterung und Renderingerweiterung. Übermittlungserweiterungen und benutzerdefinierte Berichtsverarbeitungserweiterungen sind zwar optional, jedoch erforderlich, wenn Sie die Berichtsverteilung oder benutzerdefinierte Steuerelemente unterstützen möchten.  
  
 Reporting Services bietet Standarderweiterungen, damit Sie alle Serverfunktionen verwenden können, ohne benutzerdefinierte Komponenten entwickeln zu müssen. In der folgenden Tabelle werden die Standarderweiterungen beschrieben, die zu einer vollständigen Berichtsserverinstanz beitragen, die einsatzbereite Funktionen bietet:  
  
|Typ|Standardwert|  
|----------|-------------|  
|Authentifizierung|Eine Standard-Berichtsserverinstanz unterstützt die Windows-Authentifizierung, einschließlich Identitätswechsel- und Delegationsfunktionen, falls diese in Ihrer Domäne aktiviert sind.|  
|Datenverarbeitung|Eine Standard-Berichtsserverinstanz bietet Datenverarbeitungserweiterungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-, Oracle-, Hyperion Essbase-, SAPBW-, OLE DB-, Parallel Data Warehouse- und ODBC-Datenquellen.|  
|Rendering|Eine Standard-Berichtsserverinstanz bietet Renderingerweiterungen für die Dateiformate HTML, Excel, CSV, XML, Word und PDF sowie für SharePoint-Listen und Bilddateien.|  
|Delivery|Eine Standard-Berichtsserverinstanz schließt eine E-Mail-Übermittlungserweiterung und eine Dateifreigabe-Übermittlungserweiterung ein. Falls der Berichtsserver für die SharePoint-Integration konfiguriert ist, können Sie eine Übermittlungserweiterung verwenden, die Berichte in eine SharePoint-Bibliothek speichert.|  
  
> [!NOTE]  
>  Reporting Services umfassen einen vollständigen Satz von Tools und Anwendungen, die Sie zum Verwalten des Servers, Erstellen von Inhalt und Verfügbarmachen dieses Inhalts für die Benutzer in Ihrem Unternehmen verwenden können.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben

 Die folgenden Themen enthalten zusätzliche Informationen zum Installieren, Verwenden und Verwalten eines Berichtsservers:  
  
|Task|Link|  
|----------|----------|  
|Prüfen Sie die Hardware- und Softwareanforderungen.|[Hardware and Software Requirements for Reporting Services in SharePoint Mode](http://msdn.microsoft.com/library/ed91877d-4f74-4266-a932-b824b4810c99).|  
|Installieren Sie Reporting Services im SharePoint-Modus.|[Installieren des SharePoint-Modus von Reporting Services für SharePoint 2010](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)|  
|Wenn Sie ein Webentwickler sind oder Erfahrung im Erstellen von Cascading Stylesheets haben, können Sie auf eigenes Risiko die Standardstile ändern, um Farben, Schriftarten und Layout der Symbolleiste oder des Berichts-Managers zu ändern. In dieser Version sind weder die Standardstylesheets noch Anweisungen zum Ändern der Stylesheets dokumentiert.|[Anpassen von Stylesheets für den HTML-Viewer und Berichts-Manager](http://msdn.microsoft.com/library/df805cff-b1de-4062-b2ac-423f37390fbd)|  
|Entwickler von Websites, die sich mit HTML-Formaten und Cascading Style Sheets (CSS) auskennen, können anhand der Informationen in diesem Thema ermitteln, welche Dateien geändert werden können, um die Darstellung des Berichts-Managers anzupassen.|[Konfigurieren des Webportals für die Übergabe von benutzerdefinierten Authentifizierungscookies](assetid:///91aeb053-149e-4562-ae4c-a688d0e1b2ba)|  
|Erläutert, wie die Speichereinstellungen für den Report Server-Webdienst und den Windows-Dienst angepasst werden können.|[Konfigurieren von verfügbarem Speicher für Berichtsserveranwendungen](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)|  
|Erläutert empfohlene Schritte zur Konfiguration des Berichtsservers für die Remoteverwaltung.|[Konfigurieren eines Berichtsservers für die Remoteverwaltung](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)|  
|Stellt Anweisungen zum Konfigurieren der Verfügbarkeit von **Meine Berichte** auf einer einheitlichen Berichtsserverinstanz bereit.|[Aktivieren und Deaktivieren von "Meine Berichte"](../../reporting-services/report-server/enable-and-disable-my-reports.md)|  
|Stellt Anweisungen zum Einrichten des RSClientPrint-Steuerelements bereit, das Druckfunktionen innerhalb unterstützter Browser bereitstellt. Weitere Informationen zu den Browseranforderungen von finden Sie unter [Browserunterstützung für Reporting Services und Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).|[Enable and Disable Client-Side Printing for Reporting Services (Aktivieren und Deaktivieren des clientseitige Drucks für Reporting Services)](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)|  

## <a name="next-steps"></a>Nächste Schritte

[Erweiterungen für Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)   
[Reporting Services-Tools](../../reporting-services/tools/reporting-services-tools.md)   
[Abonnements und Übermittlung &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
[Berichtsserver-Datenbank &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[Implementieren von Sicherheitserweiterungen](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
[Implementieren von Datenverarbeitungserweiterungen](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
[Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)   

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
