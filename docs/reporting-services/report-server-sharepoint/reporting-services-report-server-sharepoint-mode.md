---
title: Reporting Services-Berichtsserver (SharePoint-Modus) | Microsoft Docs
ms.custom: 
ms.date: 09/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a8cd1bd00ec92535fff73c5eaa4ff9bbe9274ef2
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---

# <a name="reporting-services-report-server-sharepoint-mode"></a>Reporting Services-Berichtsserver (SharePoint-Modus)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Einem Reporting Services-Berichtsserver konfiguriert für **SharePoint-Modus** lässt sich innerhalb einer Bereitstellung eines SharePoint-Produkts ausführen. Ein Berichtsserver im SharePoint-Modus kann die Funktionen für Zusammenarbeit und Verwaltung von SharePoint für Berichte und andere [!INCLUDE[ssRSnfoversion_md](../../includes/ssrsnoversion-md.md)] -Inhaltstypen verwenden. SharePoint-Modus erfordert die entsprechende Version des Reporting Services-add-Ins für SharePoint-Produkte installieren, auf den SharePoint-Web-Front-Ends.  
  
> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.

 Weitere Informationen zur Installation und Konfiguration finden Sie unter:  
  
-   [Installieren von Reporting Services SharePoint-Modus für SharePoint 2010](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c).  
  
