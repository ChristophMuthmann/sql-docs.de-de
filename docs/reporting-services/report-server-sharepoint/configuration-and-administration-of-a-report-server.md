---
title: Konfiguration und Verwaltung eines SQL Server Reporting Services-Berichtsservers | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server-sharepoint
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 35995be90a36fa2037d4f571b7af509afb271871
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="configuration-and-administration-of-a-sql-server-reporting-services-report-server"></a>Konfiguration und Verwaltung eines SQL Server Reporting Services-Berichtsservers

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services ist eine serverbasierte Berichtsplattform. Sie bietet zahlreiche einsatzbereite Tools und Dienste, die Ihnen dabei helfen, Berichte für Ihr Unternehmen zu erstellen, bereitzustellen und zu verwalten. Darüber hinaus ermöglichen Ihnen die Programmierfunktionen eine Erweiterung und individuelle Anpassung Ihrer Funktionen zur Berichterstellung. Sie können die Berichtsumgebung in ein SharePoint-Produkt integrieren, um die Vorteile der Zusammenarbeitsumgebung zu nutzen, die von SharePoint-Websites bereitgestellt wird.

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

Die folgenden Abschnitte enthalten Informationen zu Konzepten, Bereitstellungsszenarios, Verfahren usw. zum Integrieren der Reporting Services-Umgebung mit einem SharePoint-Produkt oder einer SharePoint-Technologie:  
  
-   Menüoptionen in einer SharePoint-Dokumentbibliothek  
  
    -   [Datenwarnungs-Manager für SharePoint-Benutzer](../../reporting-services/data-alert-manager-for-sharepoint-users.md)  
  
    -   [Erstellen und Verwalten von Abonnements für Berichtsserver im SharePoint-Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
    -   [Aktualisieren von Anmeldeinformationen in Berichtsdatenquellen von einer SharePoint-Website](../../reporting-services/report-data/update-credentials-in-report-data-sources-from-a-sharepoint-site.md)  
  
    -   [Verwalten von freigegebenen Datasets](../../reporting-services/report-data/manage-shared-datasets.md)  
  
    -   [Festlegen von Parametern für einen veröffentlichten Bericht &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)  
  
    -   [Festlegen von Verarbeitungsoptionen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
    -   [Optionen zur Cacheaktualisierung &#40;Berichts-Manager&#41;](http://msdn.microsoft.com/library/227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6)  
  
-   [Funktion zur Reporting Services-Websitesammlung](../../reporting-services/report-server-sharepoint/site-collection-features-reporting-services.md)  
  
-   [Aktivieren der Berichtsserver- und Power View-Integrationsfunktionen in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)  
  
-   [Einstellungen und Funktionen für Reporting Services-Websites &#40;SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)  
  
-   [Aktivieren der Funktion zur Synchronisierung der Berichtsserverdateien in der SharePoint-Zentraladministration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  
  
-   [Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
-   [Berichte im lokalen Modus im Vergleich mit Berichten im verbundenen Modus im Berichts-Viewer (Reporting Services im SharePoint-Modus)](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
-   [Hochladen von Dokumenten in eine SharePoint-Bibliothek &#40;Reporting Services im SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
-   [Festlegen von Verarbeitungsoptionen &#40;Reporting Services im integrierten SharePoint-Modus&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
 Weitere allgemeine Informationen zu Reporting Services finden Sie unter [Reporting Services](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation. Weitere Informationen zu anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten, -Tools und -Ressourcen finden Sie in der [SQL Server-Onlinedokumentation](../../sql-server/sql-server-technical-documentation.md).  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
