---
title: Ein Attribut einer Dimension hinzufügen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e512d61e1417bd5ad794f48289f537777a34f307
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-properties---add-an--attribute-to-a-dimension"></a>Attributeigenschaften - hinzufügen ein Attributs zu einer Dimension
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Sie können ein Attribut in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]entweder automatisch oder manuell zu einer Dimension hinzufügen.  
  
 Um ein Attribut automatisch zu erstellen, wählen Sie in **auf der Registerkarte** Dimensionsstruktur [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]des Dimensions-Designers die Spalte aus, die Sie einem Attribut zuordnen möchten, und ziehen Sie diese Spalte dann aus dem Bereich **Datenquellensicht** in den Bereich **Attribute** . Dadurch wird ein Attribut erstellt, das der Spalte zugeordnet ist. Dem Attribut wird derselbe Name zugeordnet wie der Name der Spalte. Ist bereits ein Attribut mit diesem Namen vorhanden, fügt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Ordinalzahl als Suffix hinzu, beginnend mit "1" für den ersten doppelten Namen.  
  
 Um ein Attribut manuell zu erstellen, legen Sie für den Bereich **Attribute** die Rasteransicht fest. In der Namensspalte der letzten Zeile im Raster, klicken Sie auf die  **\<neues Attribut >** Element. Geben Sie einen Namen für das neue Attribut ein. Dadurch wird ein Attribut erstellt, das keiner Spalte zugeordnet ist und für alle Eigenschaften Standardeinstellungen besitzt. Sie können die Zuordnung im Fenster **Eigenschaften** von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] festlegen, indem Sie die **KeyColumns** -Eigenschaft für das neue Attribut konfigurieren.  
  
 Weitere Informationen finden Sie unter [Automatisches Definieren eines neuen Attributs](../../analysis-services/multidimensional-models/attribute-properties-define-a-new-attribute-automatically.md), [Binden eines Attributs an eine Namensspalte](../../analysis-services/multidimensional-models/attribute-properties-bind-an-attribute-to-a-name-column.md), und [Ändern der KeyColumns-Eigenschaft eines Attributs](../../analysis-services/multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)entweder automatisch oder manuell zu einer Dimension hinzufügen.  
  
## <a name="see-also"></a>Siehe auch  
 [Dimensionsattributeigenschaftenverweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
