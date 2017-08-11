---
title: "Analysis Services-Verbindungstyp für DMX (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [Reporting Services], DMX
- Data Mining Prediction [Reporting Services]
- query view [Reporting Services]
- DMX [Reporting Services]
- design view [Reporting Services]
- data mining [Reporting Services]
- passing parameters [Reporting Services]
ms.assetid: 2de825e9-6d8a-4128-add0-da15dc6cea3e
caps.latest.revision: 64
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e4cb050e8f838eaab2bc215005b167c0dea258fc
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="analysis-services-connection-type-for-dmx-ssrs"></a>Analysis Services-Verbindungstyp für DMX (SSRS)
  Wenn Sie ein Dataset mithilfe einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenquelle erstellen, wird vom Berichts-Designer standardmäßig der MDX-Abfrage-Designer (Multidimensional Expressions) angezeigt, sobald ein gültiger Cube erkannt wird. Falls kein Cube erkannt wird, jedoch ein Data Mining-Modell verfügbar ist, zeigt der Berichts-Designer den DMX-Abfrage-Designer (Data Mining-Erweiterungen) an. Um zwischen MDX- und DMX-Designern wechseln möchten, klicken Sie auf die **DMX-Befehlstyp** (![ändern Sie in der Ansicht "Abfragesprache" DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "ändern Sie in der Ansicht "Abfragesprache" DMX")) auf der Symbolleiste. Mithilfe des DMX-Abfrage-Designers können Sie interaktiv eine DMX-Abfrage erstellen, die grafische Elemente verwendet. Damit der DMX-Abfrage-Designer verwendet werden kann, muss die angegebene Datenquelle bereits über ein Data Mining-Modell verfügen, das die Daten bereitstellt. Die Abfrageergebnisse werden für die Verwendung im Bericht in ein vereinfachtes Rowset konvertiert.  
  
> [!NOTE]  
>  Vor dem Entwerfen Ihres Berichts müssen Sie Ihr Modell trainieren. Weitere Informationen finden Sie unter [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md).  
  
## <a name="design-mode"></a>Entwurfsmodus  
 Der DMX-Abfrage-Designer wird im Entwurfsmodus geöffnet. Der Entwurfsmodus umfasst eine grafische Entwurfsoberfläche, die zum Auswählen eines einzelnen Data Mining-Modells und einer Eingabetabelle verwendet wird, und ein Raster zum Angeben der Vorhersageabfrage. Im DMX-Abfrage-Designer gibt es zwei weitere Modi: den Abfragemodus und den Ergebnismodus. Im Abfragemodus wird das Raster aus dem Entwurfsmodus durch einen Abfragebereich ersetzt, den Sie für die Eingabe von DMX-Abfragen verwenden können. Im Ergebnismodus wird das von der Abfrage zurückgegebene Resultset in einem Datenraster angezeigt.  
  
 Wenn Sie die Modi für den DMX-Abfrage-Designer ändern möchten, klicken Sie mit der rechten Maustaste auf die Abfrageentwurfsoberfläche, und wählen Sie **Entwurf**, **Abfrage**oder **Ergebnis**aus. Weitere Informationen finden Sie unter [Analysis Services DMX Query Designer User Interface](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md) und [Abrufen von Daten aus einer Data Mining-Modelle &#40; DMX &#41; &#40; SSRS &#41; ](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md).  
  
## <a name="designing-a-prediction-query"></a>Entwerfen einer Vorhersageabfrage  
 Der Bereich Abfrageentwurf im Entwurfsmodus enthält zwei Fenster: **Miningmodell** und **Eingabetabelle(n) auswählen**. Verwenden Sie das Fenster **Miningmodell** , um das für die Abfrage zu verwendende Miningmodell auszuwählen. Verwenden Sie das Fenster **Eingabetabelle(n) auswählen** , um die Tabelle auszuwählen, auf der Sie Ihre Vorhersagen basieren möchten. Wenn Sie anstelle einer Eingabetabelle eine SINGLETON-Abfrage verwenden möchten, klicken Sie mit der rechten Maustaste in den Bereich Abfrageentwurf, und wählen Sie **SINGLETON-Abfrage**aus. Das Fenster **Eingabetabelle(n) auswählen** wird durch das Fenster **SINGLETON-Abfrageeingabe** ersetzt.  
  
 Ziehen Sie im Entwurfsmodus die Felder aus den Fenstern **Miningmodell** und **Eingabetabelle(n) auswählen** in die **Feld** -Spalte des Rasterbereichs. Sie können bei Bedarf die verbleibenden Spalten ausfüllen, um einen Alias anzugeben, um das Feld in den Ergebnissen anzuzeigen, um Felder zusammen zu gruppieren und um einen Operator einzugeben, mit dem der Feldwert auf bestimmte Kriterien oder ein Argument begrenzt wird. Wenn Sie sich im Abfragemodus befinden, erstellen Sie die DMX-Abfrage, indem Sie Felder in den Bereich Abfrage ziehen.  
  
## <a name="using-parameters"></a>Verwenden von Parametern  
 Sie können Berichtsparameter an einen DMX-Abfrageparameter übergeben. Hierzu müssen Sie Ihrer DMX-Abfrage einen Parameter hinzufügen, die Abfrageparameter im Dialogfeld **Abfrageparameter** definieren und dann die zugeordneten Berichtsparameter ändern. Um einen Abfrageparameter definieren möchten, klicken Sie auf die **Abfrageparameter** (![Symbol für das Dialogfeld Abfrageparameter](../../reporting-services/report-data/media/iconqueryparameter.gif "Symbol für das Dialogfeld Abfrageparameter")) auf der Symbolleiste. Eine Anleitung zum Definieren von Parametern in einer DMX-Abfrage finden Sie unter [Definieren von Parametern im MDX-Abfrage-Designer für Analysis Services &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md).  
  
 Weitere Informationen zum Verwalten der Beziehung zwischen Berichtsparametern und Abfrageparametern finden Sie unter [Zuordnen eines Abfrageparameters mit einem Berichtsparameter &#40; Berichts-Generator und SSRS &#41; ](../../reporting-services/report-data/associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md). Weitere Informationen zu Parametern finden Sie unter [Berichtsparameter &#40; Berichts-Generator und Berichts-Designer &#41; ](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Abfrageentwurfstools &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
