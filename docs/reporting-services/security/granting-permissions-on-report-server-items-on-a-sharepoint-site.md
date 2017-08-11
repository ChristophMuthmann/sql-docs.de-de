---
title: "Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- permissions [Reporting Services], native mode
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 0eb2f34a-3643-4b03-81c2-5741ba7ebefd
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b785da81bc694c8442d2a7a618e2abe8f1cec907
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="granting-permissions-on-report-server-items-on-a-sharepoint-site"></a>Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[SPF2010](../../includes/spf2010-md.md)] stellt integrierte Sicherheitsfunktionen, die Sie verwenden können, um den Zugriff auf berichtsserverelemente zu gewähren, die Sie von SharePoint-Websites und Bibliotheken zu erreichen. Wenn Sie Benutzern bereits Berechtigungen zugewiesen haben, verfügen diese Benutzer sofort, nachdem Sie die Integrationseinstellungen zwischen [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] und einem Berichtsserver konfiguriert haben, über Zugriff auf Berichtsserverelemente und -vorgänge. Mit den vorhandenen Berechtigungen können Sie Berichtsdefinitionen und andere Dokumente hochladen, Berichte anzeigen, Abonnements erstellen und Elemente verwalten.  
  
 Wenn keine Berechtigungen zugewiesen wurden oder Sie mit den Sicherheitsfunktionen von [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]nicht vertraut sind, beachten Sie folgende Hinweise:  
  
1.  Informieren Sie sich in der Produktdokumentation zu [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]über die Standardsicherheitseinstellungen für die SharePoint-Standardgruppen, um Berechtigungen und Benutzerzugriff verwalten zu können.  
  
2.  Überprüfen Sie die Liste der Berechtigungen, die sich speziell auf den Zugriff auf Berichtsserverelemente und -vorgänge auswirken. Weitere Informationen finden Sie unter [Verwenden der integrierten Sicherheit in Windows SharePoint Services für Berichtsserverelemente](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md).  
  
3.  Weisen Sie Benutzer- und Gruppenkonten vordefinierten SharePoint-Gruppen zu.  
  
4.  Optional können Sie neue Berechtigungsebenen und -gruppen erstellen oder vorhandene ändern, um bei besonderen Anforderungen die Berechtigungen für den Serverzugriff zu modifizieren.  
  
 Sie können die Sicherheitsfunktionen von [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] nur mit Berichtsserverelementen verwenden, wenn Sie über einen Berichtsserver verfügen, der im integrierten SharePoint-Modus ausgeführt wird.  
  
## <a name="about-permissions-permission-levels-and-sharepoint-groups"></a>Informationen zu Berechtigungen, Berechtigungsebenen und SharePoint-Gruppen  
 Die folgende Liste bietet eine kurze Einführung in die Sicherheitsfunktionen von [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]. Weitere Informationen finden Sie auf der SharePoint-Website unter "Windows SharePoint Help and How-to" (in Englisch).  
  
-   Zu sicherungsfähigen Objekten zählen Websites, Listen, Bibliotheken, Ordner und Dokumente.  
  
-   Eine Berechtigung ist eine Autorisierung zur Ausführung einer bestimmten Task. [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] stellt 33 vordefinierte Berechtigungen bereit, die Sie in einer Berechtigungsstufe kombinieren können.  
  
-   Eine Berechtigungsebene besteht aus einem Satz von Berechtigungen, die Benutzern oder SharePoint-Gruppen für ein sicherungsfähiges Objekt, z. B. eine Website, eine Bibliothek, eine Liste, einen Ordner, ein Element oder ein Dokument gewährt werden können. Diese Ebene entspricht einer Rollendefinition in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Fünf Berechtigungsebenen sind vordefiniert. Diese können Sie bei Bedarf anpassen, Sie können jedoch auch neue erstellen.  
  
-   Als SharePoint-Gruppe wird eine Gruppe von Benutzern bezeichnet, die Sie zur Verwaltung der Berechtigungen für eine SharePoint-Website und zum Bereitstellen einer E-Mail-Verteilerliste für Websitemitglieder erstellen können. Eine SharePoint-Gruppe besteht aus Windows-Benutzer- und Gruppenkonten oder Benutzeranmeldungen, wenn Sie die Formularauthentifizierung verwenden. In [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] werden drei Gruppen bereitgestellt. Diese können Sie bei Bedarf anpassen, Sie können jedoch auch neue erstellen.  
  
-   Mithilfe der Berechtigungsvererbung können Unterwebsites, Listen, Bibliotheken und Elemente die Sicherheitseinstellungen der übergeordneten Website erben. Mit geerbten Berechtigungen können Sie auf in einer SharePoint-Bibliothek gespeicherte Berichtsserverelemente zugreifen. Durch Berechtigungsvererbung und vordefinierte SharePoint-Gruppen kann die Bereitstellung vereinfacht und unmittelbarer Zugriff auf die meisten Berichtsservervorgänge gewährt werden.  
  
