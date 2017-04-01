---
title: "Entpivotierungstransformation | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.unpivottrans.f1"
helpviewer_keywords: 
  - "Entpivotierungstransformation"
  - "Mehr normalisierter Dataset [Integration Services]"
  - "Normalisierte Daten [Integration Services]"
  - "Datasets [Integration Services], normalisierte Daten"
ms.assetid: f635c64b-a9c5-4f11-9c40-9cd9d5298c5d
caps.latest.revision: 45
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 45
---
# Entpivotierungstransformation
  Die Transformation für UNPIVOT ändert ein nicht normalisiertes Dataset in eine stärker normalisierte Version, indem Werte aus mehreren Spalten in einem einzelnen Datensatz in mehrere Datensätze mit den gleichen Werten in einer einzigen Spalte erweitert werden. Angenommen, ein Dataset, das Kundennamen auflistet, weist eine Zeile pro Kunden auf, wobei die Produkte und die gekaufte Menge in Spalten in der Zeile angezeigt werden. Nachdem die Entpivotierungstransformation das Dataset normalisiert hat, enthält das Dataset eine andere Zeile für jedes Produkt, das der Kunde gekauft hat.  
  
 Im folgenden Diagramm wird ein Dataset vor dem Entpivotieren der Daten in der Product-Spalte dargestellt.  
  
 ![Dataset nach dem Entpivotieren](../../../integration-services/data-flow/transformations/media/mw-dts-18.gif "Dataset nach dem Entpivotieren")  
  
 Im folgenden Diagramm wird ein Dataset nach dem Entpivotieren in der Product-Spalte dargestellt.  
  
 ![Dataset vor dem Entpivotieren](../../../integration-services/data-flow/transformations/media/mw-dts-17.gif "Dataset vor dem Entpivotieren")  
  
 Unter einigen Umständen enthalten die Ergebnisse der Transformation für UNPIVOT möglicherweise Zeilen mit unerwarteten Werten. Wenn z.B. die im Diagramm gezeigten zu entpivotierenden Beispieldaten in allen Qty-Spalten für Fred NULL-Werte enthielten, würde die Ausgabe nur eine Zeile für Fred enthalten, nicht fünf. Die Qty-Spalte würde je nach dem Datentyp der Spalte entweder NULL oder 0 enthalten.  
  
## Konfiguration der Transformation für UNPIVOT  
 Die Transformation für UNPIVOT schließt die benutzerdefinierte Eigenschaft **PivotKeyValue** ein. Diese Eigenschaft kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Diese Transformation weist je eine Eingabe und eine Ausgabe auf. Es ist keine Fehlerausgabe vorhanden.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Editor zum Entpivotieren von Transformationen** festlegen können:  
  
-   [Editor zum Entpivotieren von Transformationen](../../../integration-services/data-flow/transformations/unpivot-transformation-editor.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  