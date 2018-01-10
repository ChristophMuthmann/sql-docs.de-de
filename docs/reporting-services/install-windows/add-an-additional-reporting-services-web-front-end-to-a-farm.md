---
title: "Hinzufügen eines zusätzlichen Reporting Services-Web-Front-Ends zu einer Farm | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7a11bda-ae26-49ac-b071-37d83cae5afe
caps.latest.revision: "11"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e96982736ae430b6b2269401564e17b587f14484
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>Hinzufügen eines zusätzlichen Reporting Services-Web-Front-Ends zu einer Farm
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Modus schließt für Anwendungsserver und Web-Front-End-Server (WFE) benötigte Komponenten ein. In diesem Thema liegt der Schwerpunkt auf der Installation der erforderlichen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Komponenten für einen WFE-Server, einschließlich der Anwendungsseiten, die von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Funktionen wie z. B. Abonnements, Datenwarnungen und [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]verwendet werden. Die primäre für ein WFE benötigte [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation ist das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint 2016-Produkte.  
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Sie müssen lokaler Administrator sein, um SQL Server-Setup auszuführen.  
  
-   Der Computer muss einer Domäne hinzugefügt werden.  
  
-   Sie müssen den Namen des vorhandenen Datenbankservers wissen, der die SharePoint-Konfiguration und Inhaltsdatenbanken hostet.  
  
-   Der Datenbankserver muss konfiguriert sein, um Remotedatenbankverbindungen zu berücksichtigen.  Wenn nicht, sind Sie nicht in der Lage, den neuen Server zur Farm hinzuzufügen, da der neue Server nicht in der Lage ist, eine Verbindung mit den SharePoint-Konfigurationsdatenbanken herzustellen.  
  
-   Auf dem neuen Server muss die gleiche Version von SharePoint installiert sein, die auf den aktuellen Farmservern ausgeführt wird. Wenn auf der Farm z.B. bereits SharePoint 2013 Service Pack 1 (SP1) installieren ist, müssen Sie SP1 auch auf dem neuen Server installieren, bevor er zur Farm hinzugefügt werden kann.  
  
## <a name="steps"></a>Schritte  
 Die Schritte in diesem Thema gehen davon aus, dass ein SharePoint-Farmadministrator den Server installiert und konfiguriert. Das Diagramm zeigt eine typische dreistufige Umgebung, und die nummerierten Elemente im Diagramm werden in der folgenden Liste beschrieben:  
  
-   (1) Mehrere Web-Front-End (WFE)-Server. Die WFE-Server erfordern das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In für SharePoint 2010. Mit den folgenden Schritte wird dieser Ebene ein zweiter Anwendungsserver hinzugefügt.  
  
-   (2) Zwei Anwendungsserver, die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und Websites ausführen, z. B. Zentraladministration.  
  
-   (3) Zwei SQL Server-Datenbankserver.  
  
-   (4) Stellt eine Software oder eine Hardware-Netzwerklastenausgleichslösung (NLB) dar  
  
 ![Hinzufügen von SSRS zu einem neuen SharePoint WFE](../../reporting-services/install-windows/media/rs-sharepointscale-wfe.gif "Add SSRS to a new SharePoint WFE")  
  
 Die folgenden Schritte gehen davon aus, dass ein Administrator den Server installiert und konfiguriert.  
  
|Schritt|Beschreibung und Link|  
|----------|--------------------------|  
|Fügen Sie einen SharePoint-Server zu einer Farm hinzu.|Sie müssen SharePoint installieren, um eine weitere Reporting Services-Anwendung bereitzustellen.<br/><br/>Für SharePoint 2013 finden Sie Informationen dazu unter [Hinzufügen eines SharePoint-Servers zu einer Farm in SharePoint Server 2013](https://technet.microsoft.com/library/cc261752(v=office.15).aspx).<br/><br/>Für SharePoint 2016 finden Sie Informationen dazu unter [Hinzufügen eines SharePoint-Servers zu einer Farm in SharePoint Server 2016](https://technet.microsoft.com/library/cc261752(v=office.16).aspx).|  
|Installieren Sie das SQL Server Reporting Services-Add-In für SharePoint 2016-Produkte|Es gibt mehrere Methoden zum Installieren des Add-Ins. In den folgenden Schritten wird der SQL Server-Setup-Assistent verwendet. Weitere Informationen zur Installation des Add-Ins finden Sie unter [Installieren oder Deinstallieren des Reporting Services-Add-Ins für SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).<br /><br /> 1) Führen Sie die SQL Server-Installation aus.<br /><br /> 2) Wählen Sie auf der Seite **Setuprolle** die Option **SQL Server-Funktionsinstallation**aus.<br /><br /> 3) Wählen Sie auf der Seite **Funktionsauswahl** die Option **Reporting Services-Add-In für SharePoint-Produkte**aus.<br /><br /> 4) Klicken Sie auf den nächsten Seiten auf **Weiter** , um die Setupoptionen zu vervollständigen.<br /><br/>Weitere Informationen zum Installieren von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]finden Sie unter [Installieren des ersten Berichtsservers im SharePoint-Modus](http://msdn.microsoft.com/en-us/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538).|  
|Überprüfen Sie, ob der neue Server betriebsbereit ist.|1) Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Systemeinstellungen** auf **Server in dieser Farm verwalten** .<br /><br /> 2) Überprüfen Sie, ob der neue Server in der Liste aufgeführt ist.|  
|Aktualisieren Sie die NLB-Lösung.|Aktualisieren Sie die Hardware- oder Software-NLB-Umgebung, falls erforderlich, um den neuen Server einzuschließen.|  

## <a name="next-steps"></a>Nächste Schritte

[Hinzufügen eines SharePoint-Servers zu einer Farm in SharePoint Server 2016](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)  
[Hinzufügen eines SharePoint-Servers zu einer Farm in SharePoint Server 2013](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
