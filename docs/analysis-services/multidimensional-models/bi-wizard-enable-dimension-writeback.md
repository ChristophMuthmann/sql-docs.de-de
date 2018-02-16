---
title: "Aktivieren des Rückschreibens | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying dimensions
- writeback [Analysis Services], setting up
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], writeback
- dimensions [Analysis Services], writeback
- writeback [Analysis Services]
- dimensions [Analysis Services], modifying
- manual dimension structure modifications
ms.assetid: a4b5eb5a-366d-4fc8-ad0d-5bdb8e7b4163
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 69390faf39311c3b7072e06aff2b64fcafd9a62c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="bi-wizard---enable-dimension-writeback"></a>BI-Assistent – Rückschreiben von Dimensionen aktivieren
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Fügen Sie einem Cube oder einer Dimension die Erweiterung zum Rückschreiben von Dimensionen hinzu, um Benutzern das manuelle Ändern der Dimensionsstruktur und -elemente zu ermöglichen. Updates für eine Dimension mit aktiviertem Schreibzugriff werden direkt in der Dimensionstabelle aufgezeichnet. Durch diese Erweiterung wird die Einstellung der **WriteEnabled** -Eigenschaft für eine Dimension geändert.  
  
 Verwenden Sie den Business Intelligence-Assistenten, um das Rückschreiben von Dimensionen zu aktivieren, und wählen Sie auf der Seite **Erweiterung auswählen** die Option **Rückschreiben von Dimensionen aktivieren** aus. Anschließend führt Sie der Assistent durch die Schritte zum Auswählen einer Dimension, für die Sie das Rückschreiben von Dimensionen anwenden möchten, und zum Festlegen dieser Option für die ausgewählte Dimension.  
  
> [!NOTE]  
>  Das Rückschreiben wird nur für relationale SQL Server-Datenbanken und Data Marts unterstützt.  
  
## <a name="selecting-a-dimension"></a>Auswählen einer Dimension  
 Auf der ersten Seite **Rückschreiben von Dimensionen aktivieren** des Assistenten geben Sie die Dimension an, auf die Sie das Rückschreiben von Dimensionen anwenden möchten. Die Erweiterung zum Rückschreiben von Dimensionen, die dieser ausgewählten Dimension hinzugefügt wurde, führt zu Änderungen an der Dimension. Diese Änderungen werden an alle Cubes vererbt, die die ausgewählte Dimension enthalten.  
  
## <a name="setting-dimension-writeback-capability"></a>Festlegen des Features zum Rückschreiben von Dimensionen  
 Auf der zweiten Seite **Rückschreiben von Dimensionen aktivieren** des Assistenten findet das eigentliche Festlegen der Option **Rückschreiben in der Dimension aktivieren** statt. Durch Auswählen dieser Option wird die **WriteEnabled** -Eigenschaft der Dimension automatisch auf **True**festgelegt. Durch Deaktivieren dieser Option wird die Eigenschaft automatisch auf **False**festgelegt.  
  
## <a name="remarks"></a>Hinweise  
 Beim Erstellen eines neuen Elements müssen Sie jedes Attribut in einer Dimension angeben. Sie können kein Element einfügen, ohne dabei einen Wert für das Schlüsselattribut der Dimension anzugeben. Deshalb unterliegt das Erstellen von Elementen allen Beschränkungen (z.&#160;B. von NULL verschiedene Schlüsselwerte), die für die Dimensionstabelle definiert sind. Sie sollten auch Spalten berücksichtigen, die optional durch Dimensionseigenschaften angegeben werden, z. B. Spalten, die in den Dimensionseigenschaften **CustomRollupColumn**, **CustomRollupPropertiesColumn** oder **UnaryOperatorColumn** angegeben werden.  
  
> [!WARNING]  
>  Wenn Sie SQL Azure als Datenquelle verwenden, um einen Rückschreibevorgang in eine Analysis Services-Datenbank auszuführen, schlägt der Vorgang fehl. Dies ist programmbedingt, da die Anbieteroption, durch die mehrere aktive Resultsets (MARS) aktiviert werden, standardmäßig deaktiviert ist.  
>   
>  Als Problemumgehung fügen Sie der Verbindungszeichenfolge folgende Einstellung hinzu, damit MARS unterstützt und Rückschreibvorgänge aktiviert werden:  
>   
>  `"MultipleActiveResultSets=True"`  
>   
>  Weitere Informationen finden Sie unter [Verwenden von Multiple Active Result Sets &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Dimensionen mit aktiviertem Schreibzugriff](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
