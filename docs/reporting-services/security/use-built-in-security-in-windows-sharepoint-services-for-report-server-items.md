---
title: "Verwenden der integrierten Sicherheit in Windows SharePoint Services für Berichtsserverelemente | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 9577e88d-c22b-4934-936f-e0f1400cedf5
caps.latest.revision: "14"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5c213a3cf52c65b83609bb5f7a0a1acc1cbbc906
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="use-built-in-security-in-windows-sharepoint-services-for-report-server-items"></a>Verwenden der integrierten Sicherheit in Windows SharePoint Services für Berichtsserverelemente
  SharePoint stellt integrierte Sicherheitsfunktionen bereit, mit denen Sie von SharePoint-Websites und -Bibliotheken auf Berichtsserverelemente zugreifen können. Wenn Sie Benutzern bereits Berechtigungen für Websites und Listen zugewiesen haben, verfügen diese Benutzer sofort, nachdem Sie die Integrationseinstellungen zwischen SharePoint und einem Berichtsserver konfiguriert haben, über Zugriff auf Berichtsserverelemente und -vorgänge.  
  
## <a name="securable-items"></a>Sicherbare Elemente  
 Für die Website oder Bibliothek definierte Berechtigungen können verwendet werden, um Zugriff auf Berichtsserverelemente zu gewähren. Wenn Sie jedoch einzelne Elemente sichern möchten, können Sie Berechtigungen für die folgenden Inhaltstypen festlegen:  
  
|Dateityp|Description|  
|---------------|-----------------|  
|RDL|Eine Berichtsdefinitionsdatei, die das Berichtslayout und die zum Abrufen von Daten verwendeten Befehle definiert. Eine Berichtsdefinition verwendet Datenquellen-Verbindungsinformationen, um beim Verarbeiten des Berichts Daten abzurufen. Wenn es sich bei der Berichtsdefinition um einen im Berichts-Generator erstellten Ad-hoc-Bericht handelt, wird dem Bericht eine Berichtsmodelldatei (SMDL) zugeordnet, in der der Gültigkeitsbereich für das Durchsuchen der Daten im gerenderten Bericht festgelegt wird.|  
|SMDL|Eine Berichtsmodelldatei, in der Datenstrukturen und ihre Beziehungen beschrieben werden. Sie wird zum Erstellen und Ausführen von Berichten des Berichts-Generators verwendet.|  
|RSDS|Eine freigegebene Datenquellendatei, in der Informationen zu Verbindungen mit einer externen Datenquelle angegeben werden. Sie wird von Berichtsdefinitionsdateien (RDL) und Berichtsmodelldateien (SMDL) verwendet. Für Berichtsmodelle werden immer RSDS-Dateien verwendet, um Informationen zu Verbindungen mit einer zugrunde liegenden Datenquelle abzurufen. Bei Berichtsdefinitionen können RSDS-Dateien oder in Datenquelleneigenschaften im Report definierte Verbindungsinformationen verwendet werden.|  
|.rsc|Eine Berichtsteildatei, die das Layout und die Struktur des Berichtselements oder der Datenregion definiert. Sie wird verwendet, um den Berichtsteil auf einem Server zu veröffentlichen, damit das Element von anderen Autoren des Berichts aus dem Berichtsteilkatalog wieder verwendet werden kann.|  
|.rsd|Eine freigegebene Datasetdatei, die Abfragesyntax und Eigenschaften für ein Dataset definiert. Freigegebene Datasets können freigegeben, gespeichert, verarbeitet und aus einem Bericht extern zwischengespeichert werden.|  
  
 Zeitpläne, Abonnements und Berichtsverläufe sind keine sicherungsfähigen Elemente. Sie können Berechtigungen für die Website oder Bibliothek festlegen, mit denen bestimmt wird, ob ein Benutzer Zeitpläne, Abonnements und Berichtsverläufe erstellen oder verwenden kann, aber sie können diese Elemente nicht direkt sichern.  
  
 Wenn Sie einzelne Elemente sichern möchten, wählen Sie das Element in der Bibliothek aus, klicken Sie auf den Pfeil nach unten, und wählen Sie **Berechtigungen verwalten**aus. Wählen Sie im Menü **Aktionen** den Befehl **Berechtigungen bearbeiten**aus.  
  
## <a name="using-built-in-groups-and-permission-levels-to-access-report-server-items"></a>Verwenden integrierter Gruppen und Berechtigungsebenen zum Zugriff auf Berichtsserverelemente  
 Wenn Sie die Vererbung von Berechtigungen und SharePoint-Standardgruppen verwenden, können Sie sofort, nachdem Sie die Integrationseinstellungen für den Berichtsserver und SharePoint-Instanzen konfiguriert haben, auf die meisten Berichtsservervorgänge zugreifen.  
  
 In SharePoint werden Standardgruppen bereitgestellt, die vordefinierten Berechtigungsstufen zugeordnet sind, durch die bestimmt wird, wie Sie auf Dokumente und Seiten auf einer SharePoint-Website zugreifen können. Wenn Sie Standardgruppen und standardmäßige Berechtigungsebenen verwenden und die Websites für das Erben von Berechtigungen konfiguriert sind, können Sie mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen normalerweise wie folgt arbeiten:  
  