-   [Hinzufügen eines zusätzlichen Berichtsservers zu einer Farm](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
  
## <a name="feature-summary"></a>Zusammenfassung der Funktionen

 Wenn Sie einen Berichtsserver für die Ausführung im integrierten SharePoint-Modus konfigurieren, wird die folgende Funktionalität bereitgestellt, die nur verfügbar ist, wenn ein Berichtsserver in diesem Modus bereitgestellt wird.  
  
-   Verwenden von SharePoint-Funktionen für Dokumentverwaltung und Zusammenarbeit, einschließlich Warnungen. Eine SharePoint-Website stellt ein einheitliches Portal für den zentralen Zugriff und die zentrale Verwaltung aller Berichtselemente bereit.  
  
-   Verwenden von SharePoint-Berechtigungen und Authentifizierungsanbietern, um den Zugriff auf Berichte, Modelle und andere Elemente zu steuern.  
  
-   Verwenden von SharePoint-Bereitstellungstopologien, um Berichte über eine Internetverbindung jenseits der Firewall zu verteilen. Ein Berichtsserver stellt Berichts- und Datenverarbeitungsdienste im Kontext einer größeren SharePoint-Bereitstellung zur Verfügung, die für den Internetzugriff konfiguriert ist.  
  
-   Verwalten von Berichten, Modellen, Datenquellen, Zeitplänen und Berichtsverläufen in benutzerdefinierten Anwendungsseiten auf einer SharePoint-Website. Auf einer SharePoint-Website können Sie genauso vorgehen, um Eigenschaften festzulegen, Zeitpläne und Abonnements zu definieren und Berichtsverläufe zu erstellen und zu verwalten, wie Sie sie von anderen Tools in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kennen.  
  
-   Veröffentlichen oder Hochladen von Berichten, Berichtsmodellen, Ressourcen und freigegebenen Datenquellendateien in einer bzw. auf eine SharePoint-Bibliothek, einschließlich des Berichtscenters in Office SharePoint Server.  
  
     Verwenden Sie den Berichts-Designer, Modell-Designer und Berichts-Generator zum Erstellen von Berichten und Datenquellen, die direkt in einer SharePoint-Bibliothek veröffentlicht werden sollen. Sie können darüber hinaus die Uploadaktion für eine SharePoint-Website verwenden, um beliebige Berichtsdefinitionen und Berichtsmodelle zu einer SharePoint-Bibliothek hinzuzufügen.  
  
     Da der Berichtsserver Berichtsdefinitionen unabhängig vom verwendeten Servermodus verarbeitet, hat der Servermodus keinen Einfluss auf die Berichtsdaten und das Layout. Jeder Bericht, der auf einem Berichtsserver im einheitlichen Modus ausgeführt werden kann, kann auch auf einem Berichtsserver ausgeführt werden, der für den integrierten SharePoint-Modus konfiguriert ist.  
  
-   Abonnieren und Übermitteln von Berichten an eine SharePoint-Bibliothek mithilfe einer neuen SharePoint-Übermittlungserweiterung. Sie können Berichte per E-Mail oder in einen freigegebenen Ordner übermitteln. Die Berichtsserver-Übermittlungserweiterungen werden zum Übermitteln von Berichten verwendet. Sie können datengesteuerte Abonnements für eine umfangreiche Berichtsverteilung mit Abonnentendaten erstellen, die zur Laufzeit abgefragt werden.  
  
-   Ein Berichts-Viewer-Webpart können Sie SharePoint-Seiten zum Anzeigen eines Berichts in der SharePoint-Webanwendung hinzufügen. Der Webpart schließt Seitennavigation, Suche, Druck und Exportieren von Funktionen.  
  
-   Programmieren im Hinblick auf einen neuen SOAP-Endpunkt, um benutzerdefinierte Anwendungen zu erstellen, die in eine SharePoint-Website integriert werden. Sie können auch den aktualisierten WMI-Anbieter (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation) verwenden, um eine Berichtsserverinstanz programmgesteuert zu konfigurieren, die im integrierten SharePoint-Modus ausgeführt wird.  
  
-   Microsoft Access Services-Berichterstellung im verbundenen Modus.  
  
-   AAM-Zonen, Bereitstellungen mit Internetzugriff und SharePoint-Benutzertoken für SharePoint-Listen.  
  
## <a name="connected-mode-and-local-mode"></a>Verbundener Modus und im lokalen Modus

 Ab SQL Server 2008 R2 ist zum Anzeigen von Berichten von SharePoint 2010-Servern, auf denen das Microsoft SQL Server 2008 R2 Reporting Services-Add-In (oder höher) für SharePoint 2010-Produkte installiert ist, ein neuer *lokaler Modus* verfügbar.  
  
-   *Im lokalen Modus*: im lokalen Modus können Berichte lokal von der SharePoint-Dokumentbibliothek, ohne Kombination mit einem Reporting Services-Berichtsserver gerendert werden. Die Reporting Services-add-in für SharePoint-Produkte ist erforderlich, aber ein Reporting Services-Berichtsserver ist nicht. Das Add-In lässt sich auf verschiedene Weise installieren, einschließlich mithilfe des Vorbereitungstools für SharePoint 2010-Produkte. Weitere Informationen zum lokalen Modus finden Sie unter [lokaler Modus vs. verbundener Modus Berichte im Berichts-Viewer](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md) und [, wo Sie das Reporting Services-add-in für SharePoint-Produkte finden](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
-   *Verbundener Modus*: im verbundener Modus wird durch die Integration von einem Reporting Services-Berichtsserver in der SharePoint-Farm mithilfe der SharePoint-Zentraladministration unterstützt. Die Kombination mit einem Berichtsserver ermöglicht vollständige End-to-End-Berichterstellung, indem die Zusammenarbeitsfunktionen von SharePoint 2010 und die serverbasierten Funktionen eines Berichtservers bereitgestellt werden, einschließlich Abonnements, Momentaufnahmen und serverbasierte Verarbeitung.  
  
## <a name="unsupported-sharepoint-features"></a>Nicht unterstützte SharePoint-Funktionen

 Nicht alle SharePoint-Funktionen stehen für integrierte Vorgänge zur Verfügung. Im folgenden finden eine Liste der SharePoint-Funktionen, denen Reporting Services nicht direkt integriert sind:  
  
-   Secure Store Service.  
  
-   Sie können die SharePoint-Integration für den Outlook-Kalender oder den SharePoint-Zeitplan nicht für Reporting Services-Dateien in einer Dokumentbibliothek verwenden.  
  
-   SharePoint Business Data-Katalog.  
  
-   SharePoint-Personalisierung wird auf den Reporting Services-Seiten auch nicht unterstützt. Die Berichtsserverintegration wird nicht unterstützt, wenn die SharePoint-Webanwendung für den anonymen Zugriff aktiviert ist.  
  
-   SQL Server Reporting Services unterstützt **keine** Versionskontrolle für die SharePoint-Dokumentbibliothek. Wenn Sie Berichtselemente in einer Dokumentbibliothek speichern, die mit aktiviertem "Dokumentversionsverlauf" konfiguriert ist, funktionieren die Reporting Services-Funktionen nicht ordnungsgemäß und erzeugen Fehler im ULS-Protokoll. Das folgende Beispiel veranschaulicht einen Fehler im ULS-Protokoll:  
  
    -   "…Eine Datenquelle, die dem Bericht zugeordnet ist, wurde deaktiviert."  
  
     Der Versionsverlauf von Dokumentbibliotheken wird unter Bibliothekseinstellungen auf der Seite Versionierungseinstellungen konfiguriert.  
  
## <a name="supported-combinations-of-the-sharepoint-add-in-and-report-server"></a>Unterstützte Kombinationen des SharePoint-add-in und Bericht-Servers

 Nicht alle Funktionen werden in allen Kombinationen von Berichtsserver, Reporting Services-Add-In für SharePoint und SharePoint-Produkten unterstützt. Weitere Informationen finden Sie unter [unterstützte Kombinationen von SharePoint- und Reporting Services-Server und -add-in](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  Die richtige Version des Reporting Services-Add-Ins muss mit der entsprechenden Version von SharePoint-Produkten verwendet werden.  
  
## <a name="components-that-provide-integration"></a>Komponenten, die Integration ermöglichen

 Um die Server in einer einzelnen Bereitstellung kombinieren, integrieren Sie eine Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services mit einer Instanz von SharePoint-Produkte  
  
 Integration erfolgt über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und das Reporting Services-Add-in für SharePoint-Produkte. Das Reporting Services-Add-in die ist eine kostenlos erhältliche Komponente, die Sie herunterladen und installieren Sie dann auf einem Server mit der entsprechenden Version von SharePoint aus.  
  
> [!TIP]  
>  Nicht alle Funktionen werden in allen Kombinationen von Berichtsserver, Reporting Services-Add-In für SharePoint und SharePoint-Produkten unterstützt. Weitere Informationen finden Sie unter [unterstützte Kombinationen von SharePoint- und Reporting Services-Server und -add-in](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).  
  
-   In SharePoint bietet das Reporting Services-Add-in der ReportServer-Proxyendpunkt, ein Berichts-Viewer-Webpart und Anwendungsseiten, damit Sie anzeigen, speichern und verwalten berichtsserverinhalte auf einer SharePoint-Website oder-Farm.  
  
-   In Reporting Services stellt aktualisierte Programmdateien, einen SOAP-Endpunkt, und benutzerdefinierte Sicherheit und übermittlungserweiterungen. Der Berichtsserver muss für die Ausführung im integrierten SharePoint-Modus konfiguriert werden und dient ausschließlich dazu, den Zugriff auf Berichte und ihre Übermittlung über eine SharePoint-Website zu unterstützen.  
  
 Nachdem Sie das Reporting Services-Add-in für SharePoint installieren und konfigurieren die beiden Server für die Integration, können Sie hochladen oder Berichtsserver-Inhaltstypen auf einer SharePoint-Bibliothek veröffentlichen, und klicken Sie dann anzeigen und verwalten diese Dokumente aus einer SharePoint-Website. Das Hochladen und Veröffentlichen von berichtsserverinhalten ist ein wichtiger erster Schritt; das Webpart und Seiten sind verfügbar, bei der Wahl von Berichtsdefinitionen (RDL), Berichtsmodelle (SMDL) und freigegebene Datenquellen (rsds) auf einer SharePoint-Website.  
  
##  <a name="language-considerations"></a>Sprachbezogene Aspekte

 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] und [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Produkte sind in mehr Sprachen als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Wenn Sie einen Berichtsserver für die Ausführung innerhalb einer Bereitstellung eines SharePoint-Produkts konfigurieren, wird möglicherweise eine Kombination von Sprachen angezeigt. Benutzeroberfläche, Dokumentation und Meldungen werden in den folgenden Sprachen angezeigt:  
  
-   Alle Anwendungsseiten, Tools, Fehler, Warnungen und Meldungen, die von Reporting Services stammen erscheint in der von der Reporting Services-Instanz in einem der verwendeten Sprache der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sprachen.  
  
-   Anwendungsseiten, die Sie auf einer SharePoint-Website, die Berichts-Viewer-Webpart und der Berichts-Generator zu öffnen, werden in einem der unterstützten Sprachen für das Reporting Services-Add-in angezeigt. Um die Liste der unterstützten Sprachen anzuzeigen, wechseln Sie zu [SQL Server-downloads](http://msdn.microsoft.com/sql/downloads/) und suchen die Downloadseite für das SQL Server 2016 Reporting Services Add-in.  
  
-   SharePoint-Websites, die SharePoint-Zentraladministration, die Onlinehilfe und Meldungen sind in den Sprachen verfügbar, die von Office Server-Produkten unterstützt werden.  
  
 Wenn die Sprache Ihres SharePoint-Produkt oder eine Technologie von der berichtsserversprache abweicht, versucht Reporting Services, eine Sprache aus derselben Sprachfamilie zu verwenden, die bestmögliche Übereinstimmung bereitstellt. Falls keine geeignete Ersatzsprache verfügbar ist, verwendet der Berichtsserver Englisch.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben

 In der folgenden Tabelle werden die Aufgaben im Zusammenhang mit einem Berichtsserver für Reporting Services SharePoint-Modus zusammengefasst:  
  
|**Task**|**Link**|  
|--------------|--------------|  
|Ausführliche Schritte zum Installieren und Konfigurieren von Reporting Services im SharePoint-Modus.|[Installieren von Reporting Services SharePoint-Modus für SharePoint 2010](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c) und [Hinzufügen eines zusätzlichen Berichtsservers zu einer Farm](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).|  
|Horizontale Skalierung der Reporting Services-SharePoint-Bereitstellung durch zusätzliche Berichtsserver hinzufügen.|[Hinzufügen eines zusätzlichen Berichtsservers zu einer Farm](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) und [Bereitstellungstopologien für SQL Server BI-Funktionen in SharePoint](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26).|  
|Fügen Sie zusätzliche SharePoint Web-Front-Ends, die die Reporting Services-Komponenten, die für die Berichtsanzeige und Elemente installiert sein.|[Hinzufügen eines zusätzlichen Reporting Services-Webs-Front-End zu einer farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Konfigurieren von E-mail für den Berichtsserver in SharePoint.|[Konfigurieren von E-mail für eine Reporting Services-dienstanwendung](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|
|Neueste Informationen für diese Version, siehe TechNet Wiki.|[SQL Server 2012 Reporting Services-Tipps, Tricks und Problembehandlung](http://go.microsoft.com/fwlink/?LinkId=221297).|  

## <a name="next-steps"></a>Nächste Schritte

[Installieren oder Deinstallieren von Reporting Services Sdd-in für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
[Berichts-Viewer-Webpart auf einer SharePoint-Website](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
[Quiz: Konfigurieren von SSRS 2012 für die SharePoint-integration](http://go.microsoft.com/fwlink/?LinkId=306443)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

