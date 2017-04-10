---
title: "Lektion 5: Erstellen von Beziehungen | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lektion 5: Erstellen von Beziehungen
In dieser Lektion überprüfen Sie die Beziehungen, die beim Importieren von Daten automatisch erstellt wurden. Zudem fügen Sie neue Beziehungen zwischen verschiedenen Tabellen hinzu. Eine Beziehung ist eine Verbindung zwischen zwei Tabellen, die festlegt, wie die Daten in diesen Tabellen miteinander in Beziehung gesetzt werden sollen. Die Product-Tabelle und die Product Subcategory-Tabelle haben beispielsweise eine Beziehung, die darauf beruht, dass jedes Produkt zu einer Unterkategorie gehört. Weitere Informationen finden Sie unter [Beziehungen &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **10 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 3: Umbenennen von Spalten](../analysis-services/lesson-3-rename-columns.md).  
  
## Überprüfen vorhandener Beziehungen und Hinzufügen neuer Beziehungen  
Wenn Sie Daten mithilfe des Tabellenimport-Assistenten importiert haben, wurden sieben Tabellen aus der AdventureWorksDW-Datenbank importiert. Im Allgemeinen werden vorhandene Beziehungen automatisch zusammen mit den Daten importiert, wenn Sie Daten von einer relationalen Quelle importieren. Bevor Sie jedoch mit der Erstellung des Modells fortfahren, überprüfen Sie, ob die Beziehungen zwischen den Tabellen ordnungsgemäß erstellt wurden. In diesem Lernprogramm fügen Sie auch drei neue Beziehungen hinzu.  
  
#### So überprüfen Sie vorhandene Beziehungen  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] auf das Menü **Modell**, zeigen Sie auf **Modellansicht**, und klicken Sie anschließend auf **Diagrammsicht**.  
  
    Der Modell-Designer wird jetzt in der Diagrammsicht angezeigt. Hierbei handelt es sich um ein grafisches Format, in dem alle von Ihnen importierten Tabellen mit Zeilen zwischen den Tabellen angezeigt werden. Die Zeilen zwischen den Tabellen geben die Beziehungen an, die automatisch beim Importieren der Daten erstellt wurden.  
  
    Verwenden Sie die Steuerelemente der Miniaturkarte unten rechts im Modell-Designer, um die Sicht so anzupassen, dass so viele Tabellen wie möglich berücksichtigt werden. Sie können auch mittels Klick und Ziehen Tabellen verschieben, näher zu einander positionieren oder in einer bestimmten Reihenfolge anordnen. Das Verschieben von Tabellen beeinflusst nicht die bereits zwischen den Tabellen bestehenden Beziehungen. Klicken Sie zum Anzeigen aller Spalten in einer bestimmten Tabelle auf einen Tabellenrand, und ziehen Sie diesen, um die Tabelle zu erweitern oder zu verkleinern.  
  
2.  Klicken Sie zwischen der Tabelle **Customer** und der Tabelle **Geography** auf die durchgezogene Linie. Die durchgezogene Linie zwischen diesen zwei Tabellen zeigt an, dass diese Beziehung aktiv ist. Sie wird folglich bei der Berechnung von DAX-Formeln standardmäßig verwendet.  
  
    Beachten Sie, dass die Spalte **Geography Id** in der Tabelle **Customer** und die Spalte **Geography Id** in der Tabelle **Geography** jetzt jeweils innerhalb eines Felds angezeigt werden. Dies gibt an, dass es sich hierbei um die in der Beziehung verwendeten Spalten handelt. Die Eigenschaften der Beziehung werden jetzt auch im Fenster **Eigenschaften** angezeigt.  
  
    > [!TIP]  
    > Zusätzlich zum Verwenden des Modell-Designers in der Diagrammsicht können Sie auch das Dialogfeld **Beziehungen verwalten** verwenden, um die Beziehungen zwischen allen Tabellen in einem Tabellenformat anzuzeigen. Klicken Sie im Menü **Tabelle** auf **Beziehungen verwalten**. Das Dialogfeld **Beziehungen verwalten** zeigt die Beziehungen an, die beim Importieren von Daten automatisch erstellt wurden.  
  
