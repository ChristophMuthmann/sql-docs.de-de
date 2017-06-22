---
title: Reporting Services-Berichtsserver (SharePoint-Modus) | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 10778ec9-5fe4-4b4e-89b0-ade1f06b781d
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a633c14ae598d3535acc4f721ae5ae392f91a6a2
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---

# <a name="reporting-services-report-server-sharepoint-mode"></a>Reporting Services-Berichtsserver (SharePoint-Modus)

  Ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver, der für den **SharePoint-Modus** konfiguriert ist, lässt sich innerhalb der Bereitstellung eines SharePoint-Produkts ausführen. Ein Berichtsserver im SharePoint-Modus kann die Funktionen für Zusammenarbeit und Verwaltung von SharePoint für Berichte und andere [!INCLUDE[ssRSnfoversion_md](../../includes/ssrsnoversion-md.md)] -Inhaltstypen verwenden. Der SharePoint-Modus erfordert die Installation der entsprechenden Version des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-Ins für SharePoint-Produkte auf den SharePoint-Web-Front-Ends.  
  
 Weitere Informationen zur Installation und Konfiguration finden Sie unter:  
  
-   [Installieren des SharePoint-Modus von Reporting Services für SharePoint 2010](http://msdn.microsoft.com/en-us/47efa72e-1735-4387-8485-f8994fb08c8c).  
  
-   [Hinzufügen eines zusätzlichen Berichtsservers zu einer Farm &#40;Horizontales Skalieren für SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
  
 Informationen zu den Neuerungen in diesem Release finden Sie im Abschnitt „SharePoint“ in [Neues bei Reporting Services &#40;SSRS&#41;](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).  
  
 In diesem Thema:  
  
-   [Zusammenfassung der Funktionen](#bkmk_featuresum)  
  
-   [Verbundener Modus und lokaler Modus](#bkmk_connectedandlocal)  
  
-   [Nicht unterstützte SharePoint-Funktionen](#bkmk_unsupportedsharepoint)  
  
-   [Unterstützte Kombinationen des SharePoint-Add-Ins und Berichtsservers](#bkmk_supportedcombinations)  
  
-   [Komponenten, die die Integration ermöglichen](#bkmk_components)  
  
-   [Sprachbezogene Aspekte](#bkmk_language)  
  
-   [Verwandte Aufgaben](#bkmk_relatedtasks)  
  
##  <a name="bkmk_featuresum"></a> Zusammenfassung der Funktionen  
 Wenn Sie einen Berichtsserver für die Ausführung im integrierten SharePoint-Modus konfigurieren, wird die folgende Funktionalität bereitgestellt, die nur verfügbar ist, wenn ein Berichtsserver in diesem Modus bereitgestellt wird.  
  
-   Verwenden von SharePoint-Funktionen für Dokumentverwaltung und Zusammenarbeit, einschließlich Warnungen. Eine SharePoint-Website stellt ein einheitliches Portal für den zentralen Zugriff und die zentrale Verwaltung aller Berichtselemente bereit.  
  
-   Verwenden von SharePoint-Berechtigungen und Authentifizierungsanbietern, um den Zugriff auf Berichte, Modelle und andere Elemente zu steuern.  
  
-   Verwenden von SharePoint-Bereitstellungstopologien, um Berichte über eine Internetverbindung jenseits der Firewall zu verteilen. Ein Berichtsserver stellt Berichts- und Datenverarbeitungsdienste im Kontext einer größeren SharePoint-Bereitstellung zur Verfügung, die für den Internetzugriff konfiguriert ist.  
  
-   Verwalten von Berichten, Modellen, Datenquellen, Zeitplänen und Berichtsverläufen in benutzerdefinierten Anwendungsseiten auf einer SharePoint-Website. Auf einer SharePoint-Website können Sie genauso vorgehen, um Eigenschaften festzulegen, Zeitpläne und Abonnements zu definieren und Berichtsverläufe zu erstellen und zu verwalten, wie Sie sie von anderen Tools in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kennen.  
  
-   Veröffentlichen oder Hochladen von Berichten, Berichtsmodellen, Ressourcen und freigegebenen Datenquellendateien in einer bzw. auf eine SharePoint-Bibliothek, einschließlich des Berichtscenters in Office SharePoint Server.  
  
     Verwenden Sie den Berichts-Designer, Modell-Designer und Berichts-Generator zum Erstellen von Berichten und Datenquellen, die direkt in einer SharePoint-Bibliothek veröffentlicht werden sollen. Sie können darüber hinaus die Uploadaktion für eine SharePoint-Website verwenden, um beliebige Berichtsdefinitionen und Berichtsmodelle zu einer SharePoint-Bibliothek hinzuzufügen.  
  
     Da der Berichtsserver Berichtsdefinitionen unabhängig vom verwendeten Servermodus verarbeitet, hat der Servermodus keinen Einfluss auf die Berichtsdaten und das Layout. Jeder Bericht, der auf einem Berichtsserver im einheitlichen Modus ausgeführt werden kann, kann auch auf einem Berichtsserver ausgeführt werden, der für den integrierten SharePoint-Modus konfiguriert ist.  
  
-   Abonnieren und Übermitteln von Berichten an eine SharePoint-Bibliothek mithilfe einer neuen SharePoint-Übermittlungserweiterung. Sie können Berichte per E-Mail oder in einen freigegebenen Ordner übermitteln. Die Berichtsserver-Übermittlungserweiterungen werden zum Übermitteln von Berichten verwendet. Sie können datengesteuerte Abonnements für eine umfangreiche Berichtsverteilung mit Abonnentendaten erstellen, die zur Laufzeit abgefragt werden.  
  
-   Ein Berichts-Viewer-Webpart, den Sie SharePoint-Seiten hinzufügen können, um in der SharePoint-Webanwendung einen Bericht anzuzeigen. Der Webpart schließt Funktionen für Seitennavigation, Suche, Druck und Export ein.  
  
-   Programmieren im Hinblick auf einen neuen SOAP-Endpunkt, um benutzerdefinierte Anwendungen zu erstellen, die in eine SharePoint-Website integriert werden. Sie können auch den aktualisierten WMI-Anbieter (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation) verwenden, um eine Berichtsserverinstanz programmgesteuert zu konfigurieren, die im integrierten SharePoint-Modus ausgeführt wird.  
  
-   Microsoft Access Services-Berichterstellung im verbundenen Modus.  
  
-   AAM-Zonen, Bereitstellungen mit Internetzugriff und SharePoint-Benutzertoken für SharePoint-Listen.  
  
##  <a name="bkmk_connectedandlocal"></a> Verbundener Modus und lokaler Modus  
 Ab SQL Server 2008 R2 ist zum Anzeigen von Berichten von SharePoint 2010-Servern, auf denen das Microsoft SQL Server 2008 R2 Reporting Services-Add-In (oder höher) für SharePoint 2010-Produkte installiert ist, ein neuer *lokaler Modus* verfügbar.  
  
-   *Lokaler Modus*: Im lokalen Modus können Berichte lokal von der SharePoint-Dokumentbibliothek gerendert werden, ohne Kombination mit einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver. Das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint-Produkte ist erforderlich, ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver jedoch nicht. Das Add-In lässt sich auf verschiedene Weise installieren, einschließlich mithilfe des Vorbereitungstools für SharePoint 2010-Produkte. Weitere Informationen zum lokalen Modus finden Sie unter [Berichte im lokalen Modus im Vergleich mit Berichten im verbundenen Modus im Berichts-Viewer &#40;Reporting Services im SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md) und [Verfügbarkeit des Reporting Services-Add-Ins für SharePoint-Produkte](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
-   *Verbundener Modus*: Der verbundene Modus wird durch Integration eines [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsservers mit der SharePoint-Zentraladministration in die SharePoint-Farm unterstützt. Die Kombination mit einem Berichtsserver ermöglicht vollständige End-to-End-Berichterstellung, indem die Zusammenarbeitsfunktionen von SharePoint 2010 und die serverbasierten Funktionen eines Berichtservers bereitgestellt werden, einschließlich Abonnements, Momentaufnahmen und serverbasierte Verarbeitung.  
  
##  <a name="bkmk_unsupportedsharepoint"></a> Nicht unterstützte SharePoint-Funktionen  
 Nicht alle SharePoint-Funktionen stehen für integrierte Vorgänge zur Verfügung. Im Folgenden finden Sie eine Liste der SharePoint-Funktionen, die keine direkte Integration in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aufweisen:  
  
-   Secure Store Service.  
  
-   Sie können die SharePoint-Integration für den Outlook-Kalender oder den SharePoint-Zeitplan nicht für Reporting Services-Dateien in einer Dokumentbibliothek verwenden.  
  
-   SharePoint Business Data-Katalog.  
  
-   Die SharePoint-Personalisierung wird auf den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Seiten ebenfalls nicht unterstützt. Die Berichtsserverintegration wird nicht unterstützt, wenn die SharePoint-Webanwendung für den anonymen Zugriff aktiviert ist.  
  
-   SQL Server Reporting Services unterstützt **keine** Versionskontrolle für die SharePoint-Dokumentbibliothek. Wenn Sie Berichtselemente in einer Dokumentbibliothek speichern, die mit aktiviertem "Dokumentversionsverlauf" konfiguriert ist, funktionieren die Reporting Services-Funktionen nicht ordnungsgemäß und erzeugen Fehler im ULS-Protokoll. Das folgende Beispiel veranschaulicht einen Fehler im ULS-Protokoll:  
  
    -   "…Eine Datenquelle, die dem Bericht zugeordnet ist, wurde deaktiviert."  
  
     Der Versionsverlauf von Dokumentbibliotheken wird unter Bibliothekseinstellungen auf der Seite Versionierungseinstellungen konfiguriert.  
  
##  <a name="bkmk_supportedcombinations"></a> Unterstützte Kombinationen des SharePoint-Add-Ins und Berichtsservers  
 Nicht alle Funktionen werden in allen Kombinationen von Berichtsserver, Reporting Services-Add-In für SharePoint und SharePoint-Produkten unterstützt. Weitere Informationen finden Sie unter [Unterstützte Kombinationen von SharePoint und Reporting Services-Server und -Add-In &#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  Die richtige Version des Reporting Services-Add-Ins muss mit der entsprechenden Version von SharePoint-Produkten verwendet werden.  
  
##  <a name="bkmk_components"></a> Komponenten, die die Integration ermöglichen  
 Sie können die Server in einer einzelnen Bereitstellung kombinieren, indem Sie eine Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in eine Instanz von SharePoint-Produkten integrieren.  
  
 Die Integration wird durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint-Produkte bereitgestellt. Das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In ist eine kostenlos erhältliche Komponente, die Sie herunterladen und dann auf einem Server installieren können, auf dem die richtige Version von SharePoint ausgeführt wird.  
  
> [!TIP]  
>  Nicht alle Funktionen werden in allen Kombinationen von Berichtsserver, Reporting Services-Add-In für SharePoint und SharePoint-Produkten unterstützt. Weitere Informationen finden Sie unter [Unterstützte Kombinationen von SharePoint und Reporting Services-Server und -Add-In &#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).  
  
-   In SharePoint stellt das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-In den ReportServer-Proxyendpunkt, ein Berichts-Viewer-Webpart und Anwendungsseiten bereit, sodass Sie Berichtsserverinhalte auf einer SharePoint-Website oder -Farm anzeigen, speichern und verwalten können.  
  
-   Auf [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stellt aktualisierte Programmdateien, einen SOAP-Endpunkt und benutzerdefinierte Sicherheit und Übermittlungserweiterungen bereit. Der Berichtsserver muss für die Ausführung im integrierten SharePoint-Modus konfiguriert werden und dient ausschließlich dazu, den Zugriff auf Berichte und ihre Übermittlung über eine SharePoint-Website zu unterstützen.  
  
 Nachdem Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In in SharePoint installiert und die beiden Server für die Integration konfiguriert haben, können Sie Berichtsserver-Inhaltstypen in eine SharePoint-Bibliothek hochladen und dort veröffentlichen und diese Dokumente anschließend von einer SharePoint-Website anzeigen und verwalten. Das Hochladen und Veröffentlichen von Berichtsserverinhalten ist ein wichtiger erster Schritt; der Webpart und die Anwendungsseiten werden verfügbar, wenn Sie Berichtsdefinitionen (RDL), Berichtsmodelle (SMDL) und freigegebene Datenquellen (RSDS) auf einer SharePoint-Website auswählen.  
  
##  <a name="bkmk_language"></a> Sprachbezogene Aspekte  
 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] und [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] -Produkte sind in mehr Sprachen als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Wenn Sie einen Berichtsserver für die Ausführung innerhalb einer Bereitstellung eines SharePoint-Produkts konfigurieren, wird möglicherweise eine Kombination von Sprachen angezeigt. Benutzeroberfläche, Dokumentation und Meldungen werden in den folgenden Sprachen angezeigt:  
  
-   Alle Anwendungsseiten, Tools, Fehler, Warnungen und Meldungen, die aus [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] stammen, werden in der Sprache angezeigt, die von der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz in einer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sprachen verwendet wird.  
  
-   Anwendungsseiten, die Sie auf einer SharePoint-Website öffnen, der Berichts-Viewer-Webpart und der Berichts-Generator werden in einer der unterstützten Sprachen für das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In angezeigt. Um die Liste der unterstützten Sprachen anzuzeigen, wechseln Sie zu [SQL Server-Downloads](http://msdn.microsoft.com/sql/downloads/) und suchen die Downloadseite für das SQL Server 2016 Reporting Services Add-in.  
  
-   SharePoint-Websites, die SharePoint-Zentraladministration, die Onlinehilfe und Meldungen sind in den Sprachen verfügbar, die von Office Server-Produkten unterstützt werden.  
  
 Wenn die Sprache Ihres SharePoint-Produkts oder der SharePoint-Technologie von der Berichtsserversprache abweicht, versucht [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , eine Sprache aus derselben Sprachfamilie zu verwenden, die der ursprünglichen Sprache am ähnlichsten ist. Falls keine geeignete Ersatzsprache verfügbar ist, verwendet der Berichtsserver Englisch.  
  
##  <a name="bkmk_relatedtasks"></a> Verwandte Aufgaben  
 In der folgenden Tabelle sind die Aufgaben zusammengefasst, die sich auf einen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver im SharePoint-Modus beziehen:  
  
|**Task**|**Link**|  
|--------------|--------------|  
|Ausführliche Schritte zum Installieren und Konfigurieren von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus.|[Installieren des SharePoint-Modus von Reporting Services für SharePoint 2010](http://msdn.microsoft.com/en-us/47efa72e-1735-4387-8485-f8994fb08c8c) und [Hinzufügen eines zusätzlichen Berichtsservers zu einer Farm &#40;Horizontales Skalieren für SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).|  
|Nehmen Sie eine horizontale Skalierung für Ihre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-SharePoint-Bereitstellung vor, indem Sie zusätzliche Berichtsserver hinzufügen.|[Hinzufügen eines zusätzlichen Berichtsservers zu einer Farm &#40;Horizontales Skalieren für SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) und [Bereitstellungstopologien für SQL Server BI-Funktionen in SharePoint](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26).|  
|Fügen Sie zusätzliche SharePoint Web-Front-Ends hinzu, auf denen die zum Anzeigen und Melden von Elementen erforderlichen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Komponenten installiert sind.|[Hinzufügen eines zusätzlichen Reporting Services-Web-Front-Ends zu einer Farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Konfigurieren Sie E-Mail für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Datenwarnungen und -Abonnementfunktionen.|[Konfigurieren von E-Mail für eine Reporting Services-Dienstanwendung &#40;SharePoint 2010 und SharePoint 2013&#41;](https://msdn.microsoft.com/library/hh231673.aspx)|  
|Neueste Informationen für diese Version, siehe TechNet Wiki.|[SQL Server 2012 Reporting Services – Tipps, Tricks und Problembehandlung](http://go.microsoft.com/fwlink/?LinkId=221297).|  

## <a name="next-steps"></a>Nächste Schritte

[Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
[Berichts-Viewer-Webpart auf einer SharePoint-Website](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
[Quiz: Konfigurieren von SSRS 2012 für die SharePoint-Integration](http://go.microsoft.com/fwlink/?LinkId=306443)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
