---
title: "&#220;bersetzungen in Tabellenmodellen (Analysis Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e67f88f5-9f0c-4f19-ab09-558c56ca9335
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# &#220;bersetzungen in Tabellenmodellen (Analysis Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dient zum Hinzufügen von Unterstützung für Übersetzungszeichenfolgen für Tabellenmodelle, die mit dem Kompatibilitätsgrad 1200 erstellt wurden. Einzelne Objekte im Modell können mehrere Übersetzungen eines Namens oder einer Beschreibung aufweisen, wodurch die Unterstützung von mehrsprachigen Versionen innerhalb der Modelldefinition möglich wird.  
  
 Übersetzte Zeichenfolgen stehen nur für Objektmetadaten (Namen und Beschreibungen von Tabellen und Spalten) zur Verfügung, die in einem Clienttool wie einer Excel PivotTable-Liste angezeigt werden.  Zum Verwenden von übersetzten Listen gibt die Clientverbindung die Kultur an. Im Feature **In Excel analysieren** können Sie die Sprache in einer Dropdownliste auswählen. Für andere Tools muss die Kultur möglicherweise in der Verbindungszeichenfolge eingegeben werden.  
  
 Dieses Feature ist nicht dafür vorgesehen, übersetzte Daten in ein Modell zu laden. Wenn Sie übersetzte Datenwerte laden möchten, sollten Sie eine Verarbeitungsstrategie entwickeln, die das Extrahieren übersetzter Zeichenfolgen aus einer Datenquelle beinhaltet, die sie zur Verfügung stellt.  
  
 Ein typischer Workflow für das Hinzufügen übersetzter Metadaten sieht etwa so aus:  
  
-   Generieren einer leeren JSON-Übersetzungsdatei, die Platzhalter für jede Zeichenfolgenübersetzung enthält  
  
-   Hinzufügen von Zeichenfolgenübersetzungen zur JSON-Datei  
  
-   Rückímportieren der Übersetzungen in das Modell  
  
-   Erstellen, Verarbeiten oder Bereitstellen des Modells  
  
-   Herstellen einer Verbindung mit dem Modell mithilfe einer Clientanwendung, die eine LCID für die Verbindungszeichenfolge zulässt  
  
## Erstellen einer leeren Übersetzungsdatei  
 Verwenden Sie [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] zum Hinzufügen von Übersetzungen.  
  
1.  Klicken Sie auf **Modell** > **Übersetzungen** > **Übersetzungen verwalten**.  
  
2.  Wählen Sie die Sprachen aus, für die Sie Übersetzungen zur Verfügung stellen, und klicken Sie dann auf **Hinzufügen**.  
  
3.  Wählen Sie in der Liste eine oder mehrere Sprachen aus, je nachdem, wie Sie die Zeichenfolgen später importieren möchten.  
  
     Die Übersetzungsdatei kann mehrere Sprachen enthalten, die Verwaltung der Übersetzungen gestaltet sich aber möglicherweise einfacher, wenn Sie eine Datei pro Sprache verwenden. Die Übersetzungsdatei, die Sie jetzt erstellen, wird später im Ganzen importiert. Wenn je nach Sprache verschiedene Importoptionen realisiert werden sollen, muss jede Sprache in einer eigenen Datei vorliegen.  
  
4.  Klicken Sie auf **Sprachdatei exportieren**.  Geben Sie einen Dateinamen und einen Speicherort an.  
  
 ![ssas-tabular-translate-export](../../analysis-services/tabular-models/media/ssas-tabular-translate-export.png "ssas-tabular-translate-export")  
  
## Hinzufügen von Übersetzungen  
 Eine leere JSON-Übersetzungsdatei enthält Metadaten für Übersetzungen in einer bestimmten Sprache. Übersetzungsplatzhalter für Objektnamen und Beschreibungen sind im Abschnitt **Culture** am Ende der Modelldefinition angegeben. Übersetzungen können für folgende Elemente hinzugefügt werden:  
  
|||  
|-|-|  
|translatedCaption|Tabellen- oder Spaltentitel, der in beliebigen Clientanwendungen angezeigt wird, die Visualisierungen eines Tabellenmodells unterstützen.|  
|translatedDescription|Weniger gebräuchlich als Titel, wird eine Beschreibung als Modellinformation in einem Modellierungstool wie SSDT angezeigt.|  
  
 Löschen Sie keine Metadaten ohne Angaben aus der Datei.  Sie sollte mit der Datei übereinstimmen, auf der sie basiert. Fügen Sie einfach die gewünschten Zeichenfolgen hinzu, und speichern Sie dann die Datei.  
  
 Auch wenn er wie ein zu bearbeitender Teil aussieht, enthält der Abschnitt **referenceCulture** die Metadaten in der Standardkultur des Modells. Änderungen, die Sie am Abschnitt **referenceCulture** vornehmen, werden beim Importieren nicht gelesen und entsprechend ignoriert.  
  
 Das folgende Beispiel zeigt übersetzte Titel und Beschreibungen für die Tabellen **DimProduct** und **DimCustomer**.  
  
 ![ssas-tabular-translate-json](../../analysis-services/tabular-models/media/ssas-tabular-translate-json.png "ssas-tabular-translate-json")  
  
