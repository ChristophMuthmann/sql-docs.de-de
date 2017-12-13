---
title: Konfigurieren von Attributbeziehungseigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- flexible relationships (Analysis Services)
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
- properties [Analysis Services], attribute relationships
- rigid relationships (Analysis Services)
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cfd4e60e3ed8329e78b5de7242b3952601a87b11
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="attribute-relationships---configure-attribute-properties"></a>Attributbeziehungen - Konfigurieren von Attributeigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]In der folgenden Tabelle aufgeführt und beschreibt die Eigenschaften einer attributbeziehung.  
  
|Eigenschaft|Beschreibung|  
|--------------|-----------------|  
|Attribute|Enthält den Namen des Attributs.|  
|Cardinality|Zeigt die Kardinalität der Beziehung an. Werte sind Many für eine m:1-Beziehung oder One für eine 1:1-Beziehung. Der Standardwert lautet Many. In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ist die Cardinality-Eigenschaft wirkungslos – sie ist für zukünftige Implementierungen reserviert.|  
|Name|Enthält den Anzeigenamen des Attributs.|  
|RelationshipType|Gibt an, ob die Elementbeziehungen im Laufe der Zeit geändert werden. Werte sind Rigid, d.h., dass die Beziehungen zwischen Elementen im Laufe der Zeit nicht geändert werden, oder Flexible, d.h., dass die Beziehungen zwischen Elementen im Laufe der Zeit geändert werden. Der Standardwert ist Flexible. Wenn Sie eine Beziehung vom Typ Flexible definieren, werden Aggregationen gelöscht und als Teil eines inkrementellen Updates neu berechnet. Sie werden nicht gelöscht, wenn nur neue Elemente hinzugefügt werden. Wenn Sie eine Beziehung vom Typ Rigid definieren, werden von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Aggregationen beim inkrementellen Aktualisieren der Dimension beibehalten. Wenn eine als Beziehung vom Typ Rigid definierte Beziehung tatsächlich geändert wird, wird während der inkrementellen Verarbeitung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ein Fehler generiert. Durch das Angeben der entsprechenden Beziehungen und Beziehungseigenschaften wird die Abfrage- und Verarbeitungsleistung erhöht.|  
|Visible|Bestimmt die Sichtbarkeit der Attributbeziehung. Die Werte sind True und False. Der Standardwert lautet "True".|  
  
  
