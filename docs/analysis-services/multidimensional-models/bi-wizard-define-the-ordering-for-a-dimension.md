---
title: "Definieren der Reihenfolge für eine Dimension | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OrderBy property
- dimensions [Analysis Services], ordering
- Business Intelligence enhancements [Analysis Services], ordering
- dimensions [Analysis Services], Business Intelligence enhancements
- ordering dimensions [Analysis Services]
- OrderByAttributeID property
ms.assetid: c42fbd58-244d-4e0a-b715-6f919cbc3ad9
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1b37dde7f32df56fdea9cb595796948f710a652f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="bi-wizard---define-the-ordering-for-a-dimension"></a>BI-Assistent – Definieren der Reihenfolge für eine Dimension
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Fügen Sie die Attributreihenfolge-Erweiterung aus einem Cube oder einer Dimension angeben, wie die Elemente eines Attributs sortiert werden. Elemente können nach dem Namen oder dem Schlüssel des Attributs oder dem Namen bzw. dem Schlüssel eines anderen Attributs (auf Basis einer Attributbeziehung) sortiert werden. Standardmäßig sind Elemente nach dem Namen sortiert. Diese Erweiterung ändert die Eigenschaftseinstellungen **OrderBy** und **OrderByAttributeID** für Attribute in einer Dimension.  
  
 Verwenden Sie zum Hinzufügen der Attributreihenfolge den Business Intelligence-Assistenten, und wählen Sie auf der Seite **Erweiterung auswählen** die Option **Attributreihenfolge angeben** aus. Der Assistent führt Sie durch die Schritte zum Auswählen einer Dimension, auf die die Attributreihenfolge angewendet werden soll, und zum Angeben der Reihenfolge der Attribute für die ausgewählte Dimension.  
  
## <a name="selecting-a-dimension"></a>Auswählen einer Dimension  
 Auf der ersten Seite des Assistenten, der Seite **Attributreihenfolge angeben** , geben Sie die Dimension an, auf die die Attributreihenfolge angewendet werden soll. Durch Anwenden der Attributreihenfolge auf die ausgewählte Dimension werden Änderungen an der Dimension vorgenommen. Diese Änderungen werden an alle Cubes vererbt, die die ausgewählte Dimension enthalten.  
  
## <a name="specifying-ordering"></a>Angeben der Reihenfolge  
 Auf der zweiten Seite des Assistenten, **Attributreihenfolge angeben** ,  geben Sie an, wie die Attribute in der Dimension sortiert werden.  
  
 In der **Reihenfolgenattribut** -Spalte können Sie das Attribut für die Reihenfolge ändern. Wenn das Attribut, das Elemente sortiert werden soll, nicht in der Liste ist, führen Sie einen Bildlauf nach unten in der Liste, und wählen Sie dann  **\<neues Attribut... >** So öffnen die **wählen Sie eine Spalte** (Dialogfeld), Sie können Wählen Sie eine Spalte in einer Dimensionstabelle. Durch Auswählen einer Spalte mithilfe des Dialogfelds **Spalte auswählen** wird ein zusätzliches Attribut erstellt, mit dem die Elemente eines Attributs sortiert werden können.  
  
 In der **Kriterien** -Spalte können Sie dann auswählen, ob die Elemente des Attributs entweder nach **Schlüssel** oder nach **Name**sortiert werden sollen.  
  
  
