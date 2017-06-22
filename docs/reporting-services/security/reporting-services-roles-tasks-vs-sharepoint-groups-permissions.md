---
title: Reporting Services-Rollen-Tasks im Vergleich zu SharePoint-Gruppen-Berechtigungen | Microsoft Docs
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
- security [Reporting Services], tasks
- roles [Reporting Services], predefined
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], predefined roles
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 429f1dbb-183a-4097-bd1b-693da9fe7a36
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 779105655150aae2f1397865c67f8e835fd99646
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="reporting-services-roles-tasks-vs-sharepoint-groups-permissions"></a>Reporting Services-Rollen-Tasks im Vergleich zu SharePoint-Gruppen-Berechtigungen
  In diesem Thema werden rollen- und taskbasierte Autorisierungsfunktionen im einheitlichen Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mit den Sicherheitsfunktionen in SharePoint-Produkten verglichen. In diesem Thema werden die Terminologie und Merkmale von Rollen, Tasks, SharePoint-Gruppen, Berechtigungsstufen und Berechtigungen verglichen.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Modus &#124; SharePoint 2010 und SharePoint 2013<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Einheitlicher Modus|  
  
 **In diesem Thema:**  
  
-   [Vergleich zwischen Berechtigungstools und zugehöriger Terminologie](#bkmk_compare_tools_terms)  
  
-   [Vergleich zwischen Rollen im einheitlichen Modus und SharePoint-Gruppen](#bkmk_compare_roles_groups)  
  
-   [Vergleich zwischen Tasks im einheitlichen Modus und SharePoint-Berechtigungen](#bkmk_compare_tasks_permissions)  
  
##  <a name="bkmk_compare_tools_terms"></a> Vergleich zwischen Berechtigungstools und zugehöriger Terminologie  
 **Einheitlicher Modus:** Die Berechtigungsobjekte von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus (Rollen und Tasks) werden in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellt und im Berichts-Manager für einzelne Benutzer konfiguriert.  
  
 **SharePoint mode:** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint mode utilizes the SharePoint permission features. SharePoint-Gruppen und -Berechtigungen werden auf der folgenden Seite für **Siteeinstellungen** verwaltet.  
  
 In der folgenden Tabelle werden die Objekte und Konzepte von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus und SharePoint im Hinblick auf Berechtigungen verglichen.  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Einheitlicher Modus|SharePoint|  
|---------------------------------------------|----------------|  
|**Rolle:** Beispielsweise "Inhalts-Manager".|**Gruppe:** Beispielsweise die Standardgruppe "Anzeigende Benutzer".|  
|---|**Berechtigungsstufe der Gruppe:** Beispielsweise "Nur anzeigen" für die Gruppe "Anzeigende Benutzer".|  
|**Tasks:** Beispielsweise "Berichte verwalten".|**Berechtigungen:** Die Gruppe "Nur anzeigen" enthält beispielsweise listenbezogene Berechtigungen für die Elemente, Versionen und Anwendungsseiten von Sichten.|  
  
 Weitere Informationen zu SharePoint-Berechtigungen finden Sie unter [Berechtigungsstufen und Berechtigungen](http://office.microsoft.com/windows-sharepoint-services-help/permission-levels-and-permissions-HA010100149.aspx) und [Bestimmen von Berechtigungsstufen und Gruppen in SharePoint 2013](http://technet.microsoft.com/library/cc262690.aspx).  
  
##  <a name="bkmk_compare_roles_groups"></a> Vergleich zwischen Rollen im einheitlichen Modus und SharePoint-Gruppen  
 Die folgende Tabelle enthält eine Gegenüberstellung der vordefinierten Rollendefinitionen in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus und der SharePoint-Standardgruppen. Wenn die SharePoint-Gruppen nicht mit der von Ihnen gewünschten Rolle übereinstimmen, können Sie eine benutzerdefinierte Gruppe erstellen und in SharePoint Berechtigungsstufen zuweisen.  
  
 **Hinweis**: Die verfügbaren SharePoint-Standardgruppen hängen von der Websitevorlage ab, die verwendet wird, um die SharePoint-Website zu erstellen.  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Rolle|SharePoint-Gruppen|  
|--------------------------------------|-----------------------|  
|**Browser**<br /><br /> Sicht|Verwenden Sie die Gruppe **Besucher** , um Berechtigungen zum Anzeigen von Berichten zu erteilen. Die Gruppe **Besucher** verfügt über die Berechtigungsstufe Lesen, mit der Gruppenmitglieder Seiten, Listenelemente und Dokumente anzeigen können.|  
|**Inhalts-Manager**<br /><br /> Volle Berechtigungen für alle Elemente und Vorgänge auf Elementebene, einschließlich Berechtigungen zum Festlegen der Sicherheit.|Mit der Gruppe **Besitzer** gewähren Sie volle Kontrolle über die Verwaltung von Berichtsserverelementen auf einer SharePoint-Website. Die Gruppe **Besitzer** verfügt über die Berechtigungen Vollzugriff, mit denen Gruppenmitglieder Änderungen am Websiteinhalt, einzelnen Webseiten oder der Funktionalität vornehmen können. Der Vollzugriff sollte nur Websiteadministratoren gewährt werden.|  
|**Meine Berichte**|Es ist keine entsprechende Gruppe vorhanden. **Meine Berichte** wird auf einem Berichtsserver, der im SharePoint-Modus ausgeführt wird, nicht unterstützt. Wenn Sie eine entsprechende Funktionalität wünschen, können Sie die Funktionen für Meine Website [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] in  verwenden.|  
|**Verleger**<br /><br /> Berichte, Berichtsmodelle, freigegebene Datenquellen und Ressourcen hinzufügen, aktualisieren, anzeigen und löschen.|Mit der Gruppe **Mitglieder** erteilen Sie Berechtigungen zum Hinzufügen von Elementen, Bearbeiten von Elementen und Aktualisieren von Verweisen auf abhängige Elemente auf einer SharePoint-Website. Die Gruppe **Mitglieder** verfügt über die Berechtigungsebene Teilnehmen, mit der Gruppenmitglieder Seiten anzeigen, Elemente hinzufügen und aktualisieren sowie Änderungen zur Genehmigung übermitteln können.|  
|**Berichts-Generator**<br /><br /> Berichte anzeigen, einzelne Abonnements selbst verwalten und Berichte im Berichts-Generator öffnen.|Der Berichtsdefinition Berichts-Generator entspricht keine vordefinierte Berechtigungsebene oder SharePoint-Gruppe. In der Standardeinstellung verfügen Benutzer, die der Gruppe **Mitglieder** oder **Besitzer** angehören, über die Berechtigung zum Verwenden des Berichts-Generators. Wenn Sie den Berichts-Generator anderen Benutzern zur Verfügung stellen möchten, sollten Sie benutzerdefinierte Sicherheitseinstellungen erstellen, um eine Berechtigungsebene bereitzustellen, die den Funktionen der Berichts-Generator-Rolle ähnelt. Weitere Informationen finden Sie unter [Festlegen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md).|  
|-|Verwenden Sie die Gruppe **Anzeigende Benutzer** , um Berechtigungen zum Anzeigen gerenderter Berichte zu erteilen. Mitglieder der Gruppe **Anzeigende Benutzer** sind nicht in der Lage, den Inhalt von Berichtselementen herunterzuladen oder anzuzeigen.<br /><br /> **Hinweis:** Ab SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]hat die Gruppe **Viewer** keine Berechtigungen zur Erstellung von Abonnements.|  
|**Systembenutzer** und **Systemadministrator**|Diese Rollen sind für einen Berichtsserver, der im SharePoint-Modus ausgeführt wird, nicht erforderlich. **Systembenutzer** und **Systemadministrator** entsprechen den SharePoint-Berechtigungen auf Farm- oder Webanwendungsebene. Der Berichtsserver stellt keine Funktionalität bereit, die eine Autorisierung auf dieser Ebene erfordert.|  
  
##  <a name="bkmk_compare_tasks_permissions"></a> Vergleich zwischen Tasks im einheitlichen Modus und SharePoint-Berechtigungen  
 Die folgende Tabelle enthält eine Gegenüberstellung der Tasks von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus und SharePoint-Berechtigungen. In der Spalte **Typ** ist angegeben, ob sich der Task im einheitlichen Modus auf eine Systemrolle oder Standardrolle und zugehörige Elemente bezieht. Mit Systemrollen werden Berechtigungen auf Systemebene verwaltet, beispielsweise freigegebene Zeitpläne.  
  
|Task im einheitlichen Modus|Rollentyp|Entsprechende SharePoint-Berechtigung|  
|----------------------|---------------|--------------------------------------|  
|Berichte lesen|Element|Elemente bearbeiten, Elemente anzeigen|  
|Verknüpfte Berichte erstellen|Element|Nicht unterstützt.|  
|Alle Abonnements verwalten|Element|Benachrichtigungen verwalten|  
|Datenquellen verwalten|Element|Elemente hinzufügen, Elemente bearbeiten, Elemente löschen, Elemente anzeigen|  
|Ordner verwalten|Element|Elemente hinzufügen, Elemente bearbeiten, Elemente löschen, Elemente anzeigen|  
|Einzelne Abonnements verwalten|Element|Elemente bearbeiten<br /><br /> Vor [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]lautete die erforderliche Berechtigungsstufe "Warnungen erstellen".|  
|Modelle verwalten|Element|Elemente hinzufügen, Elemente bearbeiten, Elemente löschen, Elemente anzeigen|  
|Berichtsverlauf verwalten|Element|Elemente bearbeiten, Versionen anzeigen, Versionen löschen|  
|Berichte verwalten|Element|Elemente hinzufügen, Elemente bearbeiten, Elemente löschen, Elemente anzeigen|  
|Ressourcen verwalten|Element|Elemente hinzufügen, Elemente bearbeiten, Elemente löschen, Elemente anzeigen|  
|Sicherheit für einzelne Elemente festlegen|Element|Berechtigungen verwalten|  
|Datenquellen anzeigen|Element|Elemente anzeigen|  
|Ordner anzeigen|Element|Elemente anzeigen|  
|Modelle anzeigen|Element|Elemente anzeigen|  
|Berichte anzeigen|Element|Elemente anzeigen|  
|Ressourcen anzeigen|Element|Elemente anzeigen|  
||||  
|Berichtsdefinitionen ausführen|System|Elemente anzeigen|  
|Ereignisse generieren|System|Website verwalten|  
|Aufträge verwalten|System|Keine (nicht unterstützt)|  
|Berichtsservereigenschaften verwalten|System|Keine (nicht zutreffend) Es wird vom Berichtsserver nicht kontrolliert, ob ein Benutzer über die Berechtigung zum Anzeigen der Integrationseinstellungen in der Zentraladministration verfügt.|  
|Rollen verwalten|System|Berechtigungen verwalten|  
|Freigegebene Zeitpläne verwalten|System|Website verwalten, öffnen|  
|Berichtsserversicherheit verwalten|System|Keine (nicht zutreffend) Für den Berichtsserver werden auf einem Server, der im integrierten SharePoint-Modus ausgeführt wird, keine Rollenzuweisungen auf Systemebene verwendet.|  
|Berichtsservereigenschaften anzeigen|System|Keine (nicht zutreffend) Es wird vom Berichtsserver nicht kontrolliert, ob ein Benutzer über die Berechtigung zum Anzeigen der Integrationseinstellungen in der Zentraladministration verfügt.|  
|Freigegebene Zeitpläne anzeigen|System|Elemente öffnen|  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Festlegen von Berechtigungen für Berichtsservervorgänge in einer SharePoint-Webanwendung](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Rollendefinitionen](../../reporting-services/security/role-definitions.md)   
 [Vordefinierte Rollen](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
