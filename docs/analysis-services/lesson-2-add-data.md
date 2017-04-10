---
title: "Lektion 2: Hinzuf&#252;gen von Daten | Microsoft Docs"
ms.custom: ""
ms.date: "03/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
caps.latest.revision: 33
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 24
---
# Lektion 2: Hinzuf&#252;gen von Daten
In dieser Lektion verwenden Sie den Tabellenimport-Assistenten in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], um eine Verbindung mit der AdventureWorksDW-Datenbank herzustellen, Daten auszuwählen und die Daten zu filtern und sie anschließend in den Modellarbeitsbereich zu importieren.  
  
Mit dem Tabellenimport-Assistenten können Sie Daten aus einer Reihe verschiedener relationaler Quellen importieren: Access, SQL, Oracle, Sybase, Informix, DB2, Teradata usw. Die Schritte zum Importieren von Daten aus jeder dieser relationalen Quellen sind sehr ähnlich und mit dem unten beschriebenen Vorgang vergleichbar. Darüber hinaus können Daten mit einer gespeicherten Prozedur ausgewählt werden.  
  
Weitere Informationen zum Importieren von Daten und den verschiedenen Datenquellentypen, aus denen Importe möglich sind, finden Sie unter [Datenquellen &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/data-sources-ssas-tabular.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **20 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 1: Erstellen eines neuen Tabellenmodellprojekts](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
## Erstellen einer Verbindung  
  
#### So erstellen Sie eine Verbindung mit der AdventureWorksDW2012-Datenbank  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] auf das Menü **Modell** und anschließend auf **Aus Datenquelle importieren**.  
  
    Dadurch wird der Tabellenimport-Assistent gestartet, der Sie durch das Herstellen einer Verbindung mit einer Datenquelle führt. Wenn **Aus Datenquelle importieren** ausgegraut ist, doppelklicken Sie **Solution Explorer** auf **Model.bim**, um das Modell im Designer zu öffnen.  
  
2.  Klicken Sie im **Tabellenimport-Assistenten**unter **Relationale Datenbanken** auf **Microsoft SQL Server** und anschließend auf **Weiter**.  
  
3.  Geben Sie auf der Seite **Mit einer Microsoft SQL Server-Datenbank verbinden** in **Anzeigename der Verbindung** Folgendes ein: **Adventure Works-Datenbank aus SQL**.  
  
4.  Geben Sie in **Servername** den Namen des Servers ein, auf dem Sie die AdventureWorksDW-Datenbank installiert haben.  
  
5.  Klicken Sie im Feld **Datenbankname** auf den NACH-UNTEN-PFEIL, und wählen Sie **AdventureWorksDW** und anschließend **Weiter** aus.  
  
6.  Auf der Seite **Identitätswechselinformationen** müssen Sie die Anmeldeinformationen angeben, mit denen Analysis Services eine Verbindung mit der Datenquelle herstellt, wenn Daten importiert und verarbeitet werden. Überprüfen Sie, ob **Bestimmter Windows-Benutzername und bestimmtes Kennwort** ausgewählt ist, geben Sie in den Feldern **Benutzername** und **Kennwort** Ihre Windows-Anmeldeinformationen ein, und klicken Sie anschließend auf **Weiter**.  
  
    > [!NOTE]  
    > Die Verwendung eines Windows-Benutzerkontos und -Kennworts stellt die sicherste Methode für das Herstellen einer Verbindung mit einer Datenquelle dar. Weitere Informationen finden Sie unter [Identitätswechsel &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/impersonation-ssas-tabular.md).  
  
7.  Überprüfen Sie auf der Seite **Auswählen, wie die Daten importiert werden sollen**, ob die Option **Aus einer Liste von Tabellen und Sichten auswählen, um die zu importierenden Daten zu bestimmen** ausgewählt ist. Sie möchten in einer Liste von Tabellen und Sichten eine Auswahl treffen. Klicken Sie daher auf **Weiter**, um eine Liste aller Quelltabellen in der Quelldatenbank anzuzeigen.  
  
8.  Aktivieren Sie auf der Seite **Tabellen und Sichten auswählen** das Kontrollkästchen für die folgenden Tabellen: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** und **FactInternetSales**.  
  
9. Die Tabellen im Modell sollten leicht verständliche Namen enthalten. Klicken Sie auf die Zelle in der Spalte **Anzeigename** für **DimCustomer**. Benennen Sie die Tabelle um, indem Sie "Dim" aus "DimCustomer" entfernen.  
  
10. Benennen Sie die anderen Tabellen um:  
  
    |Quellname|Anzeigename|  
    |---------------|-----------------|  
    |DimDate|Datum|  
    |DimGeography|Geography|  
    |DimProduct|Product|  
    |DimProductCategory|Product Category|  
    |DimProductSubcategory|Product Subcategory|  
    |FactInternetSales|Internet Sales|  
  
    Klicken Sie **NICHT** auf **Fertig stellen**.  
  
Da Sie jetzt eine Verbindung mit der Datenbank hergestellt, die zu importierenden Tabellen ausgewählt und den Tabellen Anzeigenamen zugewiesen haben, wechseln Sie zum nächsten Abschnitt mit der Überschrift [Filtern der Tabellendaten vor dem Importieren](#FilterData).  
  
## <a name="FilterData"></a>Filtern der Tabellendaten  
Die DimCustomer-Tabelle, die Sie aus der Datenbank importieren, enthält eine Teilmenge der Daten aus der ursprünglichen SQL Server Adventure Works-Datenbank. Sie filtern einige der Spalten aus der DimCustomer-Tabelle, die nicht erforderlich sind. Wenn möglich, möchten Sie nicht verwendete Daten herausfiltern, um vom Modell verwendeten Speicherplatz im Arbeitsspeicher zu sparen.  
  
#### So filtern Sie die Tabellendaten vor dem Importieren  
  
1.  Wählen Sie die Zeile für die Tabelle **Customer** aus, und klicken Sie anschließend auf **Vorschau & Filter**. Das Fenster **Vorschau der ausgewählten Tabelle** wird geöffnet und enthält alle Spalten in der DimCustomer-Quelltabelle.  
  
2.  Deaktivieren Sie das Kontrollkästchen am Anfang der folgenden Spalten:  
  
    |Customer|  
    |------------|  
    |**SpanishEducation**|  
    |**FrenchEducation**|  
    |**SpanishOccupation**|  
    |**FrenchOccupation**|  
  
    Da die Werte für diese Spalten nicht relevant für die Analyse von Internetverkäufen sind, müssen die Spalten nicht importiert werden. Durch Entfernen von nicht benötigten Spalten wird das Modell kleiner.  
  
3.  Überprüfen Sie, ob alle anderen Spalten aktiviert sind, und klicken Sie anschließend auf **OK**.  
  
    Die Wörter **Angewendete Filter** werden nun in der Spalte **Filterdetails** in der Zeile **Customer** angezeigt. Wenn Sie auf diesen Link klicken, sehen Sie eine Textbeschreibung der Filter, die Sie soeben angewendet haben.  
  
4.  Filtern Sie die verbleibenden Tabellen, indem Sie die Kontrollkästchen für die folgenden Spalten in jeder Tabelle deaktivieren:  
  
    |Datum|  
    |--------|  
    |**DateKey**|  
    |**SpanishDayNameOfWeek**|  
    |**FrenchDayNameOfWeek**|  
    |**SpanishMonthName**|  
    |**FrenchMonthName**|  
  
    |Geography|  
    |-------------|  
    |**SpanishCountryRegionName**|  
    |**FrenchCountryRegionName**|  
    |**IpAddressLocator**|  
  
    |Product|  
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
  
    |Produktkategorie|  
    |--------------------|  
    |**SpanishProductCategoryName**|  
    |**FrenchProductCategoryName**|  
  
    |Product Subcategory|  
    |-----------------------|  
    |**SpanishProductSubcategoryName**|  
    |**FrenchProductSubcategoryName**|  
  
    |Internet Sales|  
    |------------------|  
    |**OrderDateKey**|  
    |**DueDateKey**|  
    |**ShipDateKey**|  
  
Nachdem Sie die nicht benötigten Daten in der Vorschau angezeigt und die herausgefiltert haben, können Sie die Daten importieren. Wechseln Sie zum nächsten Abschnitt (**Importieren der ausgewählten Tabellen- und Spaltendaten**).  
  
## <a name="Import"></a>Importieren der ausgewählten Tabellen- und Spaltendaten  
Sie können jetzt die ausgewählten Daten importieren. Der Assistent importiert die Tabellendaten zusammen mit allen Beziehungen zwischen Tabellen. Neue Tabellen und Spalten werden im Modell mit den Anzeigenamen erstellt, die Sie angegeben haben, und gefilterte Daten werden nicht importiert.  
  
#### So importieren Sie ausgewählte Tabellen- und Spaltendaten  
  
1.  Überprüfen Sie Ihre Auswahl. Wenn alles in Ordnung ist, klicken Sie auf **Fertig stellen**.  
  
    Während des Datenimports zeigt der Assistent an, wie viele Zeilen abgerufen wurden. Wenn alle Daten importiert wurden, wird in einer Meldung angezeigt, dass der Import erfolgreich abgeschlossen wurde.  
  
    > [!TIP]  
    > Klicken Sie zum Anzeigen der Beziehungen, die automatisch zwischen den importierten Tabellen erstellt wurden, in der Zeile **Datenvorbereitung** auf **Details**.  
  
2.  Klicken Sie auf **Schließen**.  
  
    Der Assistent wird geschlossen, wohingegen der Modell-Designer angezeigt wird. Jede Tabelle wurde als neue Registerkarte im Modell-Designer hinzugefügt.  
  
## Speichern des Modellprojekts  
Es ist wichtig, das Modellprojekt, häufig zu speichern.  
  
#### So speichern Sie das Modellprojekt  
  
-   Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] auf das Menü **Datei** und anschließend auf **Alle speichern**.  
  
## Nächster Schritt  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 3: Umbenennen von Spalten](../analysis-services/lesson-3-rename-columns.md).  
  
  
  