## <a name="who-sets-permissions"></a>Wer Berechtigungen festgelegt  
 Der Administrator, der [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]installiert, den SharePoint-Konfigurationsassistenten ausführt und die Portalwebsite erstellt, ist der Standardbesitzer der Portalwebsite. Der Websitebesitzer kann in der Zentraladministration Berechtigungen für eine Farm oder eine eigenständige SharePoint-Webanwendung und auf der Stammwebsite Berechtigungen für jede SharePoint-Webanwendung festlegen. Diese Person kann auch weitere Websitebesitzer ernennen.  
  
 Auf der Stammwebsite einer SharePoint-Webanwendung können Administratoren von Websitesammlungen Berechtigungen für mehrere Websites in der gesamten Websitehierarchie festlegen. Die einzelnen Websitebesitzer können für eine Unterwebsite jeweils die gleichen Aufgaben ausführen.  
  
 Ein Serveradministrator oder Administrator einer Websitesammlung kann bestimmte Optionen festlegen, um zu bestimmen, ob andere Besitzer Berechtigungen festlegen können. Je nach der Ihnen zugewiesenen Berechtigungsebene können Sie möglicherweise keine SharePoint-Gruppen oder Berechtigungsebenen erstellen oder anpassen.  
  
## <a name="using-predefined-sharepoint-groups-and-permission-levels"></a>Verwenden vordefinierter SharePoint-Gruppen und Berechtigungsebenen  
 In der Produktdokumentation zu [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] wird empfohlen, SharePoint-Standardgruppen zu verwenden (d.h. *Besitzer von* **Websitename**, *Besitzer von* **Websitename**und *Besitzer von* **Websitename**) und Berechtigungen auf der Websiteebene zuzuweisen. Den meisten Benutzern sollten Sie Berechtigungen als Mitglieder der Gruppen *Besucher von* **Websitename** oder *Besucher von* **Websitename** zuweisen. Berechtigungen für die übergeordnete Website werden von der gesamten Websitehierarchie geerbt. Die Vererbung der Berechtigungen können Sie für bestimmte Elemente unterbrechen, für die zusätzliche Einschränkungen erforderlich sind.  
  
 Den aufgeführten SharePoint-Gruppen sind die folgenden vordefinierten Berechtigungsebenen zugeordnet:  
  
-   Die Gruppe **Besitzer** verfügt über die Berechtigungen Vollzugriff, mit denen Gruppenmitglieder Änderungen am Websiteinhalt, an einzelnen Webseiten oder an der Funktionalität vornehmen können. Der Vollzugriff sollte nur Websiteadministratoren gewährt werden.  
  
-   Die Gruppe **Mitglieder** verfügt über die Berechtigungsebene Teilnehmen, mit der Gruppenmitglieder Seiten anzeigen, Elemente bearbeiten, Änderungen zur Genehmigung übermitteln sowie Elemente einer Liste hinzufügen und in dieser löschen können.  
  
-   Die Gruppe **Besucher** verfügt über die Berechtigungsstufe Lesen, mit der Gruppenmitglieder Seiten, Listenelemente und Dokumente anzeigen können.  
  
 Die SharePoint-Gruppen verfügen über Berechtigungsebenen, die unmittelbaren Zugriff auf viele Berichtsservervorgänge bieten. Wenn mit den integrierten Sicherheitseinstellungen nicht die von Ihnen benötigte Zugriffsebene gewährt wird, können Sie benutzerdefinierte Gruppen oder Berechtigungsebenen erstellen.  
  
 Weitere Informationen zu den von den Standardsicherheitsfunktionen unterstützten Berichtsservervorgängen finden Sie unter [Verwenden der integrierten Sicherheit in Windows SharePoint Services für Berichtsserverelemente](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md).  
  
 Die integrierten Sicherheitsfunktionen können von den SharePoint-Gruppen nur verwendet werden, wenn Sie diesen Windows-Benutzer- oder Gruppenkonten zugewiesen haben. Mit Ausnahme des Serveradministrators und des Besitzers der Portalwebsite, die beim Installieren der Software automatisch Zugriffsberechtigungen für [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] erhalten, müssen allen Benutzern Berichtigungen für den Serverzugriff gewährt werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Verwenden der integrierten Sicherheit in Windows SharePoint Services für Berichtsserverelemente](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
 Erläutert, wie mit den vordefinierten SharePoint-Gruppen und Berechtigungsebenen auf Berichtsserverelemente zugegriffen werden kann.  
  
 [SharePoint-Website Referenz- und Listenberechtigungen für Berichtsserverelemente](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
 Bietet eine Referenz zu allen SharePoint-Produktberechtigungen, die es erlauben, auf Berichtsservervorgänge zuzugreifen.  
  
 [Festlegen von Berechtigungen für Berichtsservervorgänge in einer SharePoint-Webanwendung](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)  
 Beschreibt die Berechtigungsanforderungen für die Ad-hoc-Berichterstellung und enthält empfohlene Vorgehensweisen für die Verfügbarmachung von Funktionen.  
  
 [Vergleich zwischen Sie Rollen und Aufgaben in Reporting Services to SharePoint Groups and Permissions](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
 Stellt eine kurze Zusammenfassung von SharePoint-Gruppen im Vergleich mit vordefinierten Rollendefinitionen in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bereit.  
  
 [Festlegen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website &#40; Reporting Services in SharePoint integrierten Modus &#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)  
 Enthält Anweisungen zum Erstellen neuer SharePoint-Gruppen, die über die Berechtigung verfügen, den Berichts-Generator zu starten und die Modellelementsicherheit festzulegen. Dieses Thema enthält zudem allgemeine Richtlinien zum Festlegen benutzerdefinierter Berechtigungen für beliebige Berichtsserverelemente oder -vorgänge.  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheit und Schutz für Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md)  
  
  
