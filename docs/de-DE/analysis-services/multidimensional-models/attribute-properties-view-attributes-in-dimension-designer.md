---
title: Anzeigen der Attribute im Dimensions-Designer | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9aea7f4ddf82a909c1fe6037513c650108e0b820
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-properties---view-attributes-in-dimension-designer"></a>Attributeigenschaften – Anzeigen von Attributen im Dimensions-Designer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Attribute werden für Dimensionsobjekte erstellt. Sie können Attribute mithilfe des Dimensions-Designers in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]anzeigen und konfigurieren. Die in einer Dimension enthaltenen Attribute werden im Dimensions-Designer auf der Registerkarte **Dimensionsstruktur** im Bereich **Attribute** angezeigt. Verwenden Sie diesen Bereich, um Attribute hinzuzufügen, zu entfernen oder zu konfigurieren. Sie können außerdem Attribute auswählen, um sie als Ebene in einer neuen Hierarchie zu verwenden oder einer vorhandenen Hierarchie als Ebene hinzuzufügen.  
  
 Um die Attribute in einer Dimension anzuzeigen, öffnen Sie den Dimensions-Designer für die Dimension. Die in der Dimension enthaltenen Attribute werden im Dimensions-Designer auf der Registerkarte **Dimensionsstruktur** im Bereich **Attribute**  angezeigt. Sie können zwischen einer Listen-, Struktur- oder Rasteransicht wechseln. Zeigen Sie dazu im Menü **Dimension** von **auf** Attribute anzeigen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , und klicken Sie dann auf einen der Befehle:  
  
1.  Attribute in einer **Liste**anzeigen. Zeigt die Attribute im Listenformat an. Klicken Sie mit der rechten Maustaste auf ein Attribut, um es aus der Liste zu löschen, umzubenennen oder die Verwendung des Attributs zu ändern. Verwenden Sie diese Ansicht zum Erstellen von Hierarchien. Attributinformationen und Elementeigenschaften werden nicht angezeigt.  
  
2.  Attribute in einer **Struktur**anzeigen. Zeigen Sie die Attribute im Strukturformat an, wobei die Dimension als Knoten der obersten Ebene in der Struktur dargestellt wird. Erweitern Sie ein Attribut, um seine Attributbeziehungen anzuzeigen oder um eine neue Attributbeziehung zu erstellen. Führen Sie hierzu folgende Aktionen aus:  
  
    -   Klicken Sie auf die Dimension, ein Attribut oder eine Elementeigenschaft, um die zugehörigen Eigenschaften im Fenster **Eigenschaften** anzuzeigen.  
  
    -   Klicken Sie mit der rechten Maustaste auf ein Attribut oder eine Elementeigenschaft, um das Attribut oder die Elementeigenschaft aus der Liste zu löschen, umzubenennen oder die Verwendung zu ändern.  
  
     Verwenden Sie diese Ansicht zum Anzeigen und Erstellen von Elementeigenschaften. Mithilfe dieser Ansicht können Sie auch Hierarchien erstellen.  
  
3.  Attribute in einem **Raster**anzeigen. Zeigt die Attribute im Rasterformat an. Das Raster zeigt die folgenden Spalten an:  
  
    -   **Name** enthält den Wert der **Name** -Eigenschaft. Geben Sie einen anderen Namen ein, um die Einstellung zu ändern.  
  
    -   **Verwendung** gibt an, ob es sich hierbei um ein Regular-, Key-, Parent- oder AccountType-Attribut handelt. Klicken Sie auf einen Wert in dieser Spalte, um eine andere Einstellung auszuwählen.  
  
    -   **Typ** gibt die Business Intelligence-Kategorie für das Attribut an. Klicken Sie auf diese Zelle, um eine andere Einstellung auszuwählen.  
  
    -   **Schlüsselspalte** zeigt den OLE DB-Datentyp für die **KeyColumn** -Eigenschaft für das Attribut an. Diese Spalte kann nicht geändert werden.  
  
    -   **Namensspalte** gibt an, ob sich die Einstellung für die **NameColumn** -Eigenschaft für das Attribut in derselben Spalte befindet wie die Einstellung für die **KeyColumn** -Eigenschaft. Diese Spalte kann nicht geändert werden.  
  
     Klicken Sie auf eine Zeile im Raster, um Eigenschaften für dieses Attribut anzuzeigen.  
  
     Verwenden Sie diese Ansicht zum Erstellen und Konfigurieren von Attributen.  
  
 In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]kennzeichnen die in der folgenden Tabelle dargestellten Symbole Attribute gemäß ihrer Verwendung.  
  
|Symbol|Attributverwendung|  
|----------|---------------------|  
|![Symbol "Attribut"](../../analysis-services/multidimensional-models/media/as-icon-attribute.gif "Attribut (Symbol)")|Regular oder AccountType|  
|![Schlüsselattribut (Symbol)](../../analysis-services/multidimensional-models/media/as-icon-key-attribute.gif "Key-Attribut (Symbol)")|Key|  
|![Übergeordnetes Attribut (Symbol)](../../analysis-services/multidimensional-models/media/as-icon-parent-attribute.gif "übergeordnete Attribut (Symbol)")|Parent|  
  
## <a name="see-also"></a>Siehe auch  
 [Dimensionsattributeigenschaftenverweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
