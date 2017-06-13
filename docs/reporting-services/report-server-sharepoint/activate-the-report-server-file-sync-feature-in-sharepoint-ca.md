---
title: Aktivieren Sie die Report Server-Dateisynchronisierungsfunktion in der SharePoint-Zertifizierungsstelle | Microsoft Docs
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
ms.assetid: 32d1988d-07e7-41c2-b636-e65ecfae4677
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d9f1b75bc40693248526282a6565db340930601b
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-ca"></a>Aktivieren Sie die Report Server-Dateisynchronisierungsfunktion in der SharePoint-Zertifizierungsstelle
  Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktion zur Synchronisierung der Berichtsserverdateien verwendet SharePoint-Ereignishandler, um den Berichtsserverkatalog mit Elementen in Dokumentbibliotheken zu synchronisieren. Diese Funktion ist nützlich, wenn Benutzer veröffentlichte Berichtselemente häufig direkt in die SharePoint-Dokumentbibliotheken hochladen. Wenn die Dateisynchronisierungsfunktion nicht aktiviert ist, werden Inhalte weiterhin synchronisiert. Dies erfolgt allerdings nicht so häufig.  
  
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
>  Gehen Sie auf die gleiche Weise vor, um die Funktion für die Synchronisierung von Berichtsserverdateien zu deaktivieren. Klicken Sie jedoch auf **Deaktivieren**.  
  
## <a name="see-also"></a>Siehe auch  
 [Problembehandlung bei Berichtsteilen (Berichts-Generator und SSRS)](http://msdn.microsoft.com/en-us/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Aktivieren der Berichtsserver- und Power View-Integrationsfunktionen in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
 [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
