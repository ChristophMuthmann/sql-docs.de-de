---
title: "Datamining-gespeicherte Prozeduren (Analysis Services – Datamining) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: stored procedures [Analysis Services], data mining
ms.assetid: a751856d-33bd-4788-9593-317b2826132d
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1d73a02535eb55e16de7058fa9f24dc335763f45
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="data-mining-stored-procedures-analysis-services---data-mining"></a>Data Mining-gespeicherte Prozeduren (Analysis Services - Data Mining)
  Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]beginnend, unterstützt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gespeicherte Prozeduren, die in jeder verwalteten Sprache geschrieben werden können. Die unterstützten verwalteten Sprachen umfassen [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET, C# und Managed C++. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]können Sie die gespeicherten Prozeduren entweder durch Verwendung einer **CALL** -Anweisung oder im Rahmen einer Data Mining Extensions-Abfrage (DMX) direkt aufrufen.  
  
 Weitere Informationen zum Aufrufen von gespeicherten Prozeduren in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] finden Sie unter [Aufrufen von gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md).  
  
 Allgemeine Informationen zur Programmierbarkeit finden Sie unter [Data Mining-Programmierung](../../analysis-services/data-mining-programming.md).  
  
 Weitere Informationen über das Programmieren von Data Mining-Objekten finden Sie in dem Artikel "[SQL Server Data Mining Programmability](http://go.microsoft.com/fwlink/?LinkId=93735)" in der MSDN Library.  
  
> [!NOTE]  
>  Wenn Sie Miningmodelle abfragen, insbesondere beim Testen neuer Data Mining-Lösungen, kann es praktisch sein, die gespeicherten Systemprozeduren aufzurufen, die intern vom Data Mining-Modul verwendet werden. Sie können die Namen dieser gespeicherten Systemprozeduren anzeigen, indem Sie mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] eine Ablaufverfolgung auf dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server erstellen und dann die Data Mining-Modelle erstellen, durchsuchen und abfragen. Jedoch garantiert [!INCLUDE[msCoName](../../includes/msconame-md.md)] nicht die versionsübergreifende Kompatibilität von gespeicherten Systemprozeduren, und Sie sollten Aufrufen von gespeicherten Systemprozeduren niemals in einem Produktionssystem verwenden. Statt dessen sollten Sie im Hinblick auf Kompatibilität eigene Abfragen mit DMX oder XML/A erstellen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [Registerkarte "übergreifende Überprüfung" &#40; Mining Mininggenauigkeitsdiagramm-Sicht &#41;](http://msdn.microsoft.com/library/bd215a68-1ad7-4046-9c44-ec8e2be13a64)   
 [Aufrufen von gespeicherten Prozeduren](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  
