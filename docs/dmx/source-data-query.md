---
title: '&lt;quelldatenabfrage&gt; | Microsoft Docs'
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- data sources [DMX]
- predictions [DMX]
- source data query element
- queries [DMX], source data
- external data access [DMX]
- <source data query> element
- training mining models
ms.assetid: 9dce5e37-1354-4d28-87c2-f9c419cb5b09
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 195c2ecd04a28ad830aca2d90df821b76d46e98e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt"></a>&lt;quelldatenabfrage&gt;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Um eine Datamining-Modell zu trainieren und Vorhersagen aus einem Miningmodell erstellen, müssen Sie Daten zugreifen, die außerhalb der [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Datenbank. Verwenden Sie die \<quelldatenabfrage >-Klausel in Data Mining Extensions (DMX) diese externen Daten definieren. Die [INSERT INTO &#40; DMX &#41;](../dmx/insert-into-dmx.md), [SELECT FROM &#60; Modell &#62; PREDICTION JOIN-Abfrage &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md), und [SELECT FROM NATURAL PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) verwenden Sie die Anweisungen, die alle  **\<quelldatenabfrage >**.  
  
## <a name="query-types"></a>Abfragetypen  
 Die drei häufigsten Arten zum Angeben von Quelldaten sind:  
  
 [OPENQUERY &#40; DMX &#41;](../dmx/source-data-query-openquery.md)  
 Diese Anweisung fragt Daten ab, die für eine Instanz von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] externe Daten sind. Dazu wird eine vorhandene Datenquelle verwendet.  
  
 Während **OPENQUERY** Funktionsweise her vergleichbar, **OPENROWSET**, **OPENQUERY** hat die folgenden Vorteile:  
  
-   Eine DMX-Abfrage ist viel einfacher zu schreiben, **OPENQUERY**. Statt jedes Mal, wenn Sie eine Abfrage schreiben, eine neue Verbindungszeichenfolge zu erstellen, können Sie die vorhandene Verbindungszeichenfolge in der Datenquelle nutzen. Das Datenquellenobjekt kann außerdem den Datenzugriff für einzelne Benutzer steuern.  
  
-   Der Administrator kann besser steuern, wie auf die Daten auf dem Server zugegriffen wird. Beispielsweise kann der Administrator festlegen, welche Anbieter in den Server geladen werden und auf welche externen Daten zugegriffen werden kann.  
  
 [OPENROWSET &#40; DMX &#41;](../dmx/source-data-query-openrowset.md)  
 Diese Anweisung fragt Daten ab, die für eine Instanz von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] externe Daten sind. Dazu wird eine vorhandene Datenquelle verwendet.  
  
 [FORM "&#40; DMX &#41;](../dmx/source-data-query-shape.md)  
 Diese Anweisung fragt mehrere Datenquellen ab, um eine geschachtelte Tabelle zu erstellen. Mithilfe von **Form**, können Sie Daten aus mehreren Quellen in einer einzigen hierarchischen Tabelle kombinieren. Auf diese Weise können Sie die Möglichkeit von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nutzen, Tabellen zu schachteln, indem eine Tabelle in eine andere Tabelle eingebettet wird.  
  
 Zur Angabe der Quelldaten haben Sie folgende Möglichkeiten:  
  
-   Eine gültige DMX-Anweisung  
  
-   Eine gültige MDX-Anweisung (Multidimensional Expressions)  
  
-   Eine Tabelle, die eine gespeicherte Prozedur zurückgibt  
  
-   Ein XMLA-Rowset (XML for Analysis)  
  
-   Ein Rowsetparameter  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [Geschachtelte Tabellen &#40; Analysis Services – Datamining &#41;](../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  

