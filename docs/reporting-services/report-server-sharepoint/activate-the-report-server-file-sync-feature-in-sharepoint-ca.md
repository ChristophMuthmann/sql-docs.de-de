---
title: Aktivieren des Features zur Synchronisierung der Berichtsserverdateien in SharePoint | Microsoft-Dokumentation
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
ms.openlocfilehash: 3dfceec4c00d396d98584f4eeca630e8ccfb90ea
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint"></a>Aktivieren der Funktion zur Synchronisierung der Berichtsserverdateien

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktion zur Synchronisierung der Berichtsserverdateien verwendet SharePoint-Ereignishandler, um den Berichtsserverkatalog mit Elementen in Dokumentbibliotheken zu synchronisieren. Diese Funktion ist nützlich, wenn Benutzer veröffentlichte Berichtselemente häufig direkt in die SharePoint-Dokumentbibliotheken hochladen. Wenn die Dateisynchronisierungsfunktion nicht aktiviert ist, werden Inhalte weiterhin synchronisiert. Dies erfolgt allerdings nicht so häufig.

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.
  
 Die Funktion zur Synchronisierung der Berichtsserverdateien kann in der SharePoint-Websiteverwaltung aktiviert werden, nachdem Sie das [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] -Add-In für SharePoint-Produkte installiert haben.  
  
 Die Funktion kann für einzelne Websites manuell aktiviert und deaktiviert werden, jedoch nicht auf Ebene der Websitesammlung.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten

 Das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint muss installiert sein. Falls das Add-In nicht installiert ist, wird die Dateisynchronisierungsfunktion nicht in der Funktionsliste der Website angezeigt.  
  
 Um die Installation zu überprüfen, zeigen Sie die Liste der installierten Anwendungen in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows- **Systemsteuerung**an. Wenn das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In installiert ist, folgen Sie den Anweisungen in diesem Thema, um die Funktion zur Synchronisierung von Berichtsserverdateien zu aktivieren.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>So aktivieren oder deaktivieren Sie die Funktion zur Synchronisierung der Berichtsserverdateien auf einer Website
  
1.  Klicken Sie auf der Hauptseite der Website auf das Menü **Websiteaktionen** , und klicken Sie dann auf **Siteeinstellungen**.  
  
2.  Klicken Sie im Bereich **Websiteaktionen** auf **Websitefunktionen verwalten**.  
  
3.  Suchen Sie **Synchronisierung der Berichtsserverdateien** in der Liste.  
  
4.  Klicken Sie auf **Aktivieren**.  

> [!NOTE]
> Gehen Sie auf die gleiche Weise vor, um die Funktion für die Synchronisierung von Berichtsserverdateien zu deaktivieren. Klicken Sie jedoch auf **Deaktivieren**.

## <a name="see-also"></a>Siehe auch

 [Problembehandlung bei Berichtsteilen (Berichts-Generator und SSRS)](http://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Aktivieren der Berichtsserver- und Power View-Integrationsfunktionen in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
 [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
