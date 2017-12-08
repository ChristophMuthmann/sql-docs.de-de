---
title: "Aktivieren von PowerPivot-Integration für Websitesammlungen in der Zertifizierungsstelle | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9958979cc8e0c966ca12c531667d9e05e7dd91f8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="activate-power-pivot-integration-for-site-collections-in-ca"></a>Aktivieren von PowerPivot-Integration für Websitesammlungen in der Zertifizierungsstelle
  Die Funktion zur [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Integration für bestimmte Websitesammlungen muss aktiviert werden, wenn Sie die Installationsoption „Vorhandene Farm“ zur Installation von SQL Server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint verwendet haben. Wenn Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint mit der Option „Neuer Server“ installiert haben, können Sie diese Aufgabe überspringen, da SQL Server-Setup bereits die Funktion zur [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Integration für die Stammwebsitesammlung aktiviert hat, als die Bereitstellung konfiguriert wurde.  
  
 Die Funktionsaktivierung auf der Ebene der Websitesammlung ist erforderlich, um Ihren Websites Anwendungsseiten und Vorlagen zur Verfügung zu stellen, einschließlich Konfigurationsseiten für geplante Datenaktualisierungen und Anwendungsseiten für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalog- und Datenfeed-Bibliotheken.  
  
 Sie müssen die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Integration für jede Websitesammlung aktivieren, die die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Abfrageverarbeitung unterstützt.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Sie müssen Administrator einer Websitesammlung sein.  
  
## <a name="activate-power-pivot-features"></a>Aktivieren von PowerPivot-Funktionen  
  
1.  Klicken Sie auf einer SharePoint-Website auf **Websiteaktionen**.  
  
     Standardmäßig wird auf SharePoint-Webanwendungen über Port 80 zugegriffen. Dies bedeutet, dass Sie häufig eine SharePoint-Website zugreifen können, indem Sie http:// eingeben\<Computername > um die Stammwebsitesammlung zu öffnen.  
  
2.  Klicken Sie auf **Siteeinstellungen**.  
  
3.  Klicken Sie unter Websitesammlungsverwaltung auf **Websitesammlungsfeatures**.  
  
4.  Scrollen Sie auf der Seite nach unten, bis Sie **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Integration Site Collection Feature**(Power Pivot-Integrationsfunktion für Webseitensammlungen) finden.  
  
5.  Klicken Sie auf **Aktivieren**.  
  
6.  Wiederholen Sie den Schritt für zusätzliche Websitesammlungen, indem Sie jede Website öffnen und auf **Websiteaktionen**klicken.  
  
## <a name="see-also"></a>Siehe auch  
 [PowerPivot-Serververwaltung und -konfiguration in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Anfängliche Konfiguration (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)   
 [Installation von PowerPivot für SharePoint 2010](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)  
  
  
