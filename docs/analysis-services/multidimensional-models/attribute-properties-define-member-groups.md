---
title: Definieren von Elementgruppen | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
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
- member groups [Analysis Services]
- grouping members
- DiscretizationMethod property
ms.assetid: 006cc915-c499-4781-b9a7-01ad31bebf6a
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 36110a1967917adda6c06ca0e32d138639e1871e
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="attribute-properties---define-member-groups"></a>Attributeigenschaften: Definieren von Elementgruppen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Wenn ein Attribut über viele Elemente verfügt, können Sie diese Elemente in Buckets gruppieren und so die Zahl derjenigen Elemente verringern, die Benutzer sehen, wenn sie die Daten einer Hierarchie durchsuchen. Sie können auch die Zahl der Buckets festlegen, in denen die Elemente Gruppen bilden und ein Benennungsschema für die Buckets vorgeben. Weitere Informationen finden Sie unter [Gruppieren von Attributelementen &#40;Diskretisierung&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
 Sie gruppieren Elemente, indem Sie die **DiscretizationMethod** -Eigenschaft festlegen, auf die Sie im Fenster **Eigenschaften** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]zugreifen können.  
  
 Wenn Sie Elementgruppen erstellen, sind Ihre Änderungen erst dann für Benutzer verfügbar, wenn Sie die Dimension verarbeitet haben. Weitere Informationen finden Sie unter [Verarbeiten eines mehrdimensionalen Modells &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-create-member-groups"></a>So erstellen Sie eine Elementgruppe  
  
1.  Öffnen Sie die Dimension, mit der Sie arbeiten möchten. Standardmäßig wird die Registerkarte **Dimensionsstruktur** geöffnet.  
  
2.  Klicken Sie in **Attribute**mit der rechten Maustaste auf die Attribute, deren Elemente Sie gruppieren möchten, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Wählen Sie in der Dropdownliste neben **DiscretizationMethod** eine Methode aus, nach der Sie die Elemente gruppieren. Weitere Informationen zu **DiscretizationMethod**-Einstellungen finden Sie unter [Gruppieren von Attributelementen &#40;Diskretisierung&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
  
