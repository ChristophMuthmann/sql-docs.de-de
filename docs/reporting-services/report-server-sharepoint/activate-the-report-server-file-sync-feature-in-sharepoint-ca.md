---
title: "Aktivieren der Funktion zur Synchronisierung der Berichtsserverdateien in der SharePoint-Zentraladministration | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 32d1988d-07e7-41c2-b636-e65ecfae4677
caps.latest.revision: 9
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 9
---
# Aktivieren der Funktion zur Synchronisierung der Berichtsserverdateien in der SharePoint-Zentraladministration
  Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktion zur Synchronisierung der Berichtsserverdateien verwendet SharePoint-Ereignishandler, um den Berichtsserverkatalog mit Elementen in Dokumentbibliotheken zu synchronisieren. Diese Funktion ist nützlich, wenn Benutzer veröffentlichte Berichtselemente häufig direkt in die SharePoint-Dokumentbibliotheken hochladen. Wenn die Dateisynchronisierungsfunktion nicht aktiviert ist, werden Inhalte weiterhin synchronisiert. Dies erfolgt allerdings nicht so häufig.  
  
 Die Funktion zur Synchronisierung der Berichtsserverdateien kann in der SharePoint-Websiteverwaltung aktiviert werden, nachdem Sie das [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]-Add-In für SharePoint-Produkte installiert haben.  
  
 Die Funktion kann für einzelne Websites manuell aktiviert und deaktiviert werden, jedoch nicht auf Ebene der Websitesammlung.  
  
## Erforderliche Komponenten  
 Das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-In für SharePoint muss installiert sein. Falls das Add-In nicht installiert ist, wird die Dateisynchronisierungsfunktion nicht in der Funktionsliste der Website angezeigt.  
  
 Um die Installation zu überprüfen, zeigen Sie die Liste der installierten Anwendungen in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows- **Systemsteuerung**an. Wenn das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-In installiert ist, folgen Sie den Anweisungen in diesem Thema, um die Funktion zur Synchronisierung von Berichtsserverdateien zu aktivieren.  
  
### So aktivieren oder deaktivieren Sie die Funktion zur Synchronisierung der Berichtsserverdateien auf einer Website  
  
1.  Klicken Sie auf der Hauptseite der Website auf das Menü **Websiteaktionen** , und klicken Sie dann auf **Siteeinstellungen**.  
  
2.  Klicken Sie im Bereich **Websiteaktionen** auf **Websitefunktionen verwalten**.  
  
3.  Suchen Sie **Synchronisierung der Berichtsserverdateien** in der Liste.  
  
4.  Klicken Sie auf **Aktivieren**.  
  
> [!NOTE]  
>  Gehen Sie auf die gleiche Weise vor, um die Funktion für die Synchronisierung von Berichtsserverdateien zu deaktivieren. Klicken Sie jedoch auf **Deaktivieren**.  
  
## Siehe auch  
 [Problembehandlung bei Berichtsteilen (Berichts-Generator und SSRS)](http://msdn.microsoft.com/de-de/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Aktivieren der Berichtsserver- und Power View-Integrationsfunktionen in SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  