---
title: "Transformation für Zusammenführen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.mergetrans.f1
- sql13.dts.designer.mergetransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- merging data [Integration Services]
- Merge transformation
- combining datasets
- datasets [Integration Services], merging
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fb8e3884d531a2e5ebac5444e27aaade5495366d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="merge-transformation"></a>Transformation für Zusammenführen
  Die Transformation für Zusammenführen fasst zwei sortierte Datasets zu einem Dataset zusammen. Die Zeilen aus jedem Dataset werden basierend auf Werten in den Schlüsselspalten in die Ausgabe eingefügt.  
  
 Durch Einschließen der Transformation für Zusammenführen in einen Datenfluss können Sie die folgenden Aufgaben ausführen:  
  
-   Zusammenführen von Daten aus zwei Datenquellen, wie z. B. Tabellen und Dateien.  
  
-   Erstellen komplexer Datasets durch Schachteln von Transformationen für Zusammenführen.  
  
-   Erneutes Zusammenführen von Zeilen nach dem Korrigieren von Fehlern in den Daten.  
  
 Die Transformation für Zusammenführen ist mit den Transformationen für UNION ALL vergleichbar. Verwenden Sie die Transformation für UNION ALL in folgenden Situationen anstelle der Transformation für Zusammenführen:  
  
-   Die Transformationseingaben werden nicht sortiert.  
  
-   Die kombinierte Ausgabe muss nicht sortiert werden.  
  
-   Die Transformation weist mehr als zwei Eingaben auf.  
  
## <a name="input-requirements"></a>Eingabeanforderungen  
 Die Transformation für Zusammenführen erfordert als Eingabe sortierte Daten. Weitere Informationen zu dieser wichtigen Anforderung finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Für die Transformation für Zusammenführung müssen die zusammengeführten Spalten außerdem in ihren Ausgaben übereinstimmende Metadaten aufweisen. Beispielsweise kann eine Spalte mit einem numerischen Datentyp nicht mit einer Spalte mit einem Zeichendatentyp zusammengeführt werden. Wenn die Daten einen Zeichenfolgen-Datentyp aufweisen, muss die Länge der Spalte in der zweiten Eingabe kleiner oder gleich der Länge der Spalte in der ersten Eingabe sein, mit der diese zusammengeführt wird.  
  
 Im [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer ordnet die Benutzeroberfläche für die Transformation für Zusammenführung automatisch Spalten mit den gleichen Metadaten zu. Sie können dann manuell andere Spalten mit kompatiblen Datentypen zuordnen.  
  
 Diese Transformation weist zwei Eingaben und eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## <a name="configuration-of-the-merge-transformation"></a>Konfiguration der Zusammenführungstransformation  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu anzuzeigen, die Sie programmgesteuert festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Nähere Informationen zum Festlegen von Eigenschaften finden Sie in den folgenden Themen:  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-transformation-editor"></a>Transformations-Editor für Zusammenführen
  Mithilfe von **Transformations-Editor für Zusammenführen** können Sie angeben, dass Spalten aus zwei sortierten Datensätzen zusammengeführt werden sollen.  
  
> [!IMPORTANT]  
>  Die Transformation für Zusammenführen erfordert als Eingabe sortierte Daten. Weitere Informationen zu dieser wichtigen Anforderung finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="options"></a>Tastatur  
 **Name der Ausgabespalte**  
 Geben Sie den Namen der Ausgabespalte an.  
  
 **Eingabe 1 für Zusammenführen**  
 Wählen Sie die Spalte aus, die als Eingabe 1 für Zusammenführen zusammengeführt werden soll.  
  
 **Eingabe 2 für Zusammenführen**  
 Wählen Sie die Spalte aus, die als Eingabe 2 für Zusammenführen zusammengeführt werden soll.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Transformation für Zusammenführungsjoin](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
