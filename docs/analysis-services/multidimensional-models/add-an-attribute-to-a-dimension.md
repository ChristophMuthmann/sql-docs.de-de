---
title: "Hinzuf&#252;gen eines Attributs zu einer Dimension | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Hinzufügen von Attributen"
  - "Automatisches Erstellen von Attributen"
  - "Attribute [Analysis Services], erstellen"
  - "Attribute [Analysis Services], hinzufügen"
  - "Manuelles Erstellen von Attributen [Analysis Services]"
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Hinzuf&#252;gen eines Attributs zu einer Dimension
  Sie können ein Attribut in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]entweder automatisch oder manuell zu einer Dimension hinzufügen.  
  
 Um ein Attribut automatisch zu erstellen, wählen Sie in **auf der Registerkarte** Dimensionsstruktur [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]des Dimensions-Designers die Spalte aus, die Sie einem Attribut zuordnen möchten, und ziehen Sie diese Spalte dann aus dem Bereich **Datenquellensicht** in den Bereich **Attribute** . Dadurch wird ein Attribut erstellt, das der Spalte zugeordnet ist. Dem Attribut wird derselbe Name zugeordnet wie der Name der Spalte. Ist bereits ein Attribut mit diesem Namen vorhanden, fügt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Ordinalzahl als Suffix hinzu, beginnend mit "1" für den ersten doppelten Namen.  
  
 Um ein Attribut manuell zu erstellen, legen Sie für den Bereich **Attribute** die Rasteransicht fest. Klicken Sie in der Namensspalte der letzten Zeile des Rasters auf das Element **\<Neues Attribut>**. Geben Sie einen Namen für das neue Attribut ein. Dadurch wird ein Attribut erstellt, das keiner Spalte zugeordnet ist und für alle Eigenschaften Standardeinstellungen besitzt. Sie können die Zuordnung im Fenster **Eigenschaften** von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] festlegen, indem Sie die **KeyColumns** -Eigenschaft für das neue Attribut konfigurieren.  
  
 Weitere Informationen finden Sie unter [Automatisches Definieren eines neuen Attributs](../../analysis-services/multidimensional-models/define-a-new-attribute-automatically.md), [Manuelles Definieren eines neuen Attributs](../Topic/Define%20a%20New%20Attribute%20Manually.md), [Binden eines Attributs an eine Namensspalte](../../analysis-services/multidimensional-models/bind-an-attribute-to-a-name-column.md), und [Ändern der KeyColumns-Eigenschaft eines Attributs](../../analysis-services/multidimensional-models/modify-the-keycolumn-property-of-an-attribute.md).  
  
## Siehe auch  
 [Dimensionsattributeigenschaftenverweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  