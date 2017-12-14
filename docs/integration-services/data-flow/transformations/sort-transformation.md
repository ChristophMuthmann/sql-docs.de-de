---
title: Transformation zum Sortieren | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
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
- sql13.dts.designer.sorttrans.f1
- sql13.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
caps.latest.revision: "50"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d7bd6daad055d9fd72d0f67c219499084940501b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sort-transformation"></a>Transformation zum Sortieren
  Die Transformation zum Sortieren sortiert Eingabedaten in auf- oder absteigender Reihenfolge und kopiert die sortierten Daten in die Transformationsausgabe. Auf eine Eingabe können mehrere Sortierungen angewendet werden. Jede Sortierung wird durch eine Ziffer identifiziert, die die Sortierreihenfolge bestimmt. Die Spalte mit der niedrigsten Nummer wird zuerst sortiert, anschließend die Sortierungsspalte mit der zweitniedrigsten Nummer usw. Wenn z.B. die **CountryRegion** -Spalte die Sortierreihenfolge 1 und die **City** -Spalte die Sortierreihenfolge 2 aufweist, wird die Ausgabe nach Land/Region und anschließend nach dem Ort sortiert. Eine positive Zahl bedeutet eine aufsteigende Sortierung, eine negative Zahl eine absteigende Sortierung. Nicht sortierte Spalten haben die Sortierreihenfolge 0. Spalten, die nicht für die Sortierung ausgewählt sind, werden automatisch zusammen mit den sortierten Spalten in die Transformationsausgabe kopiert.  
  
 Die Transformation zum Sortieren schließt Vergleichsoptionen ein, um zu definieren, wie die Transformation die Zeichenfolgendaten in einer Spalte behandelt. Weitere Informationen finden Sie unter [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
> [!NOTE]  
>  Mit der Transformation zum Sortieren können GUIDs nicht in der Reihenfolge sortiert werden, in der sie mit der ORDER BY-Klausel in Transact-SQL sortiert werden. Mit der Transformation zum Sortieren werden GUIDs, die mit 0-9 beginnen, vor GUIDs sortiert, die mit A-F beginnen. Mit der ORDER BY-Klausel erfolgt die Sortierung entsprechend der Implementierung in [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] anders. Weitere Informationen finden Sie unter [ORDER BY-Klausel &#40;Transact-SQL&#41;](../../../t-sql/queries/select-order-by-clause-transact-sql.md).  
  
 Mit der Transformation zum Sortieren können beim Sortieren auch doppelte Zeilen entfernt werden. Doppelte Zeilen sind Zeilen mit denselben Sortierschlüsselwerten. Der Sortierschlüsselwert wird basierend auf den verwendeten Optionen für Zeichenfolgenvergleiche generiert. Dies bedeutet, dass verschiedene Literalzeichenfolgen die gleichen Sortierschlüsselwerte aufweisen können. Die Transformation identifiziert Zeilen in den Eingabespalten mit unterschiedlichen Werten, aber mit dem gleichen Sortierschlüssel wie Duplikate.  
  
 Die Transformation zum Sortieren schließt die benutzerdefinierte Eigenschaft **MaximumThreads** ein, die beim Laden des Pakets durch einen Eigenschaftsausdruck aktualisiert werden kann. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Diese Transformation weist je eine Eingabe und eine Ausgabe auf. Fehlerausgaben werden nicht unterstützt.  
  
## <a name="configuration-of-the-sort-transformation"></a>Konfiguration der Transformation zum Sortieren  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Weitere Informationen zum Festlegen von Eigenschaften der Komponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Beispiel, [SortDeDuplicateDelimitedString Custom SSIS-Komponente](http://go.microsoft.com/fwlink/?LinkId=220821), auf codeplex.com  
  
## <a name="sort-transformation-editor"></a>Transformations-Editor für Sortierung
  Mithilfe des Dialogfelds **Transformations-Editor für Sortierung** können Sie die zu sortierenden Spalten auswählen, die Sortierreihenfolge festlegen und angeben, ob Duplikate entfernt werden.  
  
### <a name="options"></a>enthalten  
 **Verfügbare Eingabespalten**  
 Geben Sie mithilfe der Kontrollkästchen die zu sortierenden Spalten an.  
  
 **Name**  
 Zeigen Sie den Namen jeder verfügbaren Eingabespalte an.  
  
 **Passthrough**  
 Geben Sie an, ob die Spalte in der sortierten Ausgabe eingeschlossen werden soll.  
  
 **Eingabespalte**  
 Wählen Sie für jede Zeile eine Spalte aus der Liste der verfügbaren Eingabespalten aus. Ihre Auswahl wird entsprechend in der Auswahl der Kontrollkästchen in der **Verfügbare Eingabespalten** -Tabelle deutlich.  
  
 **Ausgabealias**  
 Geben Sie einen Alias für jede Spalte ein. Standardmäßig wird der Name der Eingabespalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
 **Sortiertyp**  
 Geben Sie an, ob in aufsteigender oder absteigender Reihenfolge sortiert wird.  
  
 **Sortierreihenfolge**  
 Geben Sie die Reihenfolge an, in der die Spalten sortiert werden. Diese Einstellung muss manuell für jede Spalte vorgenommen werden.  
  
 **Vergleichsflags**  
 Weitere Informationen zu den Optionen für das Vergleichen von Zeichenfolgen finden Sie unter [Vergleichen von Zeichenfolgendaten](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Zeilen mit doppelten Sortierwerten entfernen**  
 Geben Sie an, ob die Transformation doppelte Zeilen in die Transformationsausgabe kopiert oder einen einzelnen Eintrag für alle Duplikate erstellt, basierend auf den angegebenen Optionen für den Zeichenfolgenvergleich.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
