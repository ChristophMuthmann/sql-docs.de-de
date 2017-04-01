---
title: "Transformation f&#252;r Zusammenf&#252;hren | Microsoft Docs"
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
  - "sql13.dts.designer.mergetrans.f1"
helpviewer_keywords: 
  - "Zusammenführen von Datasets [Integration Services]"
  - "Zusammenführen von Daten [Integration Services]"
  - "Transformation für Zusammenführen"
  - "Kombinieren von Datasets"
  - "Datasets [Integration Services], zusammenführen"
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Transformation f&#252;r Zusammenf&#252;hren
  Die Transformation für Zusammenführen fasst zwei sortierte Datasets zu einem Dataset zusammen. Die Zeilen aus jedem Dataset werden basierend auf Werten in den Schlüsselspalten in die Ausgabe eingefügt.  
  
 Durch Einschließen der Transformation für Zusammenführen in einen Datenfluss können Sie die folgenden Aufgaben ausführen:  
  
-   Zusammenführen von Daten aus zwei Datenquellen, wie z. B. Tabellen und Dateien.  
  
-   Erstellen komplexer Datasets durch Schachteln von Transformationen für Zusammenführen.  
  
-   Erneutes Zusammenführen von Zeilen nach dem Korrigieren von Fehlern in den Daten.  
  
 Die Transformation für Zusammenführen ist mit den Transformationen für UNION ALL vergleichbar. Verwenden Sie die Transformation für UNION ALL in folgenden Situationen anstelle der Transformation für Zusammenführen:  
  
-   Die Transformationseingaben werden nicht sortiert.  
  
-   Die kombinierte Ausgabe muss nicht sortiert werden.  
  
-   Die Transformation weist mehr als zwei Eingaben auf.  
  
## Eingabeanforderungen  
 Die Transformation für Zusammenführen erfordert als Eingabe sortierte Daten. Weitere Informationen zu dieser wichtigen Anforderung finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Für die Transformation für Zusammenführung müssen die zusammengeführten Spalten außerdem in ihren Ausgaben übereinstimmende Metadaten aufweisen. Beispielsweise kann eine Spalte mit einem numerischen Datentyp nicht mit einer Spalte mit einem Zeichendatentyp zusammengeführt werden. Wenn die Daten einen Zeichenfolgen-Datentyp aufweisen, muss die Länge der Spalte in der zweiten Eingabe kleiner oder gleich der Länge der Spalte in der ersten Eingabe sein, mit der diese zusammengeführt wird.  
  
 Im [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer ordnet die Benutzeroberfläche für die Transformation für Zusammenführung automatisch Spalten mit den gleichen Metadaten zu. Sie können dann manuell andere Spalten mit kompatiblen Datentypen zuordnen.  
  
 Diese Transformation weist zwei Eingaben und eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## Konfiguration der Zusammenführungstransformation  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld **Transformations-Editor für Zusammenführen** festlegen können, finden Sie unter [Merge Transformation Editor](../../../integration-services/data-flow/transformations/merge-transformation-editor.md).  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu anzuzeigen, die Sie programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## Verwandte Aufgaben  
 Nähere Informationen zum Festlegen von Eigenschaften finden Sie in den folgenden Themen:  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## Siehe auch  
 [Transformation für Zusammenführungsjoin](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Transformation für UNION ALL](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  