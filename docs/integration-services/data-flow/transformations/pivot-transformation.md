---
title: "Transformation für Pivot | Microsoft-Dokumentation"
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
- sql13.dts.designer.pivottrans.f1
helpviewer_keywords:
- Pivot transformation
- normalized data [Integration Services]
- PivotUsage property
- datasets [Integration Services], normalized data
- less normalized data set [Integration Services]
ms.assetid: 55f5db6e-6777-435f-8a06-b68c129f8437
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 41e027c10bfdb1e9309c6ee1226694c1c9601837
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="pivot-transformation"></a>Transformation für Pivot
  Die Transformation für Pivot macht aus einem normalisierten Dataset eine weniger normalisierte, aber kompaktere Version, indem die Eingabedaten nach einem Spaltenwert pivotiert werden. Beispielsweise weist ein normalisiertes **Orders** -Dataset, das den Kundennamen, das Produkt und die gekaufte Menge auflistet, in der Regel mehrere Zeilen für jeden Kunden auf, der mehrere Produkte gekauft hat. Dabei zeigt jede Zeile für den betreffenden Kunden Bestelldetails für ein anderes Produkt an. Durch Pivotieren des Datasets nach der Produktspalte kann mit der Transformation für Pivot ein Dataset mit einer einzigen Zeile pro Kunde ausgegeben werden. In dieser Zeile werden alle Einkäufe des Kunden aufgelistet, wobei die Produktnamen als Spaltennamen und die Menge als Wert in der Produktspalte angezeigt werden. Da nicht jeder Kunde jedes Produkt kauft, können viele Spalten NULL-Werte enthalten.  
  
 Wenn ein Dataset pivotiert wird, übernehmen Eingabespalten unterschiedliche Rollen am Pivotvorgang. Für die Beteiligung einer Spalte gibt es folgende Möglichkeiten:  
  
-   Die Spalte wird unverändert an die Ausgabe übergeben. Viele Eingabezeilen können nur eine Ausgabezeile ergeben, weshalb die Transformation nur den ersten Eingabewert für die Spalte kopiert.  
  
-   Die Spalte dient als Schlüssel oder Teil des Schlüssels, mit dem ein Recordset definiert wird.  
  
-   Die Spalte definiert den Pivotvorgang. Die Werte in dieser Spalte sind Spalten im pivotierten Dataset zugeordnet.  
  
-   Die Spalte enthält Werte, die den Spalten hinzugefügt werden, die beim Pivotieren erstellt werden.  
  
 Diese Transformation weist eine Eingabe, eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
## <a name="sort-and-duplicate-rows"></a>Sortieren und doppelte Zeilen  
 Die Eingabedaten müssen in der Pivotspalte sortiert sein, damit die Daten effizient pivotiert werden, das heißt, dass möglichst wenige Datensätze im Ausgabedataset erstellt werden. Wenn die Daten nicht sortiert sind, kann es sein, dass die Transformation für Pivot mehrere Datensätze für jeden Wert im festgelegten Schlüssel generiert, bei dem es sich um die Spalte handelt, die die festgelegte Mitgliedschaft definiert. Wenn beispielsweise ein Dataset nach der **Name** -Spalte pivotiert wird, aber die Namen nicht sortiert sind, könnte das Ausgabedataset pro Kunde mehrere Zeilen aufweisen, denn ein Pivotvorgang wird jedes Mal ausgeführt, wenn der Wert in der **Name** -Spalte geändert wird.  
  
 Die Eingabedaten können doppelte Zeilen enthalten. Diese bewirken, dass die Transformation für Pivot einen Fehler erzeugt. "Doppelte Zeilen" bedeutet Zeilen, die in den festgelegten Schlüsselspalten und Pivotspalten die gleichen Werte aufweisen. Zur Vermeidung von Fehlern können Sie entweder die Transformation so konfigurieren, dass Fehlerzeilen in eine Fehlerausgabe umgeleitet werden, oder Sie können Werte vorab aggregieren, um sicherzustellen, dass keine doppelten Zeilen vorhanden sind.  
  
