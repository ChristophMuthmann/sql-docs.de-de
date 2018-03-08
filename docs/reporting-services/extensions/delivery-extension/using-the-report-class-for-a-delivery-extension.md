---
title: "Verwenden der Report-Klasse für eine Übermittlungserweiterung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], report information
- Report class
ms.assetid: 1145ac63-eafd-452a-82af-16f85b1676dd
caps.latest.revision: "34"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c43a942c2f28794e94cbea1beb875d0fdda73e82
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="using-the-report-class-for-a-delivery-extension"></a>Verwenden der Report-Klasse für eine Übermittlungserweiterung
  Die <xref:Microsoft.ReportingServices.Interfaces.Report>-Klasse stellt einen Bericht in der Berichtsserver-Datenbank dar. Jedes Abonnement wird einem bestimmten Bericht zugeordnet. Der Bericht ist in der Benachrichtigung enthalten. Die Übermittlungserweiterung kann das <xref:Microsoft.ReportingServices.Interfaces.Report>-Objekt verwenden, das Bestandteil der Benachrichtigung zum Rendern des Berichts ist. Das <xref:Microsoft.ReportingServices.Interfaces.Report>-Objekt enthält auch berichtsspezifische Eigenschaften, wie die URL zum Bericht auf dem Server und den Namen des Berichts. Diese Eigenschaften können alle als Teil des Übermittlungsanbieters verwendet werden.  
  
 Die <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A>-Methode der <xref:Microsoft.ReportingServices.Interfaces.Report>-Klasse kann zum Rendern eines Berichts verwendet werden. Die <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A>-Methode gibt ein Array von einem oder mehreren <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekten zurück, die zusammen einen gerenderten Bericht ausmachen. Das erste <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekt ist der gerenderte Bericht. Alle anderen <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekte sind Ressourcen, die zusammen mit den Berichtsdaten geliefert werden müssen (z. B. eine HTML-Datei und zugehörige Bilder). Renderingerweiterungen mit einem einzigen Datenstrom (IMAGE, PDF, MHTML und Excel) geben nur ein <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekt im Array zurück.  
  
 Das <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekt, das den Berichtsdatenstrom enthält, kann als Teil einer Übermittlung enthalten sein.  
  
 Ein Beispiel zur Verwendungsweise der <xref:Microsoft.ReportingServices.Interfaces.Report>-Klasse finden Sie unter [SQL Server Reporting Services-Produktbeispiele](http://go.microsoft.com/fwlink/?LinkId=177889)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Implementieren von Übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)   
 [Using the RenderedOutputFile Class for a Delivery Extension (Verwenden der RenderedOutputFile-Klasse für eine Übermittlungserweiterung)](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
  
  
