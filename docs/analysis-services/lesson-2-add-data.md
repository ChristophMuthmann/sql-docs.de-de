---
title: "Lektion 2: Hinzufügen von Daten | Microsoft Docs"
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: efd2e0c85d8c266050e74d5c363afe33e37c48c1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-2-add-data"></a>Lektion 2: Hinzufügen von Daten
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion verwenden Sie den Tabellenimport-Assistenten in SSDT zum Herstellen einer Verbindung mit der Beispieldatenbank AdventureWorksDW SQL, wählen Sie die Daten in der Vorschau anzeigen und Filtern der Daten und klicken Sie dann in den Modellarbeitsbereich zu importieren.  
  
Mit dem Tabellenimport-Assistenten können Sie Daten aus einer Reihe verschiedener relationaler Quellen importieren: Access, SQL, Oracle, Sybase, Informix, DB2, Teradata usw. Die Schritte zum Importieren von Daten aus jeder dieser relationalen Quellen sind sehr ähnlich und mit dem unten beschriebenen Vorgang vergleichbar. Daten können auch mithilfe einer gespeicherten Prozedur ausgewählt werden. Weitere Informationen zum Importieren von Daten und die verschiedenen Typen von Datenquellen, die Sie aus importieren können, finden Sie unter [Datenquellen](../analysis-services/tabular-models/data-sources-ssas-tabular.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **20 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 1: Erstellen eines neuen Tabellenmodellprojekts](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Erstellen einer Verbindung  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2014-database"></a>So erstellen eine Verbindung mit einer der AdventureWorksDW2014-Datenbank  
  
1.  Im tabellarischen Modell-Explorer mit der Maustaste **Datenquellen** > **aus Datenquelle importieren**.  
  
    Dies startet den Tabellenimport-Assistenten, der Sie durch das Einrichten einer Verbindungs mit einer Datenquelle führt. Wenn das tabellarische Modell-Explorer nicht angezeigt wird, doppelklicken klicken Sie auf **Model.bim** in **Projektmappen-Explorer** auf das Modell im Designer zu öffnen. 
    
    ![als-tabellarische-lesson2-Zeit](../analysis-services/media/as-tabular-lesson2-tme.png) 

    Hinweis: Wenn Sie Ihr Modell mit Kompatibilitätsgrad 1400 erstellen, wird die neue Daten abrufen Benutzeroberfläche anstelle des Tabellenimport-Assistenten angezeigt. Der Dialogfelder des werden geringfügig von den Schritten angezeigt, jedoch Sie vermutlich nachvollziehen können. 
  
2.  Im Tabellen-Assistenten unter **relationalen Datenbanken**, klicken Sie auf **Microsoft SQL Server** > **Weiter**.  
  
3.  Geben Sie auf der Seite **Mit einer Microsoft SQL Server-Datenbank verbinden** in **Anzeigename der Verbindung**Folgendes ein: **Adventure Works-Datenbank aus SQL**.  
  
4.  In **Servernamen**, geben Sie den Namen des Servers, auf dem Sie die AdventureWorksDW-Datenbank installiert.  
  
5.  In der **Datenbankname** Feld **AdventureWorksDW**, und klicken Sie dann auf **Weiter**.  
  
    ![als-tabellarische-lesson2-Tiw-name](../analysis-services/media/as-tabular-lesson2-tiw-name.png)
  
6.  Auf der Seite **Identitätswechselinformationen** müssen Sie die Anmeldeinformationen angeben, mit denen Analysis Services eine Verbindung mit der Datenquelle herstellt, wenn Daten importiert und verarbeitet werden. Überprüfen Sie, ob **Bestimmter Windows-Benutzername und bestimmtes Kennwort** ausgewählt ist, geben Sie in den Feldern **Benutzername** und **Kennwort**Ihre Windows-Anmeldeinformationen ein, und klicken Sie anschließend auf **Weiter**.  
  
    > [!NOTE]  
    > Die Verwendung eines Windows-Benutzerkontos und -Kennworts stellt die sicherste Methode für das Herstellen einer Verbindung mit einer Datenquelle dar. Weitere Informationen finden Sie unter [Identitätswechsel](../analysis-services/tabular-models/impersonation-ssas-tabular.md).  
  
7.  Überprüfen Sie auf der Seite **Auswählen, wie die Daten importiert werden sollen** , ob die Option **Aus einer Liste von Tabellen und Sichten auswählen, um die zu importierenden Daten zu bestimmen** ausgewählt ist. Sie möchten in einer Liste von Tabellen und Sichten eine Auswahl treffen. Klicken Sie daher auf **Weiter** , um eine Liste aller Quelltabellen in der Quelldatenbank anzuzeigen.  
  
8.  Aktivieren Sie auf der Seite **Tabellen und Sichten auswählen** das Kontrollkästchen für die folgenden Tabellen: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**und **FactInternetSales**.  
  
    Klicken Sie**NICHT** auf **Fertig stellen**.  
  
## <a name="FilterData"></a>Filter the table data  
Die DimCustomer-Tabelle, die Sie die-Beispieldatenbank importieren enthält eine Teilmenge der Daten aus der ursprünglichen SQL Server Adventure Works-Datenbank. Sie filtern einige mehr Spalten aus der DimCustomer-Tabelle, die notwendig sind, wenn Sie in das Modell importiert haben. Wenn möglich, sollten Sie Daten herausfiltern, die verwendet wird, um Speicherplatz im Arbeitsspeicher, die vom Modell verwendeten zu speichern.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>So filtern Sie die Tabellendaten vor dem Importieren  
  
1.  Wählen Sie die Zeile für die **DimCustomer** Tabelle, und klicken Sie dann auf **Vorschau & Filter**. Das Fenster **Vorschau der ausgewählten Tabelle** wird geöffnet und enthält alle Spalten in der DimCustomer-Quelltabelle.  
  
2.  Deaktivieren Sie das Kontrollkästchen am Anfang der folgenden Spalten: **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**. 

    ![als-tabellarische-lesson2-Tiw-löschen](../analysis-services/media/as-tabular-lesson2-tiw-clear.png)
  
    Da die Werte für diese Spalten nicht relevant für die Analyse von Internetverkäufen sind, müssen die Spalten nicht importiert werden. Entfernen nicht erforderlicher Spalten wird Ihr Modell kleinerer und effizienterer stellen.  
  
3.  Überprüfen Sie, ob alle anderen Spalten aktiviert sind, und klicken Sie anschließend auf **OK**.  
  
    Die Wörter **Angewendete Filter** werden nun in der Spalte **Filterdetails** in der Zeile **DimCustomer** angezeigt. Wenn Sie auf diesen Link klicken, sehen Sie eine Textbeschreibung der Filter, die Sie soeben angewendet haben.  
    
    ![als-tabellarische-lesson2-angewendete-Filter](../analysis-services/media/as-tabular-lesson2-applied-filters.png)
    
  
4.  Filtern Sie die verbleibenden Tabellen, indem Sie die Kontrollkästchen für die folgenden Spalten in jeder Tabelle deaktivieren:  
    
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
  
      |Column|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Import the selected tables and column data  
Nun, dass Sie nicht benötigte Daten herausgefiltert und in der Vorschau angezeigt haben, können Sie die restlichen Daten importieren, berücksichtigt werden sollen. Der Assistent importiert die Tabellendaten zusammen mit allen Beziehungen zwischen Tabellen. Neue Tabellen und Spalten im Modell erstellt werden, und Daten, die Sie herausgefiltert werden nicht importiert werden.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>So importieren Sie ausgewählte Tabellen- und Spaltendaten  
  
1.  Überprüfen Sie Ihre Auswahl. Wenn alles in Ordnung ist, klicken Sie auf **Fertig stellen**.  
  
    Während des Datenimports zeigt der Assistent an, wie viele Zeilen abgerufen wurden. Wenn alle Daten importiert wurden, wird in einer Meldung angezeigt, dass der Import erfolgreich abgeschlossen wurde.  
    
    ![als tabellarische-lesson2-Erfolg](../analysis-services/media/as-tabular-lesson2-success.png) 
  
    > [!TIP]  
    > Klicken Sie zum Anzeigen der Beziehungen, die automatisch zwischen den importierten Tabellen erstellt wurden, in der Zeile **Datenvorbereitung** auf **Details**. 
  
2.  Klicken Sie auf **Schließen**.  
  
    Der Assistent geschlossen wurde, und der Modell-Designer zeigt jetzt die importierten Tabellen. 
  
## <a name="save-your-model-project"></a>Speichern Sie das Modellprojekt erstellen  
Es ist wichtig, um das Modellprojekt erstellen häufig zu speichern.  
  
#### <a name="to-save-the-model-project"></a>So speichern Sie das Modellprojekt  
  
-   Click **Datei** > **Alle speichern**.  
  
## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 3: Markieren als Datumstabelle](../analysis-services/lesson-3-mark-as-date-table.md).

  
  
