---
title: "Transformation zum Sortieren | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sorttrans.f1"
helpviewer_keywords: 
  - "Transformation zum Sortieren"
  - "Absteigende Sortierungen"
  - "Aufsteigende Sortierungen"
  - "Sortieren von Daten [Integration Services]"
  - "Mehrere Sortierungen"
  - "Doppelt vorhandene Daten [Integration Services]"
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Transformation zum Sortieren
  Die Transformation zum Sortieren sortiert Eingabedaten in auf- oder absteigender Reihenfolge und kopiert die sortierten Daten in die Transformationsausgabe. Auf eine Eingabe können mehrere Sortierungen angewendet werden. Jede Sortierung wird durch eine Ziffer identifiziert, die die Sortierreihenfolge bestimmt. Die Spalte mit der niedrigsten Nummer wird zuerst sortiert, anschließend die Sortierungsspalte mit der zweitniedrigsten Nummer usw. Wenn z.B. die **CountryRegion**-Spalte die Sortierreihenfolge 1 und die **City**-Spalte die Sortierreihenfolge 2 aufweist, wird die Ausgabe nach Land/Region und anschließend nach dem Ort sortiert. Eine positive Zahl bedeutet eine aufsteigende Sortierung, eine negative Zahl eine absteigende Sortierung. Nicht sortierte Spalten haben die Sortierreihenfolge 0. Spalten, die nicht für die Sortierung ausgewählt sind, werden automatisch zusammen mit den sortierten Spalten in die Transformationsausgabe kopiert.  
  
 Die Transformation zum Sortieren schließt Vergleichsoptionen ein, um zu definieren, wie die Transformation die Zeichenfolgendaten in einer Spalte behandelt. Weitere Informationen finden Sie unter [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
> [!NOTE]  
>  Mit der Transformation zum Sortieren können GUIDs nicht in der Reihenfolge sortiert werden, in der sie mit der ORDER BY-Klausel in Transact-SQL sortiert werden. Mit der Transformation zum Sortieren werden GUIDs, die mit 0-9 beginnen, vor GUIDs sortiert, die mit A-F beginnen. Mit der ORDER BY-Klausel erfolgt die Sortierung entsprechend der Implementierung in [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] anders. Weitere Informationen finden Sie unter [ORDER BY-Klausel &#40;Transact-SQL&#41;](../Topic/ORDER%20BY%20Clause%20\(Transact-SQL\).md).  
  
 Mit der Transformation zum Sortieren können beim Sortieren auch doppelte Zeilen entfernt werden. Doppelte Zeilen sind Zeilen mit denselben Sortierschlüsselwerten. Der Sortierschlüsselwert wird basierend auf den verwendeten Optionen für Zeichenfolgenvergleiche generiert. Dies bedeutet, dass verschiedene Literalzeichenfolgen die gleichen Sortierschlüsselwerte aufweisen können. Die Transformation identifiziert Zeilen in den Eingabespalten mit unterschiedlichen Werten, aber mit dem gleichen Sortierschlüssel wie Duplikate.  
  
 Die Transformation zum Sortieren schließt die benutzerdefinierte Eigenschaft **MaximumThreads** ein, die beim Laden des Pakets durch einen Eigenschaftsausdruck aktualisiert werden kann. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Diese Transformation weist je eine Eingabe und eine Ausgabe auf. Fehlerausgaben werden nicht unterstützt.  
  
## Konfiguration der Transformation zum Sortieren  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Informationen zu den Eigenschaften, die Sie im Dialogfeld **Transformations-Editor für Sortierung** festlegen können, finden Sie unter [Sort Transformation Editor](../../../integration-services/data-flow/transformations/sort-transformation-editor.md).  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## Verwandte Aufgaben  
 Weitere Informationen zum Festlegen von Eigenschaften der Komponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Verwandte Inhalte  
 Beispiel, [SortDeDuplicateDelimitedString Custom SSIS-Komponente](http://go.microsoft.com/fwlink/?LinkId=220821), auf codeplex.com  
  
## Siehe auch  
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  