---
title: "L&#246;schen einer Spalte (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
caps.latest.revision: 5
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 5
---
# L&#246;schen einer Spalte (SSAS – tabellarisch)
  In diesem Thema wird beschrieben, wie eine Spalte aus einer Tabelle eines tabellarische Modells gelöscht wird.  
  
## Löschen von Modelltabellenspalten  
  
> [!NOTE]  
>  Wenn Sie eine Spalte aus einer Modelltabelle löschen, wird die Spalte nicht aus einer Partitionsabfragedefinition gelöscht. Falls die Spalte, die Sie löschen, Teil einer Partition ist, müssen Sie die Spalte manuell aus der Partitionsabfragedefinition löschen. Wenn Sie die Spalte nicht aus der Partitionsabfragedefinition löschen, wird die Spalte bei Verarbeitungsvorgängen abgefragt und Daten zurückgegeben, aber nicht in der Modelltabelle ausgefüllt. Weitere Informationen finden Sie unter [Partitionen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### So löschen Sie eine Modelltabellenspalte  
  
-   Klicken Sie im Modell-Designer in der Tabelle, die die Spalte enthält, mit der rechten Maustaste auf die Spalte und anschließend auf **Löschen**.  
  
#### So löschen Sie mithilfe des Dialogfelds 'Tabelleneigenschaften' eine Modelltabellenspalte  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle, die die zu löschende Spalte enthält, klicken Sie auf das Menü **Tabelle** und dann auf  **Tabelleneigenschaften**.  
  
2.  Wählen Sie unter **Spaltennamen aus** die Option **Modell** aus, *um Modelltabellen-Spaltennamen zu verwenden, falls diese von der Quelle abweichen*.  
  
3.  Deaktivieren Sie im Dialogfeld **Tabelleneigenschaften bearbeiten** im Tabellenvorschaufenster die Spalte, die Sie löschen möchten, und klicken Sie dann auf **OK**.  
  
## Siehe auch  
 [Hinzufügen von Spalten zu einer Tabelle &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [Partitionen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  