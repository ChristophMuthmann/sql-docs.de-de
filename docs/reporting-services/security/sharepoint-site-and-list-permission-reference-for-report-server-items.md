---
title: "SharePoint-Website Referenz- und Listenberechtigungen für Berichtsserverelemente | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
- permission sets [Reporting Services]
ms.assetid: 1fcb27bd-4c4a-43f4-bfff-e42a59c87c49
caps.latest.revision: 14
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ca45a9fc4c37798983c4cc8956fbb27828a5ff01
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="sharepoint-site-and-list-permission-reference-for-report-server-items"></a>Referenz zu SharePoint-Website- und Listenberechtigungen für Berichtsserverelemente
  Dieses Thema bietet eine Referenz zu den Berechtigungen in SharePoint, mit denen Sie für einen im integrierten SharePoint-Modus ausgeführten Berichtsserver Zugriff auf Berichtsservervorgänge gewähren können. Wenn Sie benutzerdefinierte Berechtigungsebenen erstellen, können Sie mithilfe dieses Themas die zu verwendenden Berechtigungen auswählen.  
  
 SharePoint stellt 33 Berechtigungen bereit, mit denen Sie den Zugriff auf Inhalte und Vorgänge steuern können. Einige, aber nicht alle Berechtigungen gelten für Dokumente und Vorgänge, an denen ein Berichtsserver von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] beteiligt ist. Mithilfe der Berechtigungsverweistabellen in diesem Artikel können Sie herausfinden, welche Berechtigungen berichtsspezifische Aufgaben unterstützen.  
  
 Jede Tabelle beginnt mit einer Liste der SharePoint-Berechtigungen und einer Beschreibung. Die Tabelle enthält drei Spalten, die angeben, wie eine Berechtigung in vordefinierten Berechtigungsebenen verwendet wird. Die vordefinierten Berechtigungsstufen umfassen:  
  
|Berechtigungsstufe|Abkürzung|  
|----------------------|------------------|  
|Vollzugriff|**V**|  
|Mitwirken|**C**|  
|Besucher|**B**|  
  
 Berechtigungen, die sich nicht auf Berichtsserver auswirken, werden nicht aufgelistet. Personalisierungsberechtigungen sind von diesem Artikel ausgeschlossen. Obwohl Sie Berichtsserverelemente in eine personalisierte Website einfügen können, werden Personalisierungsanforderungen oder -vorgänge nicht direkt vom Berichtsserver verarbeitet.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Modus &#124; SharePoint 2010 and SharePoint 2013.|  
  
## <a name="list-permissions"></a>Listenberechtigungen  
 Mit den Berechtigungen, die Sie für die Bibliothek festlegen, die Berichtsserverelemente enthält, legen Sie fest, wie Benutzer auf diese Elemente zugreifen.  
  
|Berechtigung|Description|V|C|B|Berichtsservervorgang|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|Listen verwalten|Listen erstellen oder löschen, Spalten einer Liste erstellen oder löschen und öffentliche Sichten einer Liste hinzufügen oder löschen.|X|||Während eines Veröffentlichungsvorgangs von einem Erstellungstool aus einen Ordner in einer SharePoint-Bibliothek erstellen. Diese Berechtigung wird auch zum Verwalten des Berichtsverlaufs benötigt.|  
|Elemente hinzufügen|Listen Elemente hinzufügen, Dokumentbibliotheken Dokumente hinzufügen und Webdiskussionskommentare hinzufügen.|X|X||SharePoint-Bibliotheken Berichte, Berichtsmodelle, freigegebene Datenquellen und Ressourcen (externe Bilddateien) hinzufügen. Freigegebene Datenquellen erstellen. Berichtsmodelle aus freigegebenen Datenquellen generieren. Den Berichts-Generator starten und einen neuen Bericht erstellen oder ein Modell in den Berichts-Generator laden.|  
|Elemente bearbeiten|Elemente in Listen, Dokumente in Dokumentbibliotheken und Webdiskussionskommentare in Dokumenten bearbeiten sowie Webpartseiten in Dokumentbibliotheken anpassen.<br /><br /> Abonnements erstellen und eigene Abonnements bearbeiten.|X|X||Ältere Versionen eines Dokuments, einschließlich Momentaufnahmen des Berichtsverlaufs, anzeigen. Bearbeiten Elementeigenschaften für Berichte und andere Dokumente. Berichtsverarbeitungsoptionen festlegen. Parameter für einen Bericht festlegen. Datenquelleneigenschaften bearbeiten. Berichtsverlaufs-Momentaufnahmen erstellen. Öffnen Sie ein Berichtsmodell oder einen modellbasierten Bericht im Berichts-Generator, und speichern Sie die Änderungen an der Datei. Berichte mit Durchklicken Entitäten in einem Modell zuweisen. Eine Berichtsdefinition, eine freigegebene Datenquelle, ein Berichtsmodell oder eine Ressource durch eine neuere Version ersetzen (Datei ersetzen, Metadaten beibehalten). Abhängige Elemente, auf die in einem Bericht oder Modell verwiesen wird, verwalten. Das Berichts-Viewer-Webpart in Bezug auf einen bestimmten Bericht anpassen.<br /><br /> Abonnements erstellen, ändern und löschen, für die Berichte mithilfe der Übermittlungserweiterungen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] an Zielstandorte übermittelt werden. Diese Aktionen können nur vom Abonnementbesitzer sowie Benutzern ausgeführt werden, die über die Berechtigung Benachrichtigungen verwalten verfügen.|  
|Elemente löschen|Elemente aus Listen, Dokumente aus Dokumentbibliotheken und Webdiskussionskommentare aus Dokumenten löschen.|X|X||Berichte, Berichtsmodelle, freigegebene Datenquellen und andere Dokumente aus einer Bibliothek löschen.|  
|Elemente anzeigen|Elemente in Listen, Dokumente in Dokumentbibliotheken und Webdiskussionskommentare anzeigen.|X|X|X|Einen Bericht, ein Berichtsmodell und andere Dokumente öffnen und auf dem Berichtsserver verarbeiten.|  
|Elemente öffnen|Die Quelle von Dokumenten mit serverseitigen Dateihandlern anzeigen.|X|X|X|Eine Liste der freigegebenen Datenquellen anzeigen. Eine Kopie der Quelldatei für eine Berichtsdefinition oder ein Berichtsmodell herunterladen. Berichte mit Durchklicken anzeigen, in denen ein Berichtsmodell als Datenquelle verwendet wird.|  
|Versionen anzeigen|Ältere Versionen eines Listenelements oder Dokuments anzeigen.|X|X|X|Ältere Versionen eines Dokuments und Berichtsmomentaufnahmen anzeigen.|  
|Versionen löschen|Ältere Versionen eines Listenelements oder Dokuments löschen.|X|X||Ältere Versionen eines Dokuments und Berichtsmomentaufnahmen löschen.|  
  
