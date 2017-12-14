---
title: "Transformation für Zusammenführungsjoin | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.mergejointrans.f1
- sql13.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
caps.latest.revision: "54"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7e9daf9c88882acb90097ce12495db9cab775290
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="merge-join-transformation"></a>Transformation für Zusammenführungsjoin
  Die Transformation für Zusammenführungjoins stellt eine Ausgabe bereit, die durch Verknüpfen von zwei sortierten Datasets mithilfe einer FULL JOIN-, LEFT JOIN- oder INNER JOIN-Anweisung generiert wird. Beispielsweise können Sie mit einer LEFT JOIN-Anweisung eine Tabelle, die Produktinformationen einschließt, mit einer Tabelle verknüpfen, die das Land bzw. die Region auflistet, in der ein Produkt hergestellt wurde. Das Ergebnis ist eine Tabelle, in der alle Produkte und deren Ursprungsland/-region aufgelistet sind.  
  
 Es gibt folgende Möglichkeiten, um die Transformation für Zusammenführungsjoin zu konfigurieren:  
  
-   Geben Sie die Verknüpfung mit einer FULL JOIN-, LEFT JOIN- oder INNER JOIN-Anweisung an.  
  
-   Geben Sie die vom Join verwendeten Spalten an.  
  
-   Geben Sie an, ob die Transformation NULL-Werte als identisch mit anderen NULL-Werten behandelt.  
  
    > [!NOTE]  
    >  Wenn NULL-Werte nicht als identische Werte behandelt werden, behandelt die Transformation NULL-Werte wie das SQL Server-Datenbankmodul.  
  
 Diese Transformation weist zwei Eingaben und eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## <a name="input-requirements"></a>Eingabeanforderungen  
 Die Transformation für Zusammenführungsjoin erfordert als Eingabe sortierte Daten. Weitere Informationen zu dieser wichtigen Anforderung finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## <a name="join-requirements"></a>Joinanforderungen  
 Für die Transformation für Zusammenführungsjoin müssen die verknüpften Spalten übereinstimmende Metadaten aufweisen. Beispielsweise kann eine Spalte mit einem numerischen Datentyp nicht mit einer Spalte mit einem Zeichendatentyp verknüpft werden. Wenn die Daten einen Zeichenfolgen-Datentyp aufweisen, muss die Länge der Spalte in der zweiten Eingabe kleiner oder gleich der Länge der Spalte in der ersten Eingabe sein, mit der diese zusammengeführt wird.  
  
## <a name="buffer-throttling"></a>Pufferdrosselung  
 Der Wert der **MaxBuffersPerInput** -Eigenschaft muss nicht mehr konfiguriert werden, da Microsoft Änderungen vorgenommen hat, die das Risiko einer übermäßigen Arbeitsspeicherbelegung bei der Transformation für Zusammenführungsjoins reduzieren. Dieses Problem trat in einigen Fällen auf, wenn durch die Eingaben des Zusammenführungsjoins unregelmäßige Daten erzeugt wurden.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften für diese Transformation anzuzeigen:  
  
-   [Erweitern eines Datasets mithilfe der Transformation für Zusammenführungsjoins](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-join-transformation-editor"></a>Transformations-Editor für Zusammenführungsjoin
  Im Dialogfeld **Transformations-Editor für Zusammenführungsjoin** geben Sie den Jointyp, die Joinspalten und die Ausgabespalten für zwei Eingaben an, die durch einen Join zusammengeführt werden.  
  
> [!IMPORTANT]  
>  Die Transformation für Zusammenführungsjoin erfordert als Eingabe sortierte Daten. Weitere Informationen zu dieser wichtigen Anforderung finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="options"></a>enthalten  
 **Jointyp**  
 Geben Sie an, ob Sie einen inneren Join, einen linken äußeren Join oder einen vollständigen Join verwenden möchten.  
  
 **Eingaben vertauschen**  
 Schalten Sie die Reihenfolge der Eingaben mithilfe der Schaltfläche **Eingaben vertauschen** um. Diese Option kann sich bei linkem äußeren Join als nützlich erweisen.  
  
 **Eingabe**  
 Wählen Sie alle Spalten, die zur zusammengeführten Ausgabe gehören sollen, in der Liste der verfügbaren Eingaben aus.  
  
 Eingaben werden in zwei separaten Tabellen angezeigt. Wählen Sie die Spalten aus, die in die Eingabe eingeschlossen werden sollen. Verschieben Sie die Spalten, um einen Join zwischen den Tabellen zu erstellen. Um einen Join zu löschen, wählen Sie diesen aus und drücken dann ENTF.  
  
 **Eingabespalte**  
 Wählen Sie eine Spalte, die in die zusammengeführte Ausgabe eingeschlossen werden soll, in der Liste der für die ausgewählte Eingabe verfügbaren Spalten aus.  
  
 **Ausgabealias**  
 Geben Sie einen Alias für jede Spalte ein. Standardmäßig wird der Name der Eingabespalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Transformation für Zusammenführen](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
