---
title: "Verwenden den Berichtklasse für eine Übermittlungserweiterung | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], report information
- Report class
ms.assetid: 1145ac63-eafd-452a-82af-16f85b1676dd
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 2cbf3f1a1ffeb702551a2aa0ff94134867cb1786
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="using-the-report-class-for-a-delivery-extension"></a>Verwenden der Report-Klasse für eine Übermittlungserweiterung
  Die <xref:Microsoft.ReportingServices.Interfaces.Report>-Klasse stellt einen Bericht in der Berichtsserver-Datenbank dar. Jedes Abonnement wird einem bestimmten Bericht zugeordnet. Der Bericht ist in der Benachrichtigung enthalten. Die Übermittlungserweiterung kann das <xref:Microsoft.ReportingServices.Interfaces.Report>-Objekt verwenden, das Bestandteil der Benachrichtigung zum Rendern des Berichts ist. Das <xref:Microsoft.ReportingServices.Interfaces.Report>-Objekt enthält auch berichtsspezifische Eigenschaften, wie die URL zum Bericht auf dem Server und den Namen des Berichts. Diese Eigenschaften können alle als Teil des Übermittlungsanbieters verwendet werden.  
  
 Die <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A>-Methode der <xref:Microsoft.ReportingServices.Interfaces.Report>-Klasse kann zum Rendern eines Berichts verwendet werden. Die <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A>-Methode gibt ein Array von einem oder mehreren <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekten zurück, die zusammen einen gerenderten Bericht ausmachen. Das erste <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekt ist der gerenderte Bericht. Alle anderen <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekte sind Ressourcen, die zusammen mit den Berichtsdaten geliefert werden müssen (z. B. eine HTML-Datei und zugehörige Bilder). Renderingerweiterungen mit einem einzigen Datenstrom (IMAGE, PDF, MHTML und Excel) geben nur ein <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekt im Array zurück.  
  
 Das <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekt, das den Berichtsdatenstrom enthält, kann als Teil einer Übermittlung enthalten sein.  
  
 Ein Beispiel zum Verwenden der <xref:Microsoft.ReportingServices.Interfaces.Report> Klasse, finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889)  
  
## <a name="see-also"></a>Siehe auch  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)   
 [Verwenden der RenderedOutputFile-Klasse für eine Übermittlungserweiterung](../../../reporting-services/extensions/delivery-extension/using-the-renderedoutputfile-class-for-a-delivery-extension.md)  
  
  