##  <a name="options"></a> Optionen im Dialogfeld "Pivot"  
 Sie konfigurieren den Pivotvorgang, indem Sie die Optionen im Dialogfeld **Pivot** festlegen. Um das Dialogfeld **Pivot** zu öffnen, fügen Sie dem Paket die Pivottransformation in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]hinzu. Klicken Sie anschließend mit der rechten Maustaste auf die Komponente, und klicken Sie dann auf **Bearbeiten**.  
  
 In der folgenden Liste werden die Optionen des Dialogfelds **Pivot** beschrieben.  
  
 **Pivotschlüssel**  
 Gibt die Spalte an, die für Werte über der obersten Zeile (Kopfzeile) der Tabelle verwendet wird.  
  
 **Schlüssel festlegen**  
 Gibt die zu verwendende Spalte für Werte in der linken Spalte der Tabelle an. Das Eingabedatum muss nach dieser Spalte sortiert werden.  
  
 **Pivotwert**  
 Gibt die zu verwendende Spalte für die Tabellenwerte an, die sich von den Werten in der Kopfzeile und in der linken Spalte unterscheiden.  
  
 **Nicht übereinstimmende Pivotschlüsselwerte ignorieren und nach DataFlow-Ausführung melden**  
 Aktivieren Sie diese Option, um die Pivottransformation so zu konfigurieren, dass Zeilen ignoriert werden, die nicht erkannte Werte in der Spalte **Pivotschlüssel** enthalten und dass alle Pivotschlüsselwerte zu einer Protokollmeldung ausgegeben werden, wenn das Paket ausgeführt wird.  
  
 Sie können auch die Transformation konfigurieren, die Werte auszugeben, indem Sie die benutzerdefinierte Eigenschaft von **PassThroughUnmatchedPivotKeys** auf **True**festlegen.  
  
 **Pivotausgabespalten aus Werten generieren**  
 Geben Sie die Pivotschlüsselwerte in diesem Feld ein, um die Pivottransformation zu aktivieren, um Ausgabespalten für jeden Wert zu erstellen. Sie können entweder die Werte vor dem Ausführen des Pakets eingeben oder wie folgt vorgehen.  
  
1.  Wählen Sie die Option **Nicht übereinstimmende Pivotschlüsselwerte ignorieren und nach DataFlow-Ausführung melden** aus, und klicken Sie im Dialogfeld **Pivot** auf **OK** , um die Änderungen in Bezug auf die Pivottransformation zu speichern.  
  
2.  Führen Sie das Paket aus.  
  
3.  Wenn das Paket erfolgreich ist, klicken Sie auf die Registerkarte **Status** , und suchen Sie nach der Informationsprotokollmeldung der Pivottransformation, die die Pivotschlüsselwerte enthält.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Meldung, und klicken Sie auf **Meldungstext kopieren**.  
  
5.  Klicken Sie im Menü **Debuggen** auf **Debuggen beenden** , um in den Entwurfsmodus zu wechseln.  
  
6.  Klicken mit der rechten Maustaste auf die Pivottransformation, und wählen Sie dann **Bearbeiten**aus.  
  
7.  Deaktivieren Sie die Option **Nicht übereinstimmende Pivotschlüsselwerte ignorieren und nach DataFlow-Ausführung melden** , und fügen Sie die Pivotschlüsselwerte anschließend in das Feld **Pivotausgabespalten aus Werten generieren** im folgenden Format ein.  
  
     [value1],[value2],[value3]  
  
 **Jetzt Spalten generieren**  
 Klicken Sie auf diese Option, um eine Ausgabespalte für jeden Pivotschlüsselwert zu erstellen, der im Feld **Pivotausgabespalten aus Werten generieren** aufgelistet ist.  
  
 Die Ausgabespalten werden im Feld **Vorhandene pivotierte Ausgabespalten** angezeigt.  
  
 **Vorhandene pivotierte Ausgabespalten**  
 Listet die Ausgabespalten für die Pivotschlüsselwerte auf.  
  
 In der folgenden Tabelle wird ein Dataset vor dem Anwenden der Pivotierung auf die **Jahr** -Spalte dargestellt.  
  
|Jahr|Produktname|Total|  
|----------|------------------|-----------|  
|2004|HL Mountain Tire|1504884.15|  
|2003|Road Tire Tube|35920.50|  
|2004|Water Bottle – 30 oz.|2805.00|  
|2002|Touring Tire|62364.225|  
  
 In der folgenden Tabelle wird ein Dataset nach dem Pivotieren der Daten nach der **Jahr** -Spalte angezeigt.  
  
||2002|2003|2004|  
|-|----------|----------|----------|  
|HL Mountain Tire|141164.10|446297.775|1504884.15|  
|Road Tire Tube|3592.05|35920.50|89801.25|  
|Water Bottle – 30 oz.|*NULL*|*NULL*|2805.00|  
|Touring Tire|62364.225|375051.60|1041810.00|  
  
 Zum Pivotisieren der Daten für die **Jahr** -Spalte (wie oben gezeigt) müssen die folgenden Optionen im Dialogfeld **Pivot** festgelegt werden.  
  
-   Im Listenfeld **Pivot Key** wird Jahr ausgewählt.  
  
-   Im Listenfeld **Schlüssel festlegen** wird Produktname ausgewählt.  
  
-   Im Listenfeld **Pivotwert** wird Gesamt ausgewählt.  
  
-   Die folgenden Werte werden im Feld **Pivotausgabespalten aus Werten generieren** eingegeben.  
  
     [2002],[2003],[2004]  
  
## <a name="configuration-of-the-pivot-transformation"></a>Konfiguration der Transformation für Pivot  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Informationen zum Festlegen der Eigenschaften dieser Komponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Entpivotierungstransformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)   
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
