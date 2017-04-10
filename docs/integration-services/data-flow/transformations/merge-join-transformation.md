---
title: "Transformation f&#252;r Zusammenf&#252;hrungsjoin | Microsoft Docs"
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
  - "sql13.dts.designer.mergejointrans.f1"
helpviewer_keywords: 
  - "Datasets [Integration Services]"
  - "Transformation für Zusammenführungsjoin"
  - "Datasets [Integration Services], verknüpfen"
  - "Verknüpfen von Datasets [Integration Services]"
  - "Joins [SQL Server], SSIS"
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
caps.latest.revision: 54
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 54
---
# Transformation f&#252;r Zusammenf&#252;hrungsjoin
  Die Transformation für Zusammenführungjoins stellt eine Ausgabe bereit, die durch Verknüpfen von zwei sortierten Datasets mithilfe einer FULL JOIN-, LEFT JOIN- oder INNER JOIN-Anweisung generiert wird. Beispielsweise können Sie mit einer LEFT JOIN-Anweisung eine Tabelle, die Produktinformationen einschließt, mit einer Tabelle verknüpfen, die das Land bzw. die Region auflistet, in der ein Produkt hergestellt wurde. Das Ergebnis ist eine Tabelle, in der alle Produkte und deren Ursprungsland/-region aufgelistet sind.  
  
 Es gibt folgende Möglichkeiten, um die Transformation für Zusammenführungsjoin zu konfigurieren:  
  
-   Geben Sie die Verknüpfung mit einer FULL JOIN-, LEFT JOIN- oder INNER JOIN-Anweisung an.  
  
-   Geben Sie die vom Join verwendeten Spalten an.  
  
-   Geben Sie an, ob die Transformation NULL-Werte als identisch mit anderen NULL-Werten behandelt.  
  
    > [!NOTE]  
    >  Wenn NULL-Werte nicht als identische Werte behandelt werden, behandelt die Transformation NULL-Werte wie das SQL Server-Datenbankmodul.  
  
 Diese Transformation weist zwei Eingaben und eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## Eingabeanforderungen  
 Die Transformation für Zusammenführungsjoin erfordert als Eingabe sortierte Daten. Weitere Informationen zu dieser wichtigen Anforderung finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## Joinanforderungen  
 Für die Transformation für Zusammenführungsjoin müssen die verknüpften Spalten übereinstimmende Metadaten aufweisen. Beispielsweise kann eine Spalte mit einem numerischen Datentyp nicht mit einer Spalte mit einem Zeichendatentyp verknüpft werden. Wenn die Daten einen Zeichenfolgen-Datentyp aufweisen, muss die Länge der Spalte in der zweiten Eingabe kleiner oder gleich der Länge der Spalte in der ersten Eingabe sein, mit der diese zusammengeführt wird.  
  
## Pufferdrosselung  
 Der Wert der **MaxBuffersPerInput** -Eigenschaft muss nicht mehr konfiguriert werden, da Microsoft Änderungen vorgenommen hat, die das Risiko einer übermäßigen Arbeitsspeicherbelegung bei der Transformation für Zusammenführungsjoins reduzieren. Dieses Problem trat in einigen Fällen auf, wenn durch die Eingaben des Zusammenführungsjoins unregelmäßige Daten erzeugt wurden.  
  
## Verwandte Aufgaben  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften für diese Transformation anzuzeigen:  
  
-   [Erweitern eines Datasets mithilfe der Transformation für Zusammenführungsjoins](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## Siehe auch  
 [Transformations-Editor für Zusammenführungsjoin](../../../integration-services/data-flow/transformations/merge-join-transformation-editor.md)   
 [Transformation für Zusammenführen](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Transformation für UNION ALL](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  