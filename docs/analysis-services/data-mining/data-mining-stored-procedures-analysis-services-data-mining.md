---
title: "Data Mining-gespeicherte Prozeduren (Analysis Services - Data Mining) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "Gespeicherte Prozeduren [Analysis Services], Data Mining"
ms.assetid: a751856d-33bd-4788-9593-317b2826132d
caps.latest.revision: 26
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 26
---
# Data Mining-gespeicherte Prozeduren (Analysis Services - Data Mining)
  Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]beginnend, unterstützt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gespeicherte Prozeduren, die in jeder verwalteten Sprache geschrieben werden können. Die unterstützten verwalteten Sprachen umfassen [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].NET, C# und Managed C++. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Sie die gespeicherten Prozeduren entweder durch Verwendung einer **CALL**-Anweisung oder im Rahmen einer Data Mining Extensions-Abfrage (DMX) direkt aufrufen.  
  
 Weitere Informationen zum Aufrufen von gespeicherten Prozeduren in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] finden Sie unter [Aufrufen von gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md).  
  
 Allgemeine Informationen zur Programmierbarkeit von [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] finden Sie unter [Data Mining-Programmierung](../../analysis-services/data-mining-programming.md).  
  
 Weitere Informationen über das Programmieren von Data Mining-Objekten finden Sie in dem Artikel "[SQL Server Data Mining Programmability](http://go.microsoft.com/fwlink/?LinkId=93735)" in der MSDN Library.  
  
> [!NOTE]  
>  Wenn Sie Miningmodelle abfragen, insbesondere beim Testen neuer Data Mining-Lösungen, kann es praktisch sein, die gespeicherten Systemprozeduren aufzurufen, die intern vom Data Mining-Modul verwendet werden. Sie können die Namen dieser gespeicherten Systemprozeduren anzeigen, indem Sie mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] eine Ablaufverfolgung auf dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server erstellen und dann die Data Mining-Modelle erstellen, durchsuchen und abfragen. Jedoch garantiert [!INCLUDE[msCoName](../../includes/msconame-md.md)] nicht die versionsübergreifende Kompatibilität von gespeicherten Systemprozeduren, und Sie sollten Aufrufen von gespeicherten Systemprozeduren niemals in einem Produktionssystem verwenden. Statt dessen sollten Sie im Hinblick auf Kompatibilität eigene Abfragen mit DMX oder XML/A erstellen.  
  
## In diesem Abschnitt  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
## Verweis  
 [Skriptverwaltungsaufgaben in Analysis Services](../../analysis-services/instances/script-administrative-tasks-in-analysis-services.md)  
  
## Siehe auch  
 [Kreuzvalidierung &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)   
 [Übergreifende Überprüfung &#40;Registerkarte, Mininggenauigkeitsdiagramm-Sicht&#41;](../Topic/Cross-Validation%20Tab%20\(Mining%20Accuracy%20Chart%20View\).md)   
 [Aufrufen von gespeicherten Prozeduren](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
  