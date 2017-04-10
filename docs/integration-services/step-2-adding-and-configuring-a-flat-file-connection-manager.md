---
title: "Schritt 2: Hinzuf&#252;gen und Konfigurieren eines Verbindungs-Managers f&#252;r Flatfiles | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 9a77dd32-d8c2-4961-ad37-2a971f9d6043
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Schritt 2: Hinzuf&#252;gen und Konfigurieren eines Verbindungs-Managers f&#252;r Flatfiles
In dieser Aufgabe fügen Sie einen Verbindungs-Manager für Flatfiles zum von Ihnen erstellten Paket hinzu. Mithilfe eines Verbindungs-Managers für Flatfiles können von einem Paket Daten aus einer Flatfile extrahiert werden. Mithilfe des Verbindungs-Managers für Flatfiles können Sie den Namen und Speicherort der Datei, die Gebietsschema- und Codepage sowie das Dateiformat einschließlich der Spaltentrennzeichen angeben, die angewendet werden sollen, wenn vom Paket Daten aus der Flatfile extrahiert werden. Zusätzlich können Sie die Datentypen für einzelne Spalten manuell angeben oder das Dialogfeld **Spaltentypen vorschlagen** verwenden, um die Spalten extrahierter Daten automatisch [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Datentypen zuzuordnen.  
  
Sie müssen einen neuen Verbindungs-Manager für Flatfiles für jedes Dateiformat erstellen, mit dem Sie arbeiten. Weil in diesem Lernprogramm Daten aus mehreren Flatfiles mit genau dem gleichen Datenformat extrahiert werden, müssen Sie für Ihr Paket nur einen Verbindungs-Manager für Flatfiles hinzufügen und konfigurieren.  
  
Für dieses Lernprogramm konfigurieren Sie die folgenden Eigenschaften in Ihrem Verbindungs-Manager für Flatfiles:  
  
-   **Spaltennamen:** Weil die Flatfile keine Spaltennamen aufweist, werden vom Verbindungs-Manager für Flatfiles Standardspaltennamen erstellt. Diese Standardnamen sind nicht sinnvoll, wenn der Zweck jeder Spalte identifiziert werden soll. Damit diese Standardnamen nützlicher werden, müssen Sie die Standardnamen so ändern, dass sie mit der Faktentabelle übereinstimmen, in die die Flatfiledaten geladen werden.  
  
-   **Datenzuordnungen:** Die Datentypenzuordnungen, die Sie für den Verbindungs-Manager für Flatfiles angeben, werden von allen Flatfile-Datenquellenkomponenten verwendet, die auf den Verbindungs-Manager verweisen. Sie können diese Datentypen entweder mithilfe des Verbindungs-Managers für Flatfiles manuell zuordnen oder das Dialogfeld **Spaltentypen vorschlagen** verwenden. In diesem Tutorial werden die vorgeschlagenen Zuordnungen im Dialogfeld **Spaltentypen vorschlagen** angezeigt. Sie nehmen dann manuell die erforderlichen Zuordnungen im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** vor.  
  
Der Verbindungs-Manager für Flatfiles stellt Gebietsschemainformationen zur Datendatei bereit. Wenn Ihr Computer nicht zur Verwendung der regionalen Einstellung Englisch (USA) konfiguriert ist, müssen Sie zusätzliche Eigenschaften im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** festlegen.  
  
### So fügen Sie einen Flatfile-Verbindungs-Manager zum SSIS-Paket hinzu  
  
1.  Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle im **Verbindungs-Manager**-Bereich und anschließend auf **Neue Flatfile-Verbindung**.  
  
2.  Geben Sie im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** für **Name des Verbindungs-Managers** den Namen **Sample Flat File Source Data** ein.  
  
3.  Klicken Sie auf **Durchsuchen**.  
  
4.  Suchen Sie im Dialogfeld **Öffnen** die Datei SampleCurrencyData.txt auf Ihrem Computer.  
  
    Die Beispieldaten sind in den [!INCLUDE[ssIS](../includes/ssis-md.md)]-Lektionspaketen enthalten. Um die Beispieldaten und die Lektionspakete herunterzuladen, gehen Sie wie folgt vor.  
  
    1.  Klicken Sie [hier](http://go.microsoft.com/fwlink/?LinkId=275027), um zur Seite Integration Services Product Samples zu gelangen  
  
    2.  Klicken Sie auf die Registerkarte **DOWNLOADS**.  
  
    3.  Klicken Sie auf die Datei „SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip“.  
  
5.  Löschen Sie die Spaltennamen im ersten Datenzeilen-Kontrollkästchen.  
  
### So legen Sie gebietsschemabezogene Eigenschaften fest  
  
1.  Klicken Sie im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** auf **Allgemein**.  
  
2.  Legen Sie **Gebietsschema** auf Englisch (USA) und **Codepage** auf 1252 fest.  
  
### So benennen Sie Spalten im Verbindungs-Manager für Flatfiles um  
  
1.  Klicken Sie im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** auf **Erweitert**.  
  
2.  Nehmen Sie im Eigenschaftenbereich die folgenden Änderungen vor:  
  
    -   Ändern Sie die **Column 0**-Nameneigenschaft in **AverageRate**.  
  
    -   Ändern Sie die **Column 1**-Nameneigenschaft in **CurrencyID**.  
  
    -   Ändern Sie die **Column 2**-Nameneigenschaft in **CurrencyDate**.  
  
    -   Ändern Sie die **Column 3**-Nameneigenschaft in **EndOfDayRate**.  
  
    > [!NOTE]  
    > Standardmäßig sind alle vier Spalten auf einen Zeichenfolgendatentyp [DT_STR] mit einer **OutputColumnWidth** von 50 festgelegt.  
  
### So ordnen Sie Spaltendatentypen neu zu  
  
1.  Klicken Sie im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** auf **Typen vorschlagen**.  
  
    [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] schlägt automatisch die am besten geeigneten Datentypen auf Basis der ersten 200 Datenzeilen vor. Sie können diese Vorschlagsoptionen auch ändern, um mehr oder weniger Daten auszuwerten, den Standarddatentyp für ganzzahlige oder boolesche Daten anzugeben oder Leerstellen zum Auffüllen von Zeichenfolgenspalten hinzuzufügen.  
  
    Nehmen Sie vorerst keine Änderungen an den Optionen im Dialogfeld **Spaltentypen vorschlagen** vor und klicken Sie auf **OK**, damit von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Datentypen für Spalten vorgeschlagen werden. Anschließend kehren Sie zum Bereich **Erweitert** im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** zurück, in dem Sie die von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] vorgeschlagenen Spaltendatentypen anzeigen können. (Wenn Sie auf **Abbrechen** klicken, werden keine Vorschläge zu Spaltenmetadaten gemacht und wird der Standardtyp für Zeichenfolgendaten (DT_STR) verwendet.)  
  
    In diesem Lernprogramm werden von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] die Datentypen vorgeschlagen, die in der zweiten Spalte der folgenden Tabelle für die Daten aus der Datei SampleCurrencyData.txt angezeigt werden. Die für die Spalten im Ziel erforderlichen Datentypen, die in einem späteren Schritt definiert werden, werden allerdings in der letzten Spalte der folgenden Tabelle angezeigt.  
  
    |Flatfilespalte|Vorgeschlagener Typ|Zielspalte|Zieltyp|  
    |--------------------|------------------|----------------------|--------------------|  
    |AverageRate|float [DT_R4]|FactCurrency.AverageRate|float|  
    |CurrencyID|string [DT_STR]|DimCurrency.CurrencyAlternateKey|nchar(3)|  
    |CurrencyDate|date [DT_DATE]|DimDate.FullDateAlternateKey|Datum|  
    |EndOfDayRate|float [DT_R4]|FactCurrency.EndOfDayRate|float|  
  
    Der für die Spalte **CurrencyID** vorgeschlagene Datentyp ist inkompatibel mit dem Datentyp des Felds in der Zieltabelle. Weil `DimCurrency.CurrencyAlternateKey` den Datentyp nchar (3) hat, muss **CurrencyID** von string [DT_STR] in string [DT_WSTR] geändert werden. Zusätzlich ist das Feld `DimDate.FullDateAlternateKey` als Date-Datentyp definiert. Deshalb muss **CurrencyDate** von date [DT_Date] in database date [DT_DBDATE] geändert werden.  
  
2.  Wählen Sie aus der Liste die CurrencyID-Spalte. Ändern Sie im Eigenschaftenbereich den Datentyp der Spalte **CurrencyID** von string [DT_STR] in Unicode string [DT_WSTR].  
  
3.  Ändern Sie im Eigenschaftenbereich den Datentyp der Spalte **CurrencyDate** von date [DT_DATE] in database date [DT_DBDATE].  
  
4.  Klicken Sie auf **OK**.  
  
## Nächste Aufgabe in der Lektion  
[Schritt 3: Hinzufügen und Konfigurieren eines OLE DB-Verbindungs-Managers](../integration-services/step-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
## Siehe auch  
[Verbindungs-Manager für Flatfiles](../integration-services/connection-manager/flat-file-connection-manager.md)  
[SQL Server Integration Services-Datentypen](../integration-services/data-flow/integration-services-data-types.md)  
  
  
  