> [!TIP]  
>  Zum Öffnen der Datei kann ein beliebiger JSON-Editor verwendet werden, wir empfehlen jedoch, den JSON-Editor in Visual Studio zu verwenden, damit Ihnen auch der Befehl „Code anzeigen“ im Projektmappen-Explorer zum Anzeigen der Tabellenmodelldefinition in SSDT zur Verfügung steht. Den JSON-Editor erhalten Sie als Teil einer [installierten Vollversion von Visual Studio 2015](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx). Die kostenlose Community-Edition enthält den JSON-Editor.  
  
## Importieren einer Übersetzungsdatei  
 Importierte Übersetzungszeichenfolgen werden zu einem dauerhaften Bestandteil der Modelldefinition. Nach dem Importieren der Zeichenfolgen wird nicht mehr auf die Übersetzungsdatei verwiesen.  
  
1.  Klicken Sie auf **Modell** > **Übersetzungen** > **Übersetzungen importieren**.  
  
2.  Suchen Sie die Übersetzungsdatei, und klicken Sie dann auf **Öffnen**.  
  
3.  Geben Sie optional Importoptionen an.  
  
    |||  
    |-|-|  
    |Vorhandene Übersetzungen überschreiben|Ersetzt alle vorhandenen Titel oder Beschreibungen der gleichen Sprache beim Importieren der Datei.|  
    |Ungültige Objekte ignorieren|Gibt an, ob Abweichungen in den Metadaten ignoriert oder als Fehler gekennzeichnet werden sollen.|  
    |Importergebnisse in eine Protokolldatei schreiben|Protokolldateien werden standardmäßig im Projektordner gespeichert. Der genaue Pfad für die Datei wird nach dem Abschluss des Imports bereitgestellt. Der Name der Protokolldatei lautet „SSDT_Translations_Log_\<Zeitstempel>“.|  
    |Übersetzungen vor dem Importieren in einer JSON-Datei sichern|Sichert eine vorhandene Übersetzung, deren Kultur mit der der importierten Zeichenfolgen übereinstimmt.  Wenn die importierte Kultur im Modell nicht vorhanden ist, ist die Sicherung leer.<br /><br /> Wenn Sie diese Datei zu einem späteren Zeitpunkt wiederherstellen müssen, können Sie den Inhalt von „model.bim“ durch diese JSON-Datei ersetzen.|  
  
4.  Klicken Sie auf **Importieren**.  
  
5.  Wenn Sie eine Protokolldatei oder eine Sicherung erstellt haben, finden Sie die Dateien optional im Projektordner (z. B. „C:\Users\Documents\Visual Studio 2015\Projects\Tabular1200-AW\Tabular1200-AW“).  
  
6.  Um den Import zu überprüfen, gehen Sie folgendermaßen vor:  
  
    -   Klicken Sie mit der rechten Maustaste im Projektmappen-Explorer auf die Datei **model.bim**, und wählen Sie **Code anzeigen** aus. Klicken Sie auf **Ja**, um die Entwurfsansicht zu schließen, und öffnen Sie **model.bim** erneut in der Codeansicht.  Wenn Sie eine Vollversion von Visual Studio, z. B. die kostenlose Community Edition, installiert haben, wird die Datei im integrierten JSON-Editor geöffnet.  
  
    -   Suchen Sie nach **Culture** oder einer bestimmten übersetzten Zeichenfolge, um zu überprüfen, ob die erwarteten Zeichenfolgen, tatsächlich vorhanden sind.  
  
## Stellen Sie eine Verbindung unter Verwendung eines Gebietsschemabezeichners her  
 Dieser Abschnitt beschreibt eine Möglichkeit, zu prüfen, ob die richtigen Zeichenfolgen vom Modell zurückgegeben werden.  
  
1.  Stellen Sie in Excel eine Verbindung mit dem Tabellenmodell her. Bei diesem Schritt wird angenommen, dass das Modell bereitgestellt wurde. Wenn das Modell nur im Arbeitsbereich vorhanden ist, stellen Sie es in der Analysis Services-Instanz bereit, um die Gültigkeitsprüfung abzuschließen.  
  
     Alternativ können Sie für die Verbindung mit dem Modell die Funktion **In Excel analysieren** verwenden.  
  
2.  Wählen Sie im Excel-Verbindungsdialogfeld die Kultur aus, für die Zeichenfolgenübersetzungen in Ihrem Modell vorhanden sind. Excel erkennt die im Modell definierten Kulturen und füllt die Dropdownliste entsprechend auf.  
  
     ![ssas-tabular-translations-excel](../../analysis-services/tabular-models/media/ssas-tabular-translations-excel.png "ssas-tabular-translations-excel")  
  
     Wenn Sie eine PivotTable erstellen, sollten die übersetzten Tabellen- und Spaltennamen angezeigt werden.  
  
## Siehe auch  
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Globalisierungsszenarien für Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Analysieren in Excel &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  