---
title: 'Analysis Services Tutorial Lektion 2: Abrufen von Daten | Microsoft Docs'
description: Beschreibt das Abrufen und Importieren von Daten in der Analysis Services Tutorial-Projekt.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: 1fd06f563581d42764b5b6f29b3c22d8129f9160
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="get-data"></a>Abrufen von Daten

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion verwenden Sie **Daten abrufen** zur Verbindung mit der AdventureWorksDW-Beispieldatenbank Daten, Vorschau und Filter auswählen, und klicken Sie dann in den Modellarbeitsbereich zu importieren.  
  
Verwenden Sie Daten abrufen, können Sie Daten aus einer Vielzahl von Quellen importieren. Daten können auch abgefragt werden mit einer Formel Power Query-M-Ausdruck oder eine [systemeigene SQL-Abfrageausdruck](../tabular-models/ssas-import-query.md).

> [!NOTE]
> Aufgaben und Bilder in diesem Lernprogramm zeigen Herstellen einer Verbindung mit einer AdventureWorksDW2014-Datenbank auf einem lokalen Server. In einigen Fällen kann eine AdventureWorksDW-Datenbank in Azure SQL Data Warehouse verschiedene Objekte zeigen; Allerdings sind sie im Grunde identisch.
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **10 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 1: erstellen ein neuen tabellenmodellprojekts](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Erstellen einer Verbindung  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>So erstellen eine Verbindung mit der AdventureWorksDW-Datenbank  
  
1.  In **tabellarische Modell-Explorer**, mit der rechten Maustaste **Datenquellen** > **aus Datenquelle importieren**.  
  
    Dadurch wird **Daten abrufen**, die schrittweise Anleitung zum Herstellen einer Verbindung mit einer Datenquelle. Wenn Sie nicht tabellarische Modell-Explorer in sehen **Projektmappen-Explorer**, doppelklicken Sie auf **Model.bim** auf das Modell im Designer zu öffnen. 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  Abrufen der Daten, klicken Sie auf **Datenbank** > **SQL Server-Datenbank** > **verbinden**.  
  
3.  In der **SQL Server-Datenbank** Dialogfeld im **Server**, geben Sie den Namen des Servers, auf dem Sie die AdventureWorksDW-Datenbank installiert, und klicken Sie dann auf **verbinden**.  

4.  Wenn Sie aufgefordert, Anmeldeinformationen einzugeben, müssen Sie die Anmeldeinformationen angeben, die Analysis Services für die Verbindung mit der Datenquelle, die beim Importieren und Verarbeiten von Daten verwendet. In **Identitätswechselmodus**Option **Konto Identität**, geben Sie dann die Anmeldeinformationen ein, und klicken Sie dann auf **verbinden**. Es wird empfohlen, dass Sie ein Konto verwenden, in denen nicht das Kennwort abläuft.

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > Die Verwendung eines Windows-Benutzerkontos und -Kennworts stellt die sicherste Methode für das Herstellen einer Verbindung mit einer Datenquelle dar.
  
5.  Wählen Sie im Navigator der **AdventureWorksDW** Datenbank, und klicken Sie dann auf **OK**. Dadurch wird die Verbindung mit der Datenbank erstellt. 
  
6.  Im Navigator, aktivieren Sie das Kontrollkästchen für die folgenden Tabellen: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, und **FactInternetSales**.  

    ![as-lesson2-select-tables](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
Nachdem Sie auf "OK" klicken, wird die Abfrage-Editor geöffnet. Im nächsten Abschnitt wählen Sie nur die Daten, die Sie importieren möchten.

  
## <a name="filter-the-table-data"></a>Filtern der Tabellendaten  

Tabellen in der AdventureWorksDW-Beispieldatenbank enthalten Daten, die nicht in Ihrem Modell einzuschließenden erforderlich ist. Nach Möglichkeit, die Sie nicht benötigte Daten zum Speichern von in-Memory-Speicherplatz, die vom Modell verwendeten herausfiltern möchten. Sie filtern einige Spalten aus Tabellen, damit sie nicht importiert werden in die arbeitsbereichsdatenbank oder die Model-Datenbank, nachdem sie bereitgestellt wurde. 
  
#### <a name="to-filter-the-table-data-before-importing"></a>Zum Filtern der Tabellendaten vor dem Import  
  
1.  Wählen Sie im Abfrage-Editor die **DimCustomer** Tabelle. Ein Überblick über die DimCustomer-Tabelle in der Datenquelle (die AdventureWorksDW-Beispieldatenbank) wird angezeigt. 
  
2.  Mehrfachauswahl (Strg + Klick) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, und klicken Sie dann mit der rechten Maustaste, und klicken Sie dann auf **Spalten entfernen**. 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    Da die Werte für diese Spalten nicht relevant für die Analyse von Internetverkäufen sind, müssen die Spalten nicht importiert werden. Entfernen nicht erforderlicher Spalten wird das Modell kleiner und effizienter.  

    > [!TIP]
    > Wenn Sie ein Fehler unterläuft, können Sie von einem Schritt löschen Sichern **ANGEWENDETE Schritte**.   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  Entfernen die folgenden Spalten in jeder Tabelle, um die übrigen Tabellen zu filtern:  
    
    **DimDate**
    
      |Column|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Column|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Column|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Column|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Column|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      Keine Spalten entfernt.
  
## <a name="Import"></a>Import the selected tables and column data  

Nun, dass Sie nicht benötigte Daten herausgefiltert und in der Vorschau angezeigt haben, können Sie die restlichen Daten importieren, berücksichtigt werden sollen. Der Assistent importiert die Tabellendaten zusammen mit allen Beziehungen zwischen Tabellen. Neue Tabellen und Spalten im Modell erstellt werden, und Daten, die Sie herausgefiltert wird nicht importiert werden.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>So importieren Sie ausgewählte Tabellen- und Spaltendaten  
  
1.  Überprüfen Sie Ihre Auswahl. Wenn alles in Ordnung ist, klicken Sie auf **Import**. Das Dialogfeld "Datenverarbeitung" zeigt den Status der Daten, die von der Datenquelle in der arbeitsbereichsdatenbank importiert werden.
  
    ![as-lesson2-success](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  Klicken Sie auf **Schließen**.  

  
## <a name="save-your-model-project"></a>Speichern Sie das Modellprojekt erstellen  

Es ist wichtig, um das Modellprojekt erstellen häufig zu speichern.  
  
#### <a name="to-save-the-model-project"></a>So speichern Sie das Modellprojekt  
  
-   Click **Datei** > **Alle speichern**.  
  
## <a name="whats-next"></a>Wie geht es weiter?

[Lektion 3: Markieren als Datumstabelle](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md).

  
  
