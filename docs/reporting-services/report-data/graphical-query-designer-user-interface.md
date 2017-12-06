---
title: "Grafische Benutzeroberfläche des Abfrage-Designers | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10012"
- sql13.rtp.rptdesigner.dataview.vdtquerydesigner.f1
helpviewer_keywords:
- graphical query designer [Reporting Services]
- data sources [Reporting Services], creating
- text-based query designer [Reporting Services]
- query designers [Reporting Services]
- Reporting Services, query designers
ms.assetid: 5022ae33-03a3-48de-8ac1-82742f48cebe
caps.latest.revision: "54"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 27cbba801cfa54e30dc69534f6835b3c2d381dfc
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="graphical-query-designer-user-interface"></a>Grafische Benutzeroberfläche des Abfrage-Designers
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] bietet einen grafischen Abfrage-Designer und einen textbasierten Abfrage-Designer zum Erstellen von Abfragen, um Daten aus einer relationalen Datenbank für ein Berichtsdataset im Berichts-Designer abzurufen. Verwenden Sie den grafischen Abfrage-Designer zum interaktiven Erstellen einer Abfrage sowie zum Anzeigen der Datenquellentypen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, OLE DB und ODBC. Verwenden Sie den textbasierten Abfrage-Designer, um mehrere [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, komplexe Abfragen oder Befehlssyntax und ausdrucksbasierte Abfragen anzugeben. Weitere Informationen finden Sie unter [Benutzeroberfläche des textbasierten Abfrage-Designers](http://msdn.microsoft.com/library/44b7c664-03aa-494e-a484-052b318e810c). Weitere Informationen zum Arbeiten mit bestimmten Datenquellentypen finden Sie unter [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md).  
  
 .  
  
## <a name="graphical-query-designer"></a>Grafischer Abfrage-Designer  
 Der grafische Abfrage-Designer unterstützt drei Typen von Abfragebefehlen: **Text**, **StoredProcedure**oder **TableDirect**. Bevor Sie eine Abfrage für Ihr Dataset erstellen, müssen Sie eine Befehlstypoption auf der Seite Abfrage im Dialogfeld [Dataseteigenschaften](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f) auswählen.  
  
 Die folgenden Optionen sind als Abfragetyp verfügbar:  
  
-   **Text** Unterstützt standardmäßigen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragetext für relationale Datenquellen, einschließlich der Datenverarbeitungserweiterungen für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und Oracle.  
  
-   **TableDirect** Wählt alle Spalten aus der angegebenen Tabelle aus. Zum Beispiel ist dies für eine Tabelle mit dem Namen Kunden die Entsprechung der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung `SELECT * FROM Customers`.  
  
-   **StoredProcedure** Unterstützt Aufrufe gespeicherter Prozeduren für die Datenquelle. Wenn Sie diese Option verwenden möchten, benötigen Sie vom Datenbankadministrator Ausführungsberechtigungen für die gespeicherte Prozedur der Datenquelle.  
  
 Der Standardbefehlstyp ist **Text**.  
  
> [!NOTE]  
>  Nicht alle Typen werden von allen Datenverarbeitungserweiterungen unterstützt. Der zugrunde liegende Datenanbieter muss einen Befehlstyp unterstützen, bevor die Option verfügbar ist.  
  
### <a name="command-type-text"></a>Befehlstyp "Text"  
 Für den **Text** -Befehlstyp stellt der grafische Abfrage-Designer vier Bereiche dar. Sie können Spalten, Aliasnamen, Sortierungswerte und Filterwerte für eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage angeben. Sie können den anhand Ihrer Auswahl generierten Abfragetext anzeigen, die Abfrage ausführen und das Resultset anzeigen. In der folgenden Abbildung sind die vier Bereiche dargestellt.  
  
 ![Graphischer Abfrage-Designer für SQL-Abfrage](../../reporting-services/report-data/media/rsqd-dsaw-sql.gif "Graphical query designer for sql query")  
  
 Die folgende Tabelle beschreibt die Funktion jedes Bereichs.  
  
|Bereich|Funktion|  
|----------|--------------|  
|Diagramm|Zeigt grafische Darstellungen der Tabellen in der Abfrage an. In diesem Bereich können Sie Felder auswählen und Beziehungen zwischen Tabellen definieren.|  
|Raster|Zeigt eine Liste der von der Abfrage zurückgegebenen Felder an. In diesem Bereich definieren Sie Aliase, die Sortierreihenfolge, Filter, Gruppen und Parameter.|  
|SQL|Zeigt die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage an, die im Diagrammbereich und im Rasterbereich dargestellt ist. In diesem Bereich schreiben oder aktualisieren Sie eine Abfrage mit [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|Ergebnis|Zeigt die Ergebnisse der Abfrage an. Wenn Sie die Abfrage ausführen möchten, klicken Sie mit der rechten Maustaste in einen beliebigen Bereich und anschließend auf **Ausführen**, oder klicken Sie auf der Symbolleiste auf die Schaltfläche **Ausführen** .|  
  
 Wenn Sie die Informationen in einem der ersten drei Bereiche ändern, werden diese Änderungen in den anderen Bereichen angezeigt. Beispielsweise wird eine von Ihnen im Diagrammbereich hinzugefügte Tabelle automatisch auch der [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage im SQL-Bereich hinzugefügt. Ein Feld, das zur Abfrage im SQL-Bereich hinzugefügt wird, wird automatisch zur Liste im Rasterbereich hinzugefügt. Die Tabelle im Diagrammbereich wird entsprechend aktualisiert.  
  
 Weitere Informationen finden Sie unter [Tools im Abfrage- und Sicht-Designer (Visual Database Tools)](http://msdn.microsoft.com/library/12e4b5a5-b793-4b6c-a0e5-c450c49bf26f).  
  
#### <a name="toolbar-for-the-graphical-query-designer"></a>Symbolleiste des grafischen Abfrage-Designers  
 Die Symbolleiste des grafischen Abfrage-Designers stellt Schaltflächen bereit, mit denen Sie [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen mithilfe der grafischen Benutzeroberfläche entwerfen können.  
  
|Schaltfläche|Description|  
|------------|-----------------|  
|**Als Text bearbeiten**|Wechseln zwischen dem textbasierten Abfrage-Designer und dem grafischen Abfrage-Designer.|  
|**Importieren**|Importiert eine vorhandene Abfrage aus einer Datei oder einem Bericht. Nur die Dateitypen SQL und RDL werden unterstützt. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Diagrammbereich ein-/ausblenden (Umschaltfläche)](../../reporting-services/report-data/media/rsqdicon-showhidediagram.gif "Show/Hide diagram pane toggle button")|Ein- und Ausblenden des Diagrammbereichs.|  
|![Rasterbereich ein-/ausblenden (Umschaltfläche)](../../reporting-services/report-data/media/rsqdicon-showhidegrid.gif "Show or Hide Grid pane toggle")|Ein- und Ausblenden des Rasterbereichs.|  
|![SQL-Bereich ein-/ausblenden (Umschaltfläche)](../../reporting-services/report-data/media/rsqdicon-showhidesql.gif "Show or Hide Grid pane toggle")|Ein- und Ausblenden des SQL-Bereichs.|  
|![Ergebnisbereich ein-/ausblenden (Umschaltfläche)](../../reporting-services/report-data/media/rsqdicon-showhideresult.gif "Show or Hide Grid pane toggle")|Ein- und Ausblenden des Ergebnisbereichs.|  
|![Führen Sie die Abfrage aus](../../reporting-services/report-data/media/rsqdicon-run.gif "Run the query")|Führen Sie die Abfrage aus.|  
|![Überprüfen von SQL im SQL-Bereich (Schaltfläche)](../../reporting-services/report-data/media/rsqdicon-verifysql.gif "Verify SQL in SQL pane button")|Überprüfen, ob die Syntax des Abfragetexts richtig ist.|  
|![Festlegen des aufsteigenden Sortierens für das ausgewählte Feld](../../reporting-services/report-data/media/rsqdicon-sortascending.gif "Set Sort Ascending on selected field")|Festlegen der Sortierreihenfolge auf **Aufsteigend sortieren** für die ausgewählte Spalte im Diagrammbereich.|  
|![Festlegen des absteigenden Sortierens für das ausgewählte Feld](../../reporting-services/report-data/media/rsqdicon-sortdescending.gif "Set Sort Ascending on selected field")|Festlegen der Sortierreihenfolge auf **Absteigend sortieren** für die ausgewählte Spalte im Diagrammbereich.|  
|![Entfernen des Filters auf dem ausgewählten Feld](../../reporting-services/report-data/media/rsqdicon-removefilter.gif "Remove filter on selected field")|Entfernen Sie den Filter für die ausgewählte Spalte im Diagrammbereich, für den angegeben ist, dass er einen Filter hat (![Filtergraphik neben der ausgewählten Filterspalte](../../reporting-services/report-data/media/rsqdicon-filter.gif "Filter graphic next to selected filter column")).|  
|![Verwenden von „Gruppieren nach“ für das ausgewählte Feld](../../reporting-services/report-data/media/rsqdicon-usegroupby.gif "Use Group By for the selected field")|Ein- und Ausblenden der **Gruppieren nach** -Spalte im Rasterbereich. Wenn die Umschaltfläche **Gruppieren nach** aktiviert ist, wird eine zusätzliche Spalte namens **Gruppieren nach** im Rasterbereich angezeigt, und für jeden Wert der ausgewählten Spalten in der Abfrage wird standardmäßig **Gruppieren nach**verwendet, sodass die ausgewählte Spalte in eine GROUP BY-Klausel im SQL-Text aufgenommen wird. Verwenden Sie die Schaltfläche Gruppieren nach, um automatisch eine GROUP BY-Klausel hinzuzufügen, die alle Spalten in der SELECT-Klausel enthält. Schließen Sie jede Nicht-Aggregatspalte in die GROUP BY-Klausel ein, wenn die SELECT-Klausel Aggregatfunktionsaufrufe (beispielsweise SUM(ColumnName)) enthält und im Resultset angezeigt werden soll.<br /><br /> Für die Anzeige im Ergebnisbereich muss für jede Spalte in der Abfrage eine Aggregatfunktion für die Verwendung beim Berechnen des im Ergebnisbereich anzuzeigenden Werts definiert sein, oder die Spalte in der Abfrage muss in der GROUP BY-Klausel der SQL-Abfrage angegeben sein.|  
|![Hinzufügen einer Tabelle zum Diagrammbereich](../../reporting-services/report-data/media/rsqdicon-addtable.gif "Add a new table to the diagram pane")|Hinzufügen einer neuen Tabelle aus der Datenquelle zum Diagrammbereich.<br /><br /> **Hinweis** Wenn Sie eine neue Tabelle hinzufügen, versucht der Abfrage-Designer, Fremdschlüsselbeziehungen aus der Datenquelle zuzuordnen. Bestätigen Sie nach dem Hinzufügen einer Tabelle, dass die durch Verknüpfungen zwischen den Tabellen dargestellten Fremdschlüsselbeziehungen richtig sind.|  
  
#### <a name="example"></a>Beispiel  
 Die folgende Abfrage gibt die Liste der Nachnamen aus der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Personen **-Tabelle der** -Datenbank zurück:  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 Sie können auch gespeicherte Prozeduren aus dem SQL-Bereich ausführen. Die folgende Abfrage führt die gespeicherte Prozedur **uspGetEmployeeManagers** in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank aus:  
  
```  
EXEC uspGetEmployeeManagers '1';  
```  
  
### <a name="command-type-tabledirect"></a>TableDirect-Befehlstyp  
 Für den **TableDirect** -Befehlstyp zeigt der grafische Abfrage-Designer eine Dropdownliste der verfügbaren Tabellen aus der Datenquelle und einen Ergebnisbereich an. Wenn Sie eine Tabelle auswählen und auf die Schaltfläche **Ausführen** klicken, werden alle Spalten für diese Tabelle zurückgegeben.  
  
> [!NOTE]  
>  Die TableDirect-Funktion wird nur von den Datenquellentypen **OLE DB** und **ODBC** unterstützt.  
  
 Die folgende Tabelle beschreibt die Funktion jedes Bereichs.  
  
|Bereich|Funktion|  
|----------|--------------|  
|Dropdownliste der Tabellen|Listet alle verfügbaren Tabellen aus der Datenquelle auf. Wählen Sie eine gespeicherte Prozedur aus der Liste aus, um sie zu aktivieren.|  
|Ergebnis|Zeigt alle Spalten aus der ausgewählten Tabelle an. Klicken Sie zum Ausführen der Tabellenabfrage auf die Schaltfläche **Ausführen** auf der Symbolleiste.|  
  
#### <a name="toolbar-buttons-for-the-command-type-tabledirect"></a>Schaltflächen der Symbolleiste für den TableDirect-Befehlstyp  
 Die Symbolleiste des grafischen Abfrage-Designers stellt eine Dropdownliste mit Tabellen der Datenquelle bereit. In der folgenden Tabelle wird jede Schaltfläche und ihre Funktion aufgelistet.  
  
|Schaltfläche|Description|  
|------------|-----------------|  
|**Als Text bearbeiten**|Wechseln zwischen dem textbasierten Abfrage-Designer und dem grafischen Abfrage-Designer.|  
|**Importieren**|Importiert eine vorhandene Abfrage aus einer Datei oder einem Bericht. Nur die Dateitypen SQL und RDL werden unterstützt. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Symbol der Schaltfläche Standardabfrage-Designer](../../reporting-services/report-data/media/icongenericquerydesigner.gif "Icon of the Generic Query Designer button")|Wechseln zwischen dem standardmäßigen Abfrage-Designer und dem grafischen Abfrage-Designer, wobei die Ansicht des Abfragetexts oder der gespeicherten Prozedur beibehalten wird.|  
|![Führen Sie die Abfrage aus](../../reporting-services/report-data/media/rsqdicon-run.gif "Run the query")|Auswählen aller Spalten aus der ausgewählten Tabelle.|  
  
### <a name="command-type-storedprocedure"></a>StoredProcedure-Befehlstyp  
 Für den **StoredProcedure** -Befehlstyp zeigt der grafische Abfrage-Designer eine Dropdownliste der verfügbaren gespeicherten Prozeduren aus der Datenquelle und einen Ergebnisbereich an. Die folgende Tabelle beschreibt die Funktion jedes Bereichs.  
  
|Bereich|Funktion|  
|----------|--------------|  
|Dropdownliste der gespeicherten Prozeduren|Listet alle verfügbaren gespeicherten Prozeduren aus der Datenquelle auf. Wählen Sie eine gespeicherte Prozedur aus der Liste aus, um sie zu aktivieren.|  
|Ergebnis|Zeigt das Ergebnis der Ausführung der gespeicherten Prozedur an. Klicken Sie zum Ausführen der ausgewählten gespeicherten Prozedur auf die Schaltfläche **Ausführen** auf der Symbolleiste.|  
  
#### <a name="toolbar-buttons-for-command-type-storedprocedure"></a>Schaltflächen der Symbolleiste für den StoredProcedure-Befehlstyp  
 Die Symbolleiste des grafischen Abfrage-Designers stellt eine Dropdownliste mit gespeicherten Prozeduren der Datenquelle bereit. In der folgenden Tabelle wird jede Schaltfläche und ihre Funktion aufgelistet.  
  
|Schaltfläche|Description|  
|------------|-----------------|  
|**Als Text bearbeiten**|Wechseln zwischen dem textbasierten Abfrage-Designer und dem grafischen Abfrage-Designer.|  
|**Importieren**|Importiert eine vorhandene Abfrage aus einer Datei oder einem Bericht. Nur die Dateitypen SQL und RDL werden unterstützt. Weitere Informationen finden Sie unter [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Führen Sie die Abfrage aus](../../reporting-services/report-data/media/rsqdicon-run.gif "Run the query")|Ausführen der ausgewählten gespeicherten Prozedur.|  
|Dropdownliste der gespeicherten Prozeduren|Klicken Sie auf den Pfeil nach unten, um eine Liste verfügbarer gespeicherter Prozeduren aus der Datenquelle anzuzeigen. Klicken Sie auf eine gespeicherte Prozedur aus der Liste, um sie auszuwählen.|  
  
#### <a name="example"></a>Beispiel  
 Die folgende gespeicherte Prozedur ruft eine Befehlskettenliste von Vorgesetzten aus der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank auf. Diese gespeicherte Prozedur akzeptiert *BusinessEntityID* als Parameter. Sie können jede kleine ganze Zahl eingeben.  
  
 `uspGetEmployeeManagers '1';`  
  
## <a name="see-also"></a>Siehe auch  
 [Abfrageentwurfstools &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [SQL Server-Verbindungstyp &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)   
 [OLE DB-Verbindungstyp (SSRS)](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)   
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Oracle-Verbindungstyp (SSRS)](../../reporting-services/report-data/oracle-connection-type-ssrs.md)   
 [RSReportDesigner-Konfigurationsdatei](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/200903f4-1208-4563-9dca-26aabaacfa20)  
  
  
