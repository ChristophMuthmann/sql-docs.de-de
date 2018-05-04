---
title: 'Analysis Services Tutorial ergänzenden Lektion: Detailzeilen | Microsoft Docs'
description: Beschreibt, wie ein Detail Zeilen Ausdruck in der Analysis Services-Lernprogramm zu erstellen.
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
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 16388c1753671e9b835325535685e1d9324e9b52
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="supplemental-lesson---detail-rows"></a>Ergänzende Lektion - Detailzeilen

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser ergänzenden Lektion verwenden Sie die DAX-Editor definieren Sie einen benutzerdefinierten Ausdruck des Detail-Zeilen. Ein Detail-Zeilen-Ausdruck ist eine Eigenschaft für ein Measure Endbenutzer Weitere Informationen über die aggregierten Ergebnisse eines Measures bereitstellt. 
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **10 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

In diesem Artikel ergänzende Lektion ist Teil eines Lernprogramms tabellarischer Modelle. Vor dem Ausführen der Aufgaben in dieser ergänzenden Lektion, Sie sollten haben alle vorherigen Lektionen oder über eine abgeschlossene Adventure Works Internet Sales Model Beispielprojekt.  
  
## <a name="whats-the-issue"></a>Was ist das Problem?

Betrachten Sie die Details des Measures InternetTotalSales, bevor Sie ein Detail Zeilen Ausdruck hinzufügen.

1.  Klicken Sie in SSDT, auf die **Modell** Menü > **in Excel analysieren** öffnen Excel und erstellen eine leere PivotTable.
  
2.  In **PivotTable Fields**, Hinzufügen der **InternetTotalSales** Measure aus der Tabelle FactInternetSales **Werte**, **"calendaryear"** aus der DimDate-Tabelle zu **Spalten**, und **EnglishCountryRegionName** auf **Zeilen**. Die PivotTable können Sie nun eine aggregierte Ergebnisse vom Measure InternetTotalSales nach Regionen und Jahr. 

    ![als-Lektion-Detail-Zeilen-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-pivottable.png)

3. Doppelklicken Sie auf ein aggregierter Wert für ein Jahr und einen Regionsnamen, in der PivotTable. Hier doppelgeklickt wird den Wert für Australien und das Jahr 2014. Ein neues Blatt wird geöffnet, die Daten jedoch nicht sinnvoll sind Daten enthält.

    ![als-Lektion-Detail-Zeilen-pivottable](../tutorial-tabular-1400/media/as-lesson-detail-rows-sheet.png)
  
Was ist die hier ist eine Tabelle mit Spalten und Zeilen mit Daten, die auf das aggregierte Ergebnis des Measures InternetTotalSales beitragen. Zu diesem Zweck können Sie ein Detail Zeilen Ausdruck als Eigenschaft des Measures hinzufügen.

## <a name="add-a-detail-rows-expression"></a>Fügen Sie ein Detail Zeilen Ausdruck hinzu

#### <a name="to-create-a-detail-rows-expression"></a>So erstellen Sie ein Detail Zeilen Ausdruck 
  
1. Klicken Sie im measureraster für die FactInternetSales-Tabelle, auf die **InternetTotalSales** Measure. 

2. In **Eigenschaften** > **Detail Zeilen Ausdruck**, klicken Sie auf die Schaltfläche "Editor" der DAX-Editor zu öffnen.

    ![als-Lektion-Detail-Zeilen-ellipse](../tutorial-tabular-1400/media/as-lesson-detail-rows-ellipse.png)

3. Geben Sie in DAX-Editor den folgenden Ausdruck ein:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Dieser Ausdruck gibt den Namen, Spalten, und Measures aus der FactInternetSales-Tabelle und verknüpfte Tabellen werden zurückgegeben, wenn ein Benutzer eine aggregierte Ergebnis in einer PivotTable oder eines Berichts doppelklickt.

4. Löschen Sie in Excel das Blatt, das in Schritt 3 erstellt, und doppelklicken Sie auf ein aggregierter Wert. Dieses Mal öffnet mit einer Detail Zeilen Expression-Eigenschaft für das Measure definiert, ein neues Arbeitsblatt, viel nützlicher Daten enthält.

    ![als-Lektion-Detail-Zeilen-detailsheet](../tutorial-tabular-1400/media/as-lesson-detail-rows-detailsheet.png)

5. Stellen Sie das Modell erneut bereit.

  
## <a name="see-also"></a>Siehe auch  

[SELECTCOLUMNS-Funktion (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)  
[Ergänzende Lektion – Dynamische Sicherheit](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)  
[Ergänzende Lektion – Unregelmäßige Hierarchien](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)  
