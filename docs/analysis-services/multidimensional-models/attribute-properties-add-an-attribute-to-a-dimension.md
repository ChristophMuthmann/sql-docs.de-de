---
title: "Ein Attribut einer Dimension hinzufügen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding attributes
- automatic attribute creation
- attributes [Analysis Services], creating
- attributes [Analysis Services], adding
- manual attribute creation [Analysis Services]
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fd1a1579a81f1728a47b217f06739b722fe226c7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="attribute-properties---add-an--attribute-to-a-dimension"></a>Attributeigenschaften - hinzufügen ein Attributs zu einer Dimension
  Sie können ein Attribut in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]entweder automatisch oder manuell zu einer Dimension hinzufügen.  
  
 Um ein Attribut automatisch zu erstellen, wählen Sie in **auf der Registerkarte** Dimensionsstruktur [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]des Dimensions-Designers die Spalte aus, die Sie einem Attribut zuordnen möchten, und ziehen Sie diese Spalte dann aus dem Bereich **Datenquellensicht** in den Bereich **Attribute** . Dadurch wird ein Attribut erstellt, das der Spalte zugeordnet ist. Dem Attribut wird derselbe Name zugeordnet wie der Name der Spalte. Ist bereits ein Attribut mit diesem Namen vorhanden, fügt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Ordinalzahl als Suffix hinzu, beginnend mit "1" für den ersten doppelten Namen.  
  
 Um ein Attribut manuell zu erstellen, legen Sie für den Bereich **Attribute** die Rasteransicht fest. In der Namensspalte der letzten Zeile im Raster, klicken Sie auf die  **\<neues Attribut >** Element. Geben Sie einen Namen für das neue Attribut ein. Dadurch wird ein Attribut erstellt, das keiner Spalte zugeordnet ist und für alle Eigenschaften Standardeinstellungen besitzt. Sie können die Zuordnung im Fenster **Eigenschaften** von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] festlegen, indem Sie die **KeyColumns** -Eigenschaft für das neue Attribut konfigurieren.  
  
 Weitere Informationen finden Sie unter [Automatisches Definieren eines neuen Attributs](../../analysis-services/multidimensional-models/attribute-properties-define-a-new-attribute-automatically.md), [Binden eines Attributs an eine Namensspalte](../../analysis-services/multidimensional-models/attribute-properties-bind-an-attribute-to-a-name-column.md), und [Ändern der KeyColumns-Eigenschaft eines Attributs](../../analysis-services/multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)entweder automatisch oder manuell zu einer Dimension hinzufügen.  
  
## <a name="see-also"></a>Siehe auch  
 [Dimensionsattributeigenschaftenverweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
