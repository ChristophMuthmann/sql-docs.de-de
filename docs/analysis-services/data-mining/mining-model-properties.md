---
title: Eigenschaften von Miningmodellen | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
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
- mining models [Analysis Services], properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- Data Mining Designer
- properties [data mining]
ms.assetid: c5194619-8b31-42be-a95f-585711462945
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fcc84bc6effb3e4a831ce58b81fcbe9e7eda3437
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="mining-model-properties"></a>Miningmodelleigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Miningmodelle verfügen über die folgenden Arten von Eigenschaften:  
  
-   Von der Miningstruktur geerbte Eigenschaften, die den Daten- und Inhaltstyp der von dem Modell verwendeten Daten definieren  
  
-   Eigenschaften, die sich auf den Algorithmus beziehen, der zum Erstellen des Miningmodells verwendet wurde, einschließlich sämtlicher Kundenparameter  
  
-   Eigenschaften, die auf dem Modell einen Filter definieren, die zum Trainieren des Modells verwendet wurden  
  
 Die Eigenschaften eines Miningmodells werden anfänglich definiert, wann Sie das Modell erstellen. Sie können später die meisten Eigenschaften, einschließlich der Algorithmusparameter, Filter und Spaltenverwendungseigenschaften, jedoch ändern. Mithilfe der Registerkarte **Miningmodelle** des Data Mining-Designers oder mit AMO oder XMLA können Sie Eigenschaften für Miningmodelle anpassen.  
  
 Nach dem Ändern einer Eigenschaft müssen Sie das Modell erneut verarbeiten, damit sich die Änderungen im Modell widerspiegeln. Eine erneute Verarbeitung ist auch dann erforderlich, wenn die Änderung nur Metadaten betrifft, wie beispielsweise das Hinzufügen eines Spaltenalias oder einer Spaltenbeschreibung.  
  
## <a name="properties-of-models"></a>Eigenschaften von Modellen  
 In der folgenden Tabelle werden die Eigenschaften, die für Miningmodelle spezifisch sind, beschrieben. Darüber hinaus gibt es Eigenschaften, die Sie im Mining in einzelnen Spalten festlegen können.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Algorithmus**|Legt den Algorithmustyp für das Miningmodell fest.|  
|**AlgorithmParameters**|Legt Werte für die zu jedem Algorithmustyp verfügbaren Algorithmusparameter fest.|  
|**Filter**|Legt einen Filter fest, der auf die Daten angewendet wird, die zum Trainieren und Testen des Miningmodells verwendet werden. Die Filterdefinition wird mit dem Modell gespeichert und kann optional verwendet werden, wenn Sie Vorhersageabfragen erstellen oder die Genauigkeit des Modells testen.<br /><br /> Beim Trainieren des Modells ist der Modellfilter nicht optional.|  
|**Name**|Legt den Namen des Miningmodells fest.|  
|**AllowDrillThrough**|Gibt an, ob Drillthrough für das Miningmodell aktiviert ist.|  
  
## <a name="properties-of-model-columns"></a>Eigenschaften der Modellspalte  
 Sie können die folgenden für Data Mining spezifischen Eigenschaften für jede Spalte in einem Miningmodell festlegen. Diese Eigenschaften können für jedes Miningmodell in einer Miningstruktur auf einen unterschiedlichen Wert festgelegt werden.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|**Beschreibung**|Beschreibt den Zweck der Miningspalte.|  
|**Name**|Legt den Namen der Miningmodellspalte fest. Sie können einen neuen Namen eingeben, um einen Alias für die Miningmodellspalte anzugeben.|  
|**ModelingFlags**|Legt algorithmusspezifische Flags für die Spalte fest.|  
|**SourceColumnID**|Gibt den Namen der Miningstrukturspalte an, auf der die Modellspalte basiert.<br /><br /> Diese Eigenschaft ist schreibgeschützt.|  
|**Usage**|Legt fest, wie die Spalte vom Miningmodell verwendet wird.|  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodellspalten](../../analysis-services/data-mining/mining-model-columns.md)   
 [Miningstrukturen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Ändern der Eigenschaften eines Miningmodells](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)   
 [Data Mining-Tools](../../analysis-services/data-mining/data-mining-tools.md)   
 [Erstellen einer relationalen Miningstruktur](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [Erstellen eines Alias für eine Modellspalte](../../analysis-services/data-mining/create-an-alias-for-a-model-column.md)  
  
  
