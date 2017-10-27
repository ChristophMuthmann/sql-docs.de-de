---
title: "Verwenden der RenderedOutputFile-Klasse für eine Übermittlungserweiterung | Microsoft Docs"
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
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 35fa7b98c43bb20ef6df30f27ca74a5f2ada1792
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>Verwenden der RenderedOutputFile-Klasse für eine Übermittlungserweiterung
  Die <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Klasse stellt einen Datenstrom und Informationen zu den zugehörigen Eigenschaften des Datenstroms dar. Die **Daten** Eigenschaft von der <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> Klasse wird verwendet, um einen gerenderten Bericht oder eine Berichtsressource als darstellen einer **Stream** Objekt.  
  
 Die <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> Methode der **Bericht** Objekt gibt ein Array von mindestens einem <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> Objekte, die zusammen einen einzelnen gerenderten Bericht ausmachen. Das erste <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekt ist der gerenderte Bericht. Alle anderen <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekte sind Ressourcen, die zusammen mit den Berichtsdaten geliefert werden müssen (z. B. eine HTML-Datei und zugehörige Bilder). Renderingerweiterungen mit einem einzigen Datenstrom (IMAGE, PDF, MHTML und EXCEL) geben nur ein <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>-Objekt im Array zurück.  
  
 Ein Beispiel zum Verwenden der <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> Klasse, finden Sie unter [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Siehe auch  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