3.  Verwenden Sie den Modell-Designer in der Diagrammsicht oder das Dialogfeld **Beziehungen verwalten**, um zu überprüfen, ob die folgenden Beziehungen erstellt wurden, als jede der Tabellen aus der AdventureWorksDW-Datenbank importiert wurde:  
  
    |Active|Tabelle|Verknüpfte Suchtabelle|  
    |----------|---------|------------------------|  
    |Ja|**Customer [Geography Id]**|**Geography [Geography Id]**|  
    |Ja|**Product [Product Subcategory Id]**|**Product Subcategory [Product Subcategory Id]**|  
    |Ja|**Product Subcategory [Product Category Id]**|**Product Category [Product Category Id]**|  
    |Ja|**Internet Sales [Customer Id]**|**Customer [Customer Id]**|  
    |Ja|**Internet Sales [Product Id]**|**Product [Product Id]**|  
  
Fehlt eine der in der oben stehenden Tabelle angegebenen Beziehungen, stellen Sie sicher, dass das Modell die folgenden Tabellen beinhaltet: Customer, Date, Geography, Product, Product Category, Product Subcategory und Internet Sales. Werden Tabellen über die gleiche Datenquellenverbindung zu unterschiedlichen Zeitpunkten importiert, werden Beziehungen zwischen diesen Tabellen nicht automatisch erstellt, sondern sind manuell zu erstellen.  
  
In einigen Fällen müssen Sie möglicherweise zusätzliche Beziehungen zwischen Tabellen im Modell erstellen, um eine bestimmte Geschäftslogik zu unterstützen. Für dieses Lernprogramm müssen Sie drei zusätzliche Beziehungen zwischen der Internet Sales-Tabelle und der Date-Tabelle erstellen.  
  
#### So fügen Sie neue Beziehungen zwischen Tabellen hinzu  
  
1.  Klicken Sie im Modell-Designer in der Tabelle **Internet Sales** auf die Spalte **Order Date**, und halten Sie sie gedrückt. Verschieben Sie die Spalte anschließend mit dem Cursor per Drag & Drop in die Spalte **Date** der Tabelle **Date**.  
  
    Eine durchgezogene Linie wird angezeigt. Diese bedeutet, dass Sie eine aktive Beziehung zwischen der Spalte **Order Date** in der Tabelle **Internet Sales** und der Spalte **Date** in der Tabelle **Date** erstellt haben.  
  
    > [!NOTE]  
    > Bei der Erstellung von Beziehungen wird die Reihenfolge zwischen der primären Tabelle und der zugehörigen Nachschlagetabelle automatisch entsprechend angepasst.  
  
2.  Klicken Sie in der Tabelle **Internet Sales** auf die Spalte **Due Date**, und halten Sie sie gedrückt. Verschieben Sie die Spalte anschließend mit dem Cursor per Drag & Drop in die Spalte **Date** der Tabelle **Date**.  
  
    Eine gepunktete Linie wird angezeigt. Diese bedeutet, dass Sie eine inaktive Beziehung zwischen der Spalte **Due Date** in der Tabelle **Internet Sales** und der Spalte **Date** in der Tabelle **Date** erstellt haben. Mehrere Beziehungen zwischen Tabellen sind möglich. Doch nur eine Beziehung kann jeweils aktiv sein.  
  
3.  Erstellen Sie abschließend eine weitere Beziehung. Klicken Sie in der Tabelle **Internet Sales** auf die Spalte **Ship Date**, und halten Sie die Auswahl gedrückt. Verschieben Sie die Auswahl anschließend mit dem Cursor per Drag & Drop in die Spalte **Date** der Tabelle **Date**.  
  
    Eine gepunktete Linie wird angezeigt. Diese bedeutet, dass Sie eine inaktive Beziehung zwischen der Spalte **Ship Date** in der Tabelle **Internet Sales** und der Spalte **Date** in der Tabelle **Date** erstellt haben.  
  
## Nächster Schritt  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 6: Erstellen von berechneten Spalten](../analysis-services/lesson-6-create-calculated-columns.md).  
  
  
  
