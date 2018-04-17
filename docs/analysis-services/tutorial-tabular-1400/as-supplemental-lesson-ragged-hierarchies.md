---
title: 'Analysis Services Tutorial ergänzenden Lektion: unregelmäßige Hierarchien | Microsoft Docs'
description: Beschreibt, wie in der Analysis Services-Lernprogramm unregelmäßige Hierarchien zu beheben.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 224e0661a4f4c25592ad326f3e0ce3980e3602b8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Ergänzende Lektion - unregelmäßige Hierarchien

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser ergänzenden Lektion beheben Sie ein häufig auftretendes Problem beim Pivotieren Hierarchien, die leere Werte (Mitglieder) auf verschiedenen Ebenen enthalten. Beispielsweise muss eine Organisation, in dem einer hochrangigen Führungskraft sowohl Manager als direkt unterstellte Mitarbeiter hat. Oder geografische Hierarchien Country-Region-Stadt, in denen einige Städte übergeordneten Bundesland oder Kanton, z. B. Washington d. c., Vatikanstadt fehlender zusammengesetzt. Bei eine Hierarchie leere als Member enthält, wird es häufig auf verschiedenen oder unregelmäßig, Ebenen.

![As-Lesson-Detail-ragged-hierarchies-Table](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-table.png)

Tabellarische Modelle mit Kompatibilitätsgrad 1400 verfügen über eine zusätzliche **Member ausblenden** -Eigenschaft für Hierarchien. Die **Standard** Einstellung wird vorausgesetzt, es gibt keine leeren Elemente auf jeder Ebene. Die **leere Member ausblenden** Einstellung schließt leere Elemente aus der Hierarchie, wenn einer PivotTable oder eines Berichts hinzugefügt.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **20 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
In diesem Artikel ergänzende Lektion ist Teil eines Lernprogramms tabellarischer Modelle. Vor dem Ausführen der Aufgaben in dieser ergänzenden Lektion, Sie sollten haben alle vorherigen Lektionen oder über eine abgeschlossene Adventure Works Internet Sales Model Beispielprojekt. 

Wenn Sie das Projekt AW Internet Sales als Teil des Lernprogramms erstellt haben, enthält das Modell noch keine Daten oder Hierarchien, die unregelmäßig sind. Um dieser ergänzenden Lektion abzuschließen, müssen Sie zuerst erstellen das Problem, indem einige weiteren Tabellen hinzufügen, erstellen Sie Beziehungen, berechnete Spalten ein Measure und eine neue Organisationshierarchie. Diese vorkommt ca. 15 Minuten. Klicken Sie dann, erhalten Sie in wenigen Minuten zu lösen.  

## <a name="add-tables-and-objects"></a>Hinzufügen von Tabellen und Objekte
  
### <a name="to-add-new-tables-to-your-model"></a>So fügen Sie neue Tabellen mit dem Modell hinzu
  
1.  Im tabellarischen Modell-Explorer, erweitern Sie **Datenquellen**, die Verbindung per Rechtsklick > **neue Importtabellen**.
  
2.  Wählen Sie im Navigator **DimEmployee** und **FactResellerSales**, und klicken Sie dann auf **OK**.

3.  Klicken Sie im Abfrage-Editor auf **importieren**

4.  Erstellen Sie die folgende [Beziehungen](../tutorial-tabular-1400/as-lesson-4-create-relationships.md):

    | Tabelle 1           | Column       | Filterrichtung   | Tabelle 2     | Column      | Active |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Default            | DimDate     | Datum        | ja    |
    | FactResellerSales | DueDate      | Default            | DimDate     | Datum        | Nein     |
    | FactResellerSales | ShipDateKey  | Default            | DimDate     | Datum        | Nein     |
    | FactResellerSales | ProductKey   | Default            | DimProduct  | ProductKey  | ja    |
    | FactResellerSales | EmployeeKey  | Für beide Tabellen | DimEmployee | EmployeeKey | ja    |

5. In der **DimEmployee** Tabelle, erstellen Sie die folgende [berechnete Spalten](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md): 

    **Pfad** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **Vollständiger Name** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],2,1)) 
    ```

    **"Level3"** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],3,1)) 
    ```

    **"Level4"** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],4,1)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],5,1)) 
    ```

6.  In der **DimEmployee** Tabelle, erstellen Sie eine [Hierarchie](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md) mit dem Namen **Organisation**. Fügen Sie die folgenden Spalten in Ordnung: **Level1**, **Level2**, **"Level3"**, **"Level4"**, **Level5**.

7.  In der **FactResellerSales** Tabelle, erstellen Sie die folgende [Measure](../tutorial-tabular-1400/as-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Verwendung [in Excel analysieren](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md) öffnen Sie Excel und erstellen Sie automatisch eine PivotTable.

9.  In **PivotTable Fields**, Hinzufügen der **Organisation** Hierarchie aus der **DimEmployee** Tabelle **Zeilen**, und die **ResellerTotalSales** measure aus der **FactResellerSales** Tabelle **Werte**.

    ![As-Lesson-Detail-ragged-hierarchies-PivotTable](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable.png)

    Wie Sie in der PivotTable sehen können, zeigt die Hierarchie Zeilen, die unregelmäßig sind. Es sind viele Zeilen, wobei leere Elemente angezeigt werden.

## <a name="to-fix-the-ragged-hierarchy-by-setting-the-hide-members-property"></a>Unregelmäßige Hierarchie zu beheben, indem Sie Elemente ausblenden-Eigenschaft festlegen.

1.  In **tabellarische Modell-Explorer**, erweitern Sie **Tabellen** > **DimEmployee** > **Hierarchien** > **Organisation**.

2.  In **Eigenschaften** > **Member ausblenden**Option **leere Member ausblenden**. 

    ![As-Lesson-Detail-ragged-hierarchies-hidemembers](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  Aktualisieren Sie die PivotTable in Excel zurück. 

    ![As-Lesson-Detail-ragged-hierarchies-PivotTable-Refresh](../tutorial-tabular-1400/media/as-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Das sieht doch viel besser aus!

## <a name="see-also"></a>Siehe auch   
[Lektion 9: Erstellen von Hierarchien](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)  
[Ergänzende Lektion - dynamische Sicherheit](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Ergänzende Lektion - Detailzeilen](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)  
