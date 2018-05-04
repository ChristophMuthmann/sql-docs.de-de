---
title: Legen Sie die Slice-Eigenschaft für Partitionen (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0267418bdc992468d9730407e5094b968cb6023b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="set-the-partition-slice-property-analysis-services"></a>Festlegen der Slice-Eigenschaft für Partitionen (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ein Datenslice ist eine wichtige Optimierungsfunktion, die Ihnen dabei hilft, Abfragen an Daten der entsprechenden Partitionen weiterzuleiten. Das explizite Festlegen der Slice-Eigenschaft kann die Abfrageleistung verbessern, indem die für MOLAP- und HOLAP-Partitionen generierten Standardslices überschrieben werden. Darüber hinaus bietet die Slice-Eigenschaft bei der Verarbeitung der Partition eine zusätzliche Überprüfungsmöglichkeit.  
  
 Sie können einen Datenslice mithilfe der Slice-Eigenschaft angeben, nachdem Sie eine Partition erstellt, aber noch nicht verarbeitet haben. Erweitern Sie auf der Registerkarte „Partitionen“ eine Measuregruppe, klicken Sie mit der rechten Maustaste auf eine Partition, und wählen Sie **Eigenschaften**aus.  
  
 Die Vorteile von Datenslices werden ausführlich unter [Festlegen von "Slice" für die SSAS-Cubepartition](http://go.microsoft.com/fwlink/?LinkId=317783)erläutert.  
  
## <a name="defining-a-slice"></a>Definieren eines Slices  
 Gültige Werte für eine Slice-Eigenschaft sind ein MDX-Element, eine Menge oder ein Tupel. In den folgenden Beispielen wird die gültige Slicesyntax veranschaulicht:  
  
|Slice|Element, Menge oder Tupel|  
|-----------|--------------------------|  
|[Date].[Calendar].[Calendar Year].&[2010]|Geben Sie diesen Slice für eine Partition an, in der Fakten aus dem Jahr 2010 enthalten sind (vorausgesetzt, das Modell verfügt über eine Datumsdimension mit der Hierarchie "Calendar Year", der "2010" als Element angehört). Obwohl die WHERE-Klausel oder Tabelle der Partitionsquelle möglicherweise bereits nach "2010" gefiltert ist, ermöglicht die Angabe von Slice während der Verarbeitung eine zusätzliche Überprüfung sowie gezieltere Scans während der Abfrageausführung.|  
|{ [Sales Territory].[Sales Territory Country].&[Australia], [Sales Territory].[Sales Territory Country].&[Canada] }|Geben Sie diesen Slice für eine Partition mit Fakten an, die Informationen zum Vertriebsgebiet enthalten. Ein Slice kann eine MDX-Menge sein, die aus mindestens zwei Elementen besteht.|  
|[Measures].[Sales Amount Quota] > '5000'|Im folgenden Slice wird ein MDX-Ausdruck angezeigt.|  
  
 Ein Datenslice einer Partition sollte die Daten in der Partition so getreu wie möglich wiedergeben. Wenn eine Partition z. B. auf die Daten des Jahres 2012 beschränkt ist, sollte der Datenslice der Partition das 2012-Element der Time-Dimension angeben. Es ist nicht immer möglich, einen Datenslice anzugeben, der den genauen Inhalt einer Partition wiedergibt. Wenn eine Partition z. B. Daten ausschließlich für January und February enthält, die Ebenen der Time-Dimension jedoch Year, Quarter und Month lauten, bietet der Partitions-Assistent keine Möglichkeit, die January- und February-Elemente zugleich auszuwählen. Wählen Sie in solchen Fällen das übergeordnete Objekt der Elemente aus, die den Inhalt der Partition wiedergeben. Wählen Sie in diesem Beispiel Quarter 1 aus.  
  
> [!NOTE]  
>  Beachten Sie, dass dynamische MDX-Funktionen (z.B. [Generate &#40;MDX&#41;](../../mdx/generate-mdx.md) oder [Except &#40;MDX&#41;](../../mdx/except-mdx-function.md)) in der Slice-Eigenschaft für Partitionen nicht unterstützt werden. Sie müssen das Slice mit expliziten Tupel- oder Elementverweisen definieren.  
>   
>  Anstatt z. B. den Bereichsoperator (:) zum Definieren eines Bereichs zu verwenden, müssen Sie jedes Element anhand der bestimmten Jahre auflisten.  
>   
>  Wenn Sie ein komplexes Slice definieren müssen, empfiehlt sich das Definieren der Tupel im Slice mithilfe eines XMLA-Alter-Skripts. Anschließend können Sie das Befehlszeilentool „ascmd“ oder den Analysis Services Task [DDL ausführen](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) in Integration Services verwenden, um unmittelbar vor dem Verarbeiten der Partition das Skript auszuführen und den bestimmten Satz an Elementen zu erstellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie und verwalten Sie einer lokalen Partition & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
  
