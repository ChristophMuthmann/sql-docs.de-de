---
title: "Ziel für dimensionsverarbeitung | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dimensionprocessingdest.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b32a1d596ff1395a693f8316d7a6ee1f0d8aa918
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="dimension-processing-destination"></a>Ziel für Dimensionsverarbeitung
  Das Ziel für Dimensionsverarbeitung lädt und verarbeitet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dimension. Weitere Informationen zu Dimensionen finden Sie unter [Dimensionen &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 Das Ziel für Dimensionsverarbeitung schließt die folgenden Funktionen ein:  
  
-   Optionen für die inkrementelle Verarbeitung, vollständige Verarbeitung oder Updateverarbeitung.  
  
-   Fehlerkonfiguration, um anzugeben, ob die Dimensionsverarbeitung Fehler ignoriert oder nach einer bestimmten Anzahl von Fehlern beendet wird.  
  
-   Zuordnung von Eingabespalten zu Spalten in Dimensionstabellen.  
  
 Weitere Informationen zum Verarbeiten von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Objekten finden Sie unter [Verarbeitungsoptionen und -einstellungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>Konfiguration des Ziels für die Dimensionsverarbeitung  
 Das Ziel für Dimensionsverarbeitung stellt mithilfe eines Verbindungs-Managers für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eine Verbindung mit dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt oder der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] her, die die vom Ziel verarbeiteten Dimensionen enthält. Weitere Informationen finden Sie unter [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Das Ziel weist eine Eingabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Ziel-Editor für Dimensionsverarbeitung** festlegen können:  
  
-   [Ziel-Editor für Dimensionsverarbeitung &#40;Seite Verbindungs-Manager&#41;](../../integration-services/data-flow/dimension-processing-destination-editor-connection-manager-page.md)  
  
-   [Ziel-Editor für Dimensionsverarbeitung &#40;Seite Zuordnungen&#41;](../../integration-services/data-flow/dimension-processing-destination-editor-mappings-page.md)  
  
-   [Ziel-Editor für Dimensionsverarbeitung &#40;Seite Erweitert&#41;](../../integration-services/data-flow/dimension-processing-destination-editor-advanced-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften anzuzeigen, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datenfluss](../../integration-services/data-flow/data-flow.md)   
 [Integration Services-Transformationen](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
