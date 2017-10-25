---
title: "Hinzufügen von Spalten zu einer Tabelle (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5974a3cc-caf8-4558-8836-6e3c24b1ee23
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 170b1c7aceb4a642343f00faa6dc6ffbb3f6cbbb
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="add-columns-to-a-table-ssas-tabular"></a>Hinzufügen von Spalten zu einer Tabelle (SSAS – tabellarisch)
  In diesem Thema wird beschrieben, wie einer vorhandenen Tabelle Spalten hinzugefügt werden.  
  
## <a name="add-columns-from-the-data-source"></a>Hinzufügen von Spalten aus der Datenquelle  
 Wenn Sie Daten mit dem Tabellenimport-Assistenten aus einer Tabelle der Datenquelle importieren, wird eine neue Tabelle im Modell erstellt, die alle Spalten der Quelltabelle oder, falls Sie bestimmte Spalten mit der Vorschau- und Filterfunktion herausfiltern, nur die ausgewählten Spalten und gefilterten Daten enthält. Sie können auch eine SQL-Abfrage schreiben, durch die bestimmte Spalten für den Import angegeben werden. Wenn Sie feststellen, dass eine Quelltabelle über zusätzliche Spalten verfügt, die Sie der Modelltabelle hinzufügen möchten, oder wenn eine berechnete Spalte mit Werten hinzugefügt werden soll, die von einer DAX-Formel abgeleitet sind, haben Sie später noch Gelegenheit dazu.  
  
 Wenn Sie die Spalten z. B. ursprünglich aus einer Datenquelle importiert und dabei die Vorschau- und Filterfunktion im Tabellenimport-Assistenten verwendet haben, um eine begrenzte Anzahl von Spalten aus der Quelltabelle auszuwählen, stellen Sie möglicherweise später fest, dass Sie eine weitere Spalte hinzufügen müssen, die zwar in der Quelltabelle, aber noch nicht in der Modelltabelle vorhanden ist. Oder der FactSales-Tabelle in der Datenquelle wurde eine neue AdjustedProfit-Spalte hinzugefügt und die gleiche AdjustedProfit-Spalte soll der Sales-Tabelle im Modell hinzugefügt werden.  
  
 In diesen Fällen können Sie das Dialogfeld Tabelleneigenschaften bearbeiten verwenden, um Spalten in der Quelltabelle auszuwählen und sie der Modelltabelle hinzuzufügen. Das Dialogfeld Tabelleneigenschaften bearbeiten enthält das Tabellenvorschaufenster. Im Tabellenvorschaufenster wird die Tabelle an ihrem Quellspeicherort angezeigt. Spalten, die sich bereits in der Tabellendefinition des Modells befinden, sind automatisch ausgewählt. Dagegen sind Spalten, die noch nicht in der Tabellendefinition des Modells enthalten sind, nicht ausgewählt. Sie können der Tabellendefinition des Modells Spalten aus der Quelle hinzufügen, indem Sie die Spalte auswählen und auf OK klicken. Das Tabellenvorschaufenster im Dialogfeld Tabelleneigenschaften bearbeiten verfügt über die gleiche Ansicht und die gleichen Funktionen wie das Tabellenvorschaufenster, das sich im Tabellenimport-Assistenten auf der Seite Vorschau und Filter befindet.  
  
> [!IMPORTANT]  
>  Wenn Sie einer Tabelle, die mindestens zwei Partitionen enthält, eine Spalte hinzufügen, bevor diese Spalte der Tabellendefinition mithilfe des Dialogfelds Tabelleneigenschaften bearbeiten hinzugefügt wurde, müssen Sie die Spalte zunächst allen definierten Partitionen mithilfe des Partitions-Managers hinzufügen. Nachdem Sie den definierten Partitionen die Spalte hinzugefügt haben, können Sie der Tabellendefinition die gleiche Spalte mithilfe des Dialogfelds Tabelleneigenschaften bearbeiten hinzufügen.  
  