|**SharePoint-Gruppen**|**Berechtigungsstufe**|**Zusammenfassung**|**Zugriff auf den Berichtsserver**|  
|---------------------------|--------------------------|-----------------|------------------------------|  
|**Besitzer**|Vollzugriff|Besitzer verfügen über vollständige Berechtigungen zum Erstellen, Verwalten und Sichern von Berichtsserverelementen und -vorgängen.|Legen Berechtigungen fest, die den Zugriff auf alle in Bibliotheken auf der gesamten Website gespeicherten Berichtsserverelemente steuern. Legen Berechtigungen innerhalb eines Berichtsmodells fest (auch als Modellelementsicherheit bezeichnet). Passen einen Berichts-Viewer-Webpart an. Fügen Berichte und andere Elemente zu Bibliotheken hinzu. Bearbeiten Elementeigenschaften für Berichte und andere Dokumente. Löschen Berichte und andere Elemente. Zeigen Berichte an, einschließlich Berichten, bei denen Berichtsmodelle für das Durchsuchen von Daten verwendet werden. Legen Parameter für Berichte fest. Legen Verarbeitungsoptionen für einen Bericht fest. Generieren Berichtsmodelle. Erstellen Berichte im Berichts-Generator. Erstellen und verwalten freigegebene Datenquellen. Erstellen, ändern und löschen Abonnements, die sich im Besitz beliebiger Benutzer befinden. Erstellen und verwalten freigegebene Zeitpläne, die auf der gesamten Website verwendet werden. Erstellen und verwalten Versionen eines Dokuments, einschließlich Berichtsverläufen. Laden die Quelldatei für eine Berichtsdefinition oder ein Berichtsmodell herunter. Ersetzen eine Berichtsdefinition, ein Berichtsmodell, eine freigegebene Datenquelle oder eine Ressource (wobei die Elementeigenschaften und Berechtigungen beibehalten werden).|  
|**Element**|Mitwirken|Mitglieder können neue Elemente erstellen und Elementberichte und Modelle aus Entwurfstools in einer SharePoint-Bibliothek veröffentlichen.|Fügen Berichte und andere Elemente zu Bibliotheken hinzu. Bearbeiten Elementeigenschaften für Berichte und andere Dokumente. Löschen Berichte und andere Elemente. Zeigen Berichte an, einschließlich Berichten, bei denen Berichtsmodelle für das Durchsuchen von Daten verwendet werden. Zeigen frühere Versionen eines Dokuments an, einschließlich Berichtsverlaufs-Momentaufnahmen (hierfür ist es erforderlich, dass ein Benutzer auch über die Berechtigung zum Öffnen des Berichts verfügt, für den der Berichtsverlauf erstellt wurde). Legen Parameter für Berichte fest. Legen Verarbeitungsoptionen für einen Bericht fest. Generieren Berichtsmodelle. Erstellen Berichte im Berichts-Generator. Erstellen und verwalten freigegebene Datenquellen. Erstellen, ändern und löschen Abonnements, die sich im Besitz des Benutzers befinden. Verwenden freigegebene Zeitpläne mit einem Abonnement. Erstellen und verwalten Versionen eines Dokuments, einschließlich Berichtsverläufen. Laden die Quelldatei für eine Berichtsdefinition oder ein Berichtsmodell herunter. Ersetzen eine Berichtsdefinition, ein Berichtsmodell, eine freigegebene Datenquelle oder eine Ressource (wobei die Elementeigenschaften und Berechtigungen beibehalten werden).|  
|**Besucher** und **Viewer**|Lesen|Besucher können Berichte anzeigen.|Zeigen Berichte an, einschließlich Berichten, bei denen Berichtsmodelle für das Durchsuchen von Daten verwendet werden.|  
  
 Wenn Sie die integrierten Gruppen und Berechtigungsebenen nicht verwenden, müssen Sie bestimmte Berechtigungen einschließen, um auf [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen zugreifen zu können. Weitere Informationen finden Sie unter [Festlegen von Berechtigungen für Berichtsservervorgänge in einer SharePoint-Webanwendung](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Vergleichen der Rollen und Aufgaben in Reporting Services mit SharePoint-Gruppen und -Berechtigungen](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Festlegen von Berechtigungen für Berichtsservervorgänge in einer SharePoint-Webanwendung](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Granting Permissions on Report Server Items on a SharePoint Site (Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website)](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