> [!NOTE]  
>  Zu den Listenberechtigungen gehören weiterhin Auschecken überschreiben, Elemente genehmigen und Anwendungsseiten anzeigen. Diese Berechtigungen werden vom Berichtsserver nicht ausgewertet. Diese Vorgänge werden nicht vom Berichtsserver durchgeführt.  
  
## <a name="site-permissions"></a>Websiteberechtigungen  
 Websiteberechtigungen steuern den Zugriff auf Berichtsservervorgänge, die nicht direkt mit den in einer spezifischen Bibliothek gespeicherten Elementen verbunden sind. Zu den Beispielen gehören das Erstellen und Verwalten freigegebener Zeitpläne, die von Elementen in einer Vielzahl von Bibliotheken verwendet werden können, und das Konfigurieren des Berichts-Viewer-Webparts, das in einer Website verwendet werden kann.  
  
|Berechtigung|Description|V|C|B|Berichtsservervorgang|  
|----------------|-----------------|-------|-------|-------|-----------------------------|  
|Berechtigungen verwalten|Berechtigungsebenen für die Website erstellen und ändern und Benutzern und Gruppen Berechtigungen zuweisen.|X|||Sie können Berechtigungen für alle Berichtsserverelemente und -vorgänge verwalten. Sie können Einstellungen für die Modellelementsicherheit festlegen.|  
|Website verwalten|Alle Verwaltungsaufgaben für die Website ausführen und Inhalte verwalten.|X|||Freigegebene Zeitpläne erstellen, ändern und löschen.|  
|Seiten hinzufügen und anpassen|HTML- oder Webpartseiten hinzufügen, ändern oder löschen, und die Website in einem mit [!INCLUDE[winSPServ](../../includes/winspserv-md.md)]kompatiblen Editor bearbeiten.|X|||Einen Berichts-Viewer-Webpart hinzufügen oder entfernen.|  
|Benutzerinformationen durchsuchen|Informationen über die Benutzer der Website anzeigen.|X|X|X|Suchen nach Berichten und anderen Elementen über verschiedene Sites, Bibliotheken und Ordner hinweg. Veröffentlichen von Berichten und anderen Elementen in einer Bibliothek.|  
|Berechtigungen auflisten|Berechtigungen für die Website, die Liste, den Ordner, das Dokument oder das Listenelement auflisten.|X|||Berechtigungen für alle Berichtsserverelemente lesen. Einen Bericht mit Durchklicken anzeigen, in dem ein Berichtsmodell mit Sicherheitseinstellungen für Modellelemente verwendet wird.|  
|Benachrichtigungen verwalten|Benachrichtigungen für alle Benutzer der Website verwalten.|X|||Abonnements auf einer Website erstellen, ändern und löschen.|  
|Remoteschnittstellen verwenden|Mit SOAP-, Web DAV- oder SharePoint Designer-Schnittstellen auf die Website zugreifen.|X|X|X|Wird zum Aufrufen des URL-Proxy-Endpunktes für den Berichtsserver verwendet.|  
|Öffnen|Eine Website, eine Liste oder einen Ordner öffnen und auf im Container enthaltene Elemente zugreifen.|X|X|X|Zeitpläne und Elementeigenschaften lesen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Vergleich zwischen Sie Rollen und Aufgaben in Reporting Services to SharePoint Groups and Permissions](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
