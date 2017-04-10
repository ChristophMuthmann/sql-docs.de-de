---
title: "Editor zum Entpivotieren von Transformationen | Microsoft Docs"
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
  - "sql13.dts.designer.unpivottransformation.f1"
helpviewer_keywords: 
  - "Editor zum Entpivotieren von Transformationen"
ms.assetid: 72a36ef0-4070-4f6c-9c74-0720109617dd
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# Editor zum Entpivotieren von Transformationen
  Mithilfe des Dialogfelds **Transformations-Editor für UNPIVOT** können Sie die in Zeilen neu anzuordnenden Spalten, die Datenspalte sowie die Ausgabespalte für den neuen pivotierten Wert angeben.  
  
> [!NOTE]  
>  In diesem Thema wird die Verwendung der Optionen auf der Grundlage des in[Entpivotierungstransformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md) beschriebenen Entpivotierungsszenarios veranschaulicht.  
  
 Weitere Informationen zur Entpivotierungstransformation finden Sie unter [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md).  
  
## enthalten  
 **Verfügbare Eingabespalten**  
 Geben Sie mithilfe der Kontrollkästchen die Spalten an, die in Zeilen neu angeordnet werden sollen.  
  
 **Name**  
 Zeigt den Namen der verfügbaren Eingabespalte an.  
  
 **Pass-Through**  
 Gibt an, ob die Spalte in die entpivotierte Ausgabe eingeschlossen werden soll.  
  
 **Eingabespalte**  
 Wählen Sie für jede Zeile eine Spalte aus der Liste der verfügbaren Eingabespalten aus. Ihre Auswahl wird entsprechend in der Auswahl der Kontrollkästchen in der **Verfügbare Eingabespalten** -Tabelle deutlich.  
  
 Im Entpivotierungsszenario, das in [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)beschrieben wird, sind als Eingabespalten die Spalten **Ham**, **Soda**, **Milk**, **Beer**und **Chips** verfügbar.  
  
 **Zielspalte**  
 Geben Sie einen Namen für die Datenspalte an.  
  
 Im Entpivotierungsszenario, das in [Entpivotierungstransformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md) beschrieben wird, ist die Zielspalte die Mengenspalte (**Qty**).  
  
 **Pivotschlüsselwert**  
 Geben Sie einen Namen für den Pivotwert an. Standardmäßig wird der Name der Eingabespalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
 Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.  
  
 In dem in [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)beschriebenen Entpivotierungsszenario werden die pivotierten Werte in der neuen, durch die Option **Name der Pivotschlüsselwert-Spalte** angegebenen Product-Spalte als die Textwerte **Ham**, **Soda**, **Milk**, **Beer**und **Chips**angezeigt.  
  
 **Name der Pivotschlüsselwertspalte**  
 Geben Sie einen Namen für die Pivotwertspalte an. Standardwert ist "Pivotschlüsselwert"; Sie können jedoch einen eindeutigen, beschreibenden Namen auswählen.  
  
 In dem in [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)beschriebenen Entpivotierungsszenario lautete der Name der Pivotschlüsselwert-Spalte **Product** und bezieht sich auf die neue **Product** -Spalte, in die die Spalten **Ham**, **Soda**, **Milk**, **Beer**und **Chips** entpivotiert werden.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformation für Pivot](../../../integration-services/data-flow/transformations/pivot-transformation.md)  
  
  