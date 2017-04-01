---
title: "Starten des Berichts-Generators | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Berichts-Generator, starten"
  - "Berichts-Generator starten"
  - "SharePoint-Integration [Reporting Services], Berichts-Generator starten"
  - "Starten des Berichts-Generators"
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
caps.latest.revision: 56
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 56
---
# Starten des Berichts-Generators
  Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] ist eine eigenständige Berichterstellungsumgebung. Sie können darin paginierte Berichte erstellen und in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen oder integrierten SharePoint-Modus veröffentlichen.  
  
 Beim ersten Starten von [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Webportal oder [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im integrierten SharePoint-Modus werden Sie aufgefordert, den Download im Microsoft Download Center durchzuführen. 
 
![report-builder-get-report-builder](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 Sie oder ein Administrator können auch [Berichts-Generator aus dem Microsoft Download Center auf Ihrem Computer installieren](http://go.microsoft.com/fwlink/?LinkID=219138). Einzelheiten finden Sie unter „Installieren des Berichts-Generators mit Systems Manager Server“ in [Installieren des Berichts-Generators](../../reporting-services/install-windows/install-report-builder.md).
 
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] wird nicht installiert, wenn Sie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] installieren. Sie müssen den Download und die Installation separat durchführen.  
  
 Wenn beim Starten von [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] aus dem Webportal oder von der SharePoint-Website aus eine frühere Version von [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] geöffnet wird, wenden Sie sich an Ihren Administrator. Dieser kann die Version auf dem Webportal oder der SharePoint-Website aktualisieren.  
  
## So starten Sie [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] aus dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Webportal  
  
1.  Geben Sie in der Adressleiste des Webbrowsers die URL für den Berichtsserver ein. Standardmäßig lautet die URL http://\<*Servername*>/reports.  
  
2.  Wählen Sie in der oberen Leiste des Webportals **Neu** > **Paginierter Bericht** aus.  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     Bei der ersten Ausführung werden Sie aufgefordert, [Berichts-Generator zu installieren](../../reporting-services/install-windows/install-report-builder.md). 
  
     Bei nachfolgenden Ausführungen wird [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] geöffnet, und Sie können einen paginierten Bericht erstellen oder einen Bericht auf dem Berichtsserver öffnen.  
  
## So starten Sie [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] im integrierten SharePoint-Modus  
  
1.  Navigieren Sie zu der SharePoint-Website mit der gewünschten Bibliothek.  
  
2.  Öffnen Sie die Bibliothek.  
  
3.  Klicken Sie auf **Dokumente**.  
  
4.  Klicken Sie im Menü **Neues Dokument** auf **Berichts-Generator-Bericht**.  
  
     Dadurch wird beim ersten Mal der SQL Server-Assistent für den [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] gestartet. Einzelheiten finden Sie unter [Installieren des Berichts-Generators](../../reporting-services/install-windows/install-report-builder.md).  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] wird geöffnet, und Sie können einen paginierten Bericht erstellen oder einen Bericht auf dem Berichtsserver öffnen.  
  
     **Hinweis:** Wenn das Menü **Neues Dokument** die Optionen **Berichts-Generator-Bericht**, **Berichts-Generator-Modell** oder **Berichtsdatenquelle** nicht enthält, müssen die entsprechenden Inhaltstypen der SharePoint-Bibliothek hinzugefügt werden. Weitere Informationen finden Sie unter [Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
## Siehe auch  
 [Berichts-Generator in SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 [Set default options for Report Builder](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  
  
  