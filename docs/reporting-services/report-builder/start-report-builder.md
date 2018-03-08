---
title: Starten des Berichts-Generators | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
caps.latest.revision: "56"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 53fba534d61d2fe1a1358daa1571ec66a1fab663
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="start-report-builder"></a>Starten des Berichts-Generators

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] ist eine eigenständige Berichterstellungsumgebung. Sie können darin paginierte Berichte erstellen und in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen oder integrierten SharePoint-Modus veröffentlichen.  
  
 Beim ersten Starten von [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webportal oder [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im integrierten SharePoint-Modus werden Sie aufgefordert, den Download im Microsoft Download Center durchzuführen. 
 
![report-builder-get-report-builder](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 Sie oder ein Administrator können auch [Berichts-Generator aus dem Microsoft Download Center auf Ihrem Computer installieren](http://go.microsoft.com/fwlink/?LinkID=219138). Einzelheiten finden Sie unter „Installieren des Berichts-Generators mit Systems Manager Server“ in [Installieren des Berichts-Generators](../../reporting-services/install-windows/install-report-builder.md) .
 
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] wird nicht installiert, wenn Sie SQL Server Reporting Services installieren. Sie müssen den Download und die Installation separat durchführen.  
  
 Wenn beim Starten von [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] aus dem Webportal oder von der SharePoint-Website aus eine frühere Version von [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] geöffnet wird, wenden Sie sich an Ihren Administrator. Dieser kann die Version auf dem Webportal oder der SharePoint-Website aktualisieren.  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversion-mdmd-from-the-includessrsnoversionincludesssrsnoversion-mdmd-web-portal"></a>So starten Sie [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] aus dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webportal  
  
1.  Geben Sie in der Adressleiste des Webbrowsers die URL für den Berichtsserver ein. Standardmäßig lautet die URL http://\<*Servername*>/Berichte.  
  
2.  Wählen Sie in der oberen Leiste des Webportals **Neu** > **Paginierter Bericht**aus.  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     Bei der ersten Ausführung werden Sie aufgefordert, [Berichts-Generator zu installieren](../../reporting-services/install-windows/install-report-builder.md). 
  
     Bei nachfolgenden Ausführungen wird [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] geöffnet, und Sie können einen paginierten Bericht erstellen oder einen Bericht auf dem Berichtsserver öffnen.  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversion-mdmd-in-sharepoint-integrated-mode"></a>So starten Sie [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] im integrierten SharePoint-Modus  
  
1.  Navigieren Sie zu der SharePoint-Website mit der gewünschten Bibliothek.  
  
2.  Öffnen Sie die Bibliothek.  
  
3.  Klicken Sie auf **Dokumente**.  
  
4.  Klicken Sie im Menü **Neues Dokument** auf **Berichts-Generator-Bericht**.  
  
     Dadurch wird beim ersten Mal der SQL Server-Assistent für den [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] gestartet. Einzelheiten finden Sie unter [Installieren des Berichts-Generators](../../reporting-services/install-windows/install-report-builder.md) .  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] wird geöffnet, und Sie können einen paginierten Bericht erstellen oder einen Bericht auf dem Berichtsserver öffnen.  
  
     **Hinweis:** Wenn das Menü **Neues Dokument** die Optionen **Berichts-Generator-Bericht**, **Berichts-Generator-Modell**oder **Berichtsdatenquelle**nicht enthält, müssen die entsprechenden Inhaltstypen der SharePoint-Bibliothek hinzugefügt werden. Weitere Informationen finden Sie unter [Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  

## <a name="next-steps"></a>Nächste Schritte

[Berichts-Generator in SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
[Set default options for Report Builder (Festlegen von Standardoptionen für den Berichts-Generator)](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