> [!NOTE]  
>  Wenn Tabellen und Spalten mittels einer SQL-Abfrage ausgewählt wurden, als Sie die Daten ursprünglich mit dem Tabellenimport-Assistenten importiert haben, müssen Sie erneut eine SQL-Abfrage im Dialogfeld Tabelleneigenschaften bearbeiten verwenden, um der Modelltabelle Spalten hinzuzufügen.  
  
#### <a name="to-add-a-column-from-the-data-source-by-using-the-edit-table-properties-dialog-box"></a>So fügen Sie mithilfe des Dialogfelds Tabelleneigenschaften bearbeiten eine Spalte aus der Datenquelle hinzu  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle, der Sie eine Spalte hinzufügen möchten, klicken Sie auf das Menü **Tabelle** und dann auf  **Tabelleneigenschaften**.  
  
2.  Wählen Sie im Dialogfeld **Tabelleneigenschaften bearbeiten** im Tabellenvorschaufenster die Quellspalte aus, die Sie hinzufügen möchten, und klicken Sie dann auf OK. Die bereits in der Tabellendefinition enthaltenen Spalten sind automatisch ausgewählt.  
  
## <a name="add-a-calculated-column"></a>Hinzufügen einer berechneten Spalte  
 In einer berechneten Spalte wird eine DAX-Formel verwendet, um einen Wert pro Zeile zu definieren. Beispielsweise können Sie eine berechnete Spalte mit einer einfachen Formel (= 1) erstellen, durch die jeder Zeile der Wert 1 hinzugefügt wird. Berechnete Spalten können auch komplexere Formeln enthalten, durch die Werte auf der Grundlage anderer Modelldaten berechnet werden. Berechnete Spalten werden in anderen Themen ausführlich behandelt. Weitere Informationen finden Sie unter [Berechnete Spalten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/ssas-calculated-columns.md).  
  
#### <a name="to-create-a-calculated-column"></a>So erstellen Sie eine berechnete Spalte  
  
1.  Wählen Sie im Modell-Designer in der Datensicht die Tabelle aus, der Sie eine neue, leere berechnete Spalte hinzufügen möchten, scrollen Sie zur äußersten rechten Spalte, oder klicken Sie auf das Menü **Spalte** und dann auf **Spalte hinzufügen**.  
  
     Um zwischen zwei vorhandenen Spalten eine neue Spalte zu erstellen, klicken Sie mit der rechten Maustaste auf eine vorhandene Spalte, und klicken Sie dann auf **Spalte einfügen**.  
  
2.  Geben Sie in der Bearbeitungsleiste eine DAX-Formel ein, um Attribute für jede Zeile hinzuzufügen.  
  
## <a name="add-a-blank-column"></a>Hinzufügen einer leeren Spalte  
 Sie können eine benannte, leere Spalte in einer Modelltabelle erstellen. Leere Spalten können hilfreich sein, wenn Sie Daten aus einer anderen Quelle einfügen möchten. Bedenken Sie jedoch, dass eingefügte Daten anders gespeichert werden als importierte Daten. Weitere Informationen finden Sie unter [Kopieren und Einfügen von Daten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md).  
  
#### <a name="to-create-a-named-blank-column"></a>So erstellen Sie eine benannte, leere Spalte  
  
1.  Wählen Sie im Modell-Designer in der Datensicht die Tabelle aus, der Sie eine leere Spalte hinzufügen möchten, scrollen Sie zur äußerst rechten Spalte, oder klicken Sie auf das Menü **Spalte** und dann auf **Spalte hinzufügen**.  
  
     Klicken Sie mit der rechten Maustaste auf eine vorhandene Spalte, und klicken Sie dann auf **Spalte einfügen**, um zwischen zwei vorhandenen Spalten eine neue Spalte zu erstellen.  
  
2.  Klicken Sie auf die oberste Zelle, geben Sie einen Namen ein, und drücken Sie die EINGABETASTE.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabelleneigenschaften bearbeiten &#40; Dialogfeld, SSAS&#41;](http://msdn.microsoft.com/library/8d913e83-7246-44cc-8fc7-31729023c0d8)   
 [Ändern von Tabellen-, Spalten- oder Zeilenfilterzuordnungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/change-table-column-or-row-filter-mappings-ssas-tabular.md)  
  
  

