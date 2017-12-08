---
title: Was ist neu in Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
caps.latest.revision: "97"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 5264fa7ed32a1f35136c710da28af09c6ee0fab8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="what39s-new-in-analysis-services"></a>Was ist neu in Analysis Services
SQL Server 2016 Analysis Services umfasst viele neue Verbesserungen, die Leistung zu verbessern, einfacher Lösung erstellen, automatisierte datenbankverwaltung bereitstellen, verbesserte Beziehungen mit bidirektionale kreuzfilterung, parallele Verarbeitung von Partitionen und vieles mehr. Das Herzstück der meisten Verbesserungen in dieser Version ist der neue Kompatibilitätsgrad 1200 für tabellarische Modelldatenbanken.     

## <a name="azure-analysis-services"></a>Azure Analysis Services
Wie auf der SQL PASS-Konferenz 2016 angekündigt, ist Analysis Services nun als Azure-Dienst in der Cloud verfügbar. **Azure Analysis Services** tabellarische Modelle mit dem Kompatibilitätsgrad 1200 oder höher unterstützt. DirectQuery, Partitionen, Sicherheit auf Zeilenebene, Bidirektionale Beziehungen und Übersetzungen werden unterstützt. Um mehr über den Dienst zu erfahren, und ihn kostenlos zu testen, wechseln Sie zu [Azure Analysis Services](http://azure.microsoft.com/services/analysis-services/). 

## <a name="whats-new-in-sql-server-2016-service-pack-1-sp1-analysis-services"></a>Was ist neu in Analysis Services für SQL Server 2016 Service Pack 1 (SP1)

[SQL Server 2016 SP1 herunterladen](http://www.microsoft.com/download/details.aspx?id=54276) 

Analysis Services für SQL Server 2016 Service SP1 bieten verbesserte Leistung und Skalierbarkeit durch NUMA-Unterstützung (Non-Uniform Memory Access) und optimierte Speicherzuweisung auf der Basis von **Intel TBB** (Intel Threading Building Blocks). Diese neue Funktionalität hilft beim Senken der Gesamtbetriebskosten (Total Cost of Ownership, TCO), da mehr Benutzer auf einer geringeren Anzahl leistungsstärkerer Enterprise-Server unterstützt werden. 

Insbesondere bieten Analysis Services für SQL Server 2016 SP1 Verbesserungen in diesen wichtigen Bereichen:

-   **NUMA-Unterstützung** : Zum Erzielen einer besseren NUMA-Unterstützung verwaltet das In-Memory-Modul (VertiPaq) innerhalb von Analysis Services jetzt eine separate Auftragswarteschlange auf jedem NUMA-Knoten. Dadurch wird sichergestellt, dass die Segmentscanaufträge auf dem gleichen Knoten ausgeführt werden, auf dem der Arbeitsspeicher für die Segmentdaten zugewiesen ist. Beachten Sie, dass NUMA-Unterstützung standardmäßig nur auf Systemen mit mindestens vier NUMA-Knoten aktiviert ist. Auf Systemen mit zwei Knoten wiegen die Kosten für den Zugriff auf remote zugewiesenen Speicher im Allgemeinen den Mehraufwand für die Verwaltung der NUMA-Anforderungen nicht auf.
-   **Speicherbelegung** : Analysis Services wurden mithilfe von Intel Threading Building Blocks beschleunigt, einem skalierbaren Allozierungsmodul, das für jeden Kern separate Speicherpools bereitstellt. Mit zunehmender Kernanzahl kann das System nahezu linear skalieren.
-   **Heapfragmentierung** : Das auf Intel TBB basierende skalierbare Allozierungsmodul hilft auch beim Abschwächen von Leistungsproblemen aufgrund von Heapfragmentierung, die für den Windows-Heap nachgewiesen werden konnte.

Leistungs- und Skalierbarkeitstests zeigten erhebliche Zuwächse im Abfragedurchsatz, wenn SQL Server 2016 SP1 Analysis Services auf großen Enterprise Servern mit vielen Knoten ausgeführt wird.


## <a name="whats-new-in-sql-server-2016-analysis-services"></a>Neuigkeiten in SQL Server 2016 Analysis Services

Während die meisten Verbesserungen in dieser Version spezifisch für tabellarische Modelle sind, wurden auch einige Verbesserungen für mehrdimensionale Modelle vorgenommen. Dies betrifft z.B. die Optimierung bei Distinct Count ROLAP für Datenquellen wie DB2 und Oracle, die Unterstützung für die Drillthrough Mehrfachauswahl mit Excel 2016 sowie Excel-Optimierungen.    

#### <a name="get-the-latest-tools"></a>Abrufen der neuesten Tools
Um optimal von alle Erweiterungen in dieser Version nutzen zu können, werden Sie sicher, dass die neuesten Versionen von SSDT und SSMS installiert.    
- [Herunterladen von SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)    
- [SQL Server Management Studio (SSMS) herunterladen](http://msdn.microsoft.com/library/mt238290.aspx)   

Wenn Sie über eine benutzerdefinierte AMO-abhängige Anwendung verfügen, müssen Sie möglicherweise eine aktualisierte Version von AMO installieren. Anweisungen finden Sie unter [Installieren von Analysis Services-Datenanbietern &#40;AMO, ADOMD.NET, MSOLAP&#41;](../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md).    

 #### <a name="technet-virtual-labs-sql-server-2016-analysis-services"></a>TechNet Virtual Labs: SQL Server 2016 Analysis Services
Besser Lernen durch Anwenden? Folgen Sie Schritt für Schritt unter [Virtuelle Übungseinheit zu Neuheiten in SQL Server 2016 Analysis Services](http://vlabs.holsystems.com/vlabs/technet?eng=VLabs&auth=none&src=vlabs&altadd=true&labid=23110&lod=true).
In dieser Übungseinheit erstellen und überwachen Sie erweiterte Ereignisse (xEvents), upgraden ein tabellarisches Projekt auf den Kompatibilitätsgrad 1200, arbeiten mit Visual Studio-Konfigurationen, implementieren neue Berechnungsfunktionen und neue Tabellenbeziehungsfunktionen, konfigurieren Anzeigeordner, verwalten Modellübersetzungen, arbeiten mit der neuen Tabular Model Scripting Language (TMSL) und mit PowerShell und testen die neuen Funktionen des DirectQuery-Modus.

## <a name="modeling"></a>Modellierung    
### <a name="improved-modeling-performance-for-tabular-1200-models"></a>Verbesserte Modellierungsleistung für tabellarische 1200-Modelle    
Für tabellarische 1200-Modelle sind Vorgänge mit Metadaten in SSDT wesentlich schneller als für tabellarische 1100- oder 1103-Modelle. Ein Vergleich auf der gleichen Hardware hat gezeigt, dass die Erstellung einer Beziehung für ein Modell mit SQL Server 2014-Kompatibilitätsgrad (1103) mit 23 Tabellen 3 Sekunden dauert. Dagegen dauert die Erstellung der gleichen Beziehung für ein Modell mit Kompatibilitätsgrad 1200 weniger als eine Sekunde.    
### <a name="project-templates-added-for-tabular-1200-models-in-ssdt"></a>Projektvorlagen wurden für tabellarische 1200-Modelle in SSDT hinzugefügt    
Ab dieser Version benötigen Sie nicht mehr zwei Versionen von SSDT für die Erstellung von relationalen Projekten und BI-Projekten. Mit[SQL Server Data Tools für Visual Studio 2015](http://msdn.microsoft.com/library/mt204009.aspx) werden Projektvorlagen für Analysis Services-Lösungen hinzugefügt, einschließlich **tabellarischer Analysis Services-Projekte** , die zum Erstellen von Modellen mit Kompatibilitätsgrad 1200 verwendet werden. Weitere Analysis Services-Projektvorlagen für mehrdimensionale Lösungen und Data Mining-Lösungen sind ebenfalls enthalten, aber mit der gleichen Funktionsebene (1100 oder 1103) wie in früheren Releases.    
### <a name="display-folders"></a>Anzeigeordner
Anzeigeordner sind jetzt für Tabellenmodelle 1200 verfügbar. Anzeigeordner werden in SQL Server Data Tools definiert und in Clientanwendungen wie Excel oder Power BI Desktop gerendert. Sie können damit eine große Anzahl von Measures in einzelnen Ordnern organisieren und so eine visuelle Hierarchie für eine einfachere Navigation in Feldlisten hinzufügen.
### <a name="bi-directional-cross-filtering"></a>Bidirektionale Kreuzfilterung
Neu in dieser Version ist eine integrierte Methode zum Aktivieren bidirektionaler Kreuzfilter in tabellarischen Modellen, durch die keine Notwendigkeit für manuell erstellte DAX-Umgehungen für die Tabellenbeziehungen übergreifende Weitergabe des Filterkontexts mehr besteht. Filter werden nur automatisch generiert, wenn die Richtung mit einem hohen Grad an Sicherheit bestimmt werden kann. Bei einer Mehrdeutigkeit in Form von mehreren Abfragepfaden über Tabellenbeziehungen wird kein Filter automatisch erstellt. Weitere Informationen finden Sie unter [Bidirektionale Kreuzfilter für tabellarische Modelle in SQL Server 2016 Analysis Services](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) .
 ### <a name="translations"></a>Übersetzungen    
 Sie können jetzt übersetzte Metadaten in einem tabellarischen 1200-Modell speichern. Metadaten im Modell enthalten Felder für **Culture**, übersetzte Beschriftungen und übersetzte Beschreibungen. Verwenden Sie zum Hinzufügen von Übersetzungen den Befehl **Modell** > **Übersetzungen** in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Einzelheiten finden Sie unter [Übersetzungen in Tabellenmodellen &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md).    
 ### <a name="pasted-tables"></a>Eingefügte Tabellen    
 Es ist jetzt möglich, ein tabellarisches Modell mit 1100 oder 1103 auf 1200 zu aktualisieren, wenn das Modell eingefügte Tabellen enthält. Es wird empfohlen, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]zu verwenden. Legen Sie in SSDT **CompatibilityLevel** auf 1200 fest, und stellen Sie es dann in einer [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] -Instanz von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]bereit. Einzelheiten dazu finden Sie unter [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) .    
 ### <a name="calculated-tables-in-ssdt"></a>Berechnete Tabellen in SSDT    
Eine *berechnete Tabelle* ist eine reine Modellkonstruktion, die auf einem DAX-Ausdruck oder einer DAX-Abfrage in SSDT basiert. Wenn eine berechnete Tabelle in einer Datenbank bereitgestellt wird, kann sie nicht von regulären Tabellen unterschieden werden.    

 Es gibt verschiedene Verwendungsmöglichkeiten für berechnete Tabellen, einschließlich der Erstellung neuer Tabellen, um eine vorhandene Tabelle in einer bestimmten Rolle verfügbar zu machen. Das klassische Beispiel ist eine Datumstabelle, die in mehreren Kontexten (Bestelldatum, Versanddatum usw.) verwendet wird. Durch das Erstellen einer berechneten Tabelle für eine bestimmte Rolle können Sie jetzt eine Tabellenbeziehung aktivieren, um Abfragen oder Dateninteraktionen mit der berechneten Tabelle zu ermöglichen. Ein weiterer Verwendungszweck für berechnete Tabellen ist, Teile von vorhandenen Tabellen zu einer völlig neuen Tabelle zu kombinieren, die nur im Modell vorhanden ist.  Weitere Informationen finden Sie unter [Erstellen einer berechneten Tabelle &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/create-a-calculated-table-ssas-tabular.md).    
 ### <a name="formula-fixup"></a>Formelkorrektur    
 Mit der Formelkorrektur in einem tabellarischen 1200-Modell aktualisiert SSDT automatisch alle Measures, die auf eine Spalte oder Tabelle verweisen, die umbenannt wurde.    
 ### <a name="support-for-visual-studio-configuration-manager"></a>Unterstützung für den Visual Studio-Konfigurations-Manager    
 Für die Unterstützung mehrerer Umgebungen, z. B. Test- und Vorbereitungsumgebungen, können Entwickler in Visual Studio mit dem Konfigurations-Manager mehrere Projektkonfigurationen erstellen. Mehrdimensionale Modelle nutzen dies bereits, tabellarische Modellen bisher jedoch nicht. Ab dieser Version können Sie den Konfigurations-Manager für die Bereitstellung auf unterschiedlichen Servern verwenden.    

## <a name="instance-management"></a>Instanzverwaltung    
 ### <a name="administer-tabular-1200-models-in-ssms"></a>Verwalten von tabellarischen 1200-Modellen in SSMS    
 In dieser Version kann eine Analysis Services-Instanz im tabellarischen Servermodus tabellarische Modelle mit jedem Kompatibilitätsgrad (1100, 1103, 1200) ausführen. Die neueste Version von [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx) wurde aktualisiert, um Eigenschaften anzuzeigen und die Verwaltung von Datenbankmodellen für tabellarische Modelle mit Kompatibilitätsgrad 1200 zu ermöglichen.    
 ### <a name="parallel-processing-for-multiple-table-partitions-in-tabular-models"></a>Parallele Verarbeitung für mehrere Tabellenpartitionen in tabellarischen Modellen    
 Diese Version enthält neue Funktionen für die parallele Verarbeitung für Tabellen mit zwei oder mehr Partitionen, sodass die Verarbeitungsleistung erhöht wird. Es sind keine Konfigurationseinstellungen für diese Funktion vorhanden. Weitere Informationen zum Konfigurieren von Partitionen und zum Verarbeiten von Tabellen finden Sie unter [Tabellenmodellpartitionen &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md).    
 ### <a name="add-computer-accounts-as-administrators-in-ssms"></a>Hinzufügen von Computerkonten als Administratoren in SSMS    
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Administratoren können jetzt [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] zum Konfigurieren von Computerkonten als Mitglieder der [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Administratorgruppe verwenden. Legen Sie im Dialogfeld **Benutzer oder Gruppen auswählen** die **Speicherorte** für die Computerdomäne fest, und fügen Sie dann den Objekttyp **Computer** hinzu. Weitere Informationen finden Sie unter [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).    
 ### <a name="dbcc-for-analysis-services"></a>DBCC für Analysis Services    
 Database Consistency Checker (DBCC) wird intern ausgeführt, um potenzielle Probleme mit beschädigten Daten beim Laden der Datenbank zu ermitteln. Sie können das Tool aber auch bei Bedarf ausführen, wenn Sie Probleme in Ihren Daten oder Ihrem Modell vermuten. DBCC führt verschiedene Überprüfungen abhängig davon aus, ob das Modell tabellarisch oder mehrdimensional ist. Einzelheiten finden Sie unter [Datenbankkonsistenzprüfung &#40;DBCC&#41; für tabellarische und mehrdimensionale Analysis Services-Datenbanken](../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md).    
 ### <a name="extended-events-updates"></a>Updates für erweiterte Ereignisse    
 In dieser Version wird [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] eine grafische Benutzeroberfläche hinzugefügt, um erweiterte [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Ereignisse zu konfigurieren und zu verwalten. Sie können Livedatenströme zum Überwachen der Serveraktivität in Echtzeit einrichten, Sitzungsdaten für schnellere Analysen im Arbeitsspeicher belassen oder Datenströme für die Offlineanalyse in einer Datei speichern. Weitere Informationen finden Sie unter [Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) und im Guy in a Cube-Blogbeitrag und -Video zur [Verwendung erweiterter Ereignisse mit Analysis Services](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx).    



## <a name="scripting"></a>Skripterstellung
 ### <a name="powershell-for-tabular-models"></a>PowerShell für tabellarische Modelle    
 Diese Version enthält die PowerShell-Erweiterungen für tabellarische Modelle mit dem Kompatibilitätsgrad 1200. Sie können alle anwendbaren Cmdlets sowie spezifische Cmdlets für den tabellarischen Modus verwenden: [Invoke-ProcessASDatabase](../analysis-services/powershell/invoke-processasdatabase.md) und [Invoke-ProcessTable](../analysis-services/powershell/invoke-processtable-cmdlet.md).    
 ### <a name="ssms-scripting-database-operations"></a>SSMS-Skripts für Datenbankvorgänge    
 In der neuesten Version von [SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)sind Skripts jetzt für Datenbankbefehle aktiviert, einschließlich der Befehle zum Erstellen, Ändern, Löschen, Sichern, Wiederherstellen, Anfügen und Trennen. Die Ausgabe erfolgt in der Skriptsprache für tabellarische Modelle (Tabular Model Scripting Language, TMSL) in JSON. Weitere Informationen finden Sie unter [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../analysis-services/tabular-model-scripting-language-tmsl-reference.md).    
 ### <a name="analysis-services-execute-ddl-task"></a>DDL ausführen (Analysis Services-Task)    
 Der[Analysis Services-Task „DDL ausführen“](../integration-services/control-flow/analysis-services-execute-ddl-task.md) akzeptiert nun auch TMSL-Befehle (Tabular Model Scripting Language).     
 ### <a name="ssas-powershell-cmdlet"></a>SSAS-PowerShell-Cmdlets    
 Das SSAS-PowerShell-Cmdlet **Invoke-ASCmd** akzeptiert jetzt TMSL-Befehle (Tabular Model Scripting Language). Weitere SSAS-PowerShell-Cmdlets werden in einer künftigen Version aktualisiert, sodass die neuen tabellarischen Metadaten verwendet werden können (auf Ausnahmen wird in den Anmerkungen zur jeweiligen Version hingewiesen).    
Einzelheiten dazu finden Sie unter [Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) .    
 ### <a name="tabular-model-scripting-language-tmsl-supported-in-ssms"></a>TMSL-Unterstützung (Tabular Model Scripting Language) in SSMS    
  Mithilfe der [neuesten Version von SSMS](http://msdn.microsoft.com/library/mt238290.aspx)können Sie Skripts zum Automatisieren der meisten Verwaltungsaufgaben für tabellarische 1200-Modelle erstellen. Derzeit können die folgenden Aufgaben mithilfe von Skripts ausgeführt werden: „Process“ auf allen Ebenen sowie CREATE, ALTER und DELETE auf Datenbankebene.    
    
 Funktionell entspricht TMSL der ASSL-XMLA-Erweiterung, die mehrdimensionale Objektdefinitionen bietet. Jedoch verwendet TMSL native Deskriptoren wie **model**, **table**und **relationship** , um tabellarische Metadaten zu beschreiben. Weitere Einzelheiten zum Schema finden Sie unter [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../analysis-services/tabular-model-scripting-language-tmsl-reference.md).    
    
 Ein generiertes JSON-basiertes Skript für ein tabellarisches Modell könnte folgendermaßen aussehen:    
    
```    
{    
  "create": {    
    "database": { 
      "name": "AdventureWorksTabular1200",    
      "id": "AdventureWorksTabular1200",    
      "compatibilityLevel": 1200,    
      "readWriteMode": "readWrite",    
      "model": {}    
    }    
  }    
}    
```    

Die Nutzlast ist ein JSON-Dokument, das so einfach wie das oben gezeigte Beispiel sein kann. Es kann aber auch mit dem vollständigen Satz von Objektdefinitionen ausgeschmückt sein. Eine Beschreibung der Syntax [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../analysis-services/tabular-model-scripting-language-tmsl-reference.md).

Auf Datenbankebene geben die Befehle CREATE, ALTER und DELETE das TMSL-Skript im vertrauten XMLA-Fenster aus.  Andere Befehle wie „Process“ können in diesem Release auch mit Skripts verwendet werden. Skriptunterstützung für viele weitere Aktionen wird ggf. in einer zukünftigen Version hinzugefügt.    

**Skriptfähige Befehle** | **Beschreibung**
--------------- | ----------------
Erstellen|Fügt eine Datenbank, eine Verbindung oder eine Partition hinzu. Die ASSL-Entsprechung ist CREATE.
createOrReplace|Aktualisiert eine vorhandene Objektdefinition (Datenbank, Verbindung oder Partition) durch Überschreiben einer früheren Version. Die ASSL-Entsprechung ist ALTER, wobei „AllowOverwrite“ auf „true“ und „ObjectDefinition“ auf „ExpandFull“ festgelegt ist.
Löschen|Entfernt eine Objektdefinition. Die ASSL-Entsprechung ist DELETE.
refresh|Verarbeitet das Objekt. Die ASSL-Entsprechung ist PROCESS.

## <a name="dax"></a>DAX
### <a name="improved-dax-formula-editing"></a>Verbesserte DAX-Formelbearbeitung
Durch Updates der Bearbeitungsleiste können Sie Formeln einfacher schreiben, indem Sie Funktionen, Felder und Measures mithilfe von Syntaxfarben unterscheiden. Sie erhalten intelligente Funktions- und Feldvorschläge und werden mit „ *Fehlerwellenlinien*“ darüber informiert, ob Teile des DAX-Ausdrucks falsch sind. Zudem können Sie mehrere Zeilen (Alt + Eingabe) und Einzüge (Tab) verwenden. Über die Bearbeitungsleiste können Sie jetzt auch Kommentare als Teil Ihrer Measures schreiben. Geben Sie einfach „//“ ein, und alles in der gleichen Zeile nach diesen Zeichen wird als Kommentar gewertet.

### <a name="dax-variables"></a>DAX-Variablen    
Diese Version bietet jetzt Unterstützung für Variablen in DAX. Variablen können jetzt das Ergebnis eines Ausdrucks als benannte Variable speichern, die dann als Argument für andere Measureausdrücke übergeben werden kann. Sobald die resultierenden Werte für einen Variablenausdruck berechnet wurden, werden diese Werte nicht wieder geändert, auch wenn auf die Variable in einem anderen Ausdruck verwiesen wird. Weitere Informationen finden Sie unter [VAR-Funktion](http://msdn.microsoft.com/library/mt243785.aspx).    
### <a name="new-dax-functions"></a>Neue DAX-Funktionen
Mit dieser Version stellt DAX über 50 neue Funktionen zur Unterstützung schnellerer Berechnungen und verbesserter Visualisierungen in Power BI bereit. Weitere Informationen finden Sie unter [Neue DAX-Funktionen](http://msdn.microsoft.com/library/mt704075.aspx).
### <a name="save-incomplete-measures"></a>Speichern unvollständiger Measures
Sie können jetzt unvollständige DAX-Measures direkt in einem Projekt mit einem tabellarischen 1200-Modell speichern und erneut verwenden, wenn Sie fortfahren möchten.
### <a name="additional-dax-enhancements"></a>Zusätzliche DAX-Erweiterungen
- Nicht leere Berechnung: reduziert die Anzahl der Scans, die für nicht leere Berechnungen erforderlich sind.
- Measurezusammenführung: Mehrere Measures aus der gleichen Tabelle werden in einer Abfrage für das Speichermodul zusammengefasst.
- Gruppierungssätze: Wenn eine Abfrage Measures auf mehrere Granularitäten (Summe/Jahr/Monat) abfragt, wird nur eine Abfrage auf der untersten Ebene gesendet, und die restlichen Granularitäten werden von der niedrigsten Ebene abgeleitet.     
- Beseitigung redundanter Verknüpfungen: Eine einzelne Abfrage an das Speichermodul gibt sowohl die Dimensionsspalten als auch die Measurewerte zurück.
- Strenge Evaluierung von IF/SWITCH: Eine Verzweigung, deren Bedingung FALSE ist, führt nicht mehr zu Speichermodulabfragen. Früher wurden Verzweigungen sorgfältig ausgewertet, aber die Ergebnisse später verworfen.     
    
## <a name="developer"></a>Entwickler    
 ### <a name="microsoftanalysisservicestabular-namespace-for-tabular-1200-programmability-in-amo"></a>Microsoft.AnalysisServices.Tabular-Namespace für tabellarische 1200-Programmierbarkeit in AMO
 Zu Analysis Services Management Objects (AMO) gehört jetzt ein neuer tabellarischer Namespace für die Verwaltung einer tabellarischen Instanz von SQL Server 2016 Analysis Services sowie die Datendefinitionssprache zum programmgesteuerten Erstellen oder Ändern von tabellarischen 1200-Modellen. Weitere Informationen zur API finden Sie unter [Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) .    
 ### <a name="analysis-services-management-objects-amo-updates"></a>Aktualisierungen von Analysis Services Management Objects (AMO)
 [Analysis Services Management Objects &#40;AMO&#41;](http://msdn.microsoft.com/library/mt436122.aspx) wurde überarbeitet und enthält jetzt eine zweite Assembly: „Microsoft.AnalysisServices.Core.dll“. Die neue Assembly trennt allgemeine Klassen wie Server, Datenbank und Rolle, die umfassend in Analysis Services eingesetzt werden, unabhängig vom Servermodus.    
    
 Zuvor waren diese Klassen Teil der ursprünglichen Microsoft.AnalysisServices-Assembly. Durch das Verschieben in eine neue Assembly sind zukünftige Erweiterungen von AMO mit einer klaren Trennung zwischen generischen und kontextspezifischen APIs möglich.    
    
 Vorhandene Anwendungen sind von den neuen Assemblys sind nicht betroffen. Sollten Sie Anwendungen aus einem beliebigen Grund unter Verwendung der neuen AMO-Assembly neu erstellen, müssen Sie jedoch einen Verweis auf „Microsoft.AnalysisServices.Core“ hinzufügen.    
    
 Auch PowerShell-Skripts, die AMO laden und aufrufen, müssen jetzt „Microsoft.AnalysisServices.Core.dll“ laden. Achten Sie darauf, dass alle Skripts zu aktualisieren.  

### <a name="json-editor-for-bim-files"></a>JSON-Editor für BIM-Dateien
Mit der Codeansicht in Visual Studio 2015 wird jetzt die BIM-Datei für tabellarische 1200-Modelle im JSON-Format gerendert. Die Version von Visual Studio bestimmt, ob die BIM-Datei über den integrierten JSON-Editor in JSON oder als einfacher Text gerendert wird.

Damit Sie im JSON-Editor die Abschnitte des Modells erweitern und reduzieren können, benötigen Sie die neueste Version von SQL Server Data Tools sowie Visual Studio 2015 (beliebige Edition, einschließlich der kostenlosen Community Edition). Für alle anderen Versionen von SSDT oder Visual Studio wird die BIM-Datei in JSON als einfacher Text gerendert.
Ein leeres Modell enthält mindestens folgenden JSON-Code:

    ```    
    {    
      "name": "SemanticModel",
      "id": "SemanticModel",
      "compatibilityLevel": 1200,
      "readWriteMode": "readWrite",
      "model": {}
    }    
    ```    
    
> [!WARNING]    
> Vermeiden Sie das direkte Bearbeiten des JSON-Codes. Dadurch kann das Modell beschädigt werden.    
 ### <a name="new-elements-in-ms-csdlbi-20-schema"></a>Neue Elemente im Schema „MS-CSDLBI 2.0“    
 Die folgenden Elemente wurden dem komplexen Typ **TProperty** hinzugefügt, der im Schema „[MS-CSDLBI] 2.0“ definiert ist:    
    
|Element|Definition|    
|-------------|----------------|    
|DefaultValue|Eine Eigenschaft, die den Wert angibt, der beim Auswerten der Abfrage verwendet wird. Die DefaultValue-Eigenschaft ist optional, aber sie wird automatisch aktiviert, wenn die Werte des Elements nicht aggregiert werden können.|    
|Statistik|Ein Satz von Statistiken aus den zugrunde liegenden Daten, die der Spalte zugeordnet sind. Diese Statistiken werden vom komplexen Typ „TPropertyStatistics“ definiert und nur bereitgestellt, wenn das Generieren nicht rechenintensiv ist, wie im Abschnitt 2.1.13.5 des Dokuments „Conceptual Schema Definition File Format with Business Intelligence Annotations“ (Dateiformat der konzeptionellen Schemadefinition mit Business Intelligence-Anmerkungen) beschrieben.|    
    
## <a name="directquery"></a>DirectQuery    
### <a name="new-directquery-implementation"></a>Neue DirectQuery-Implementierung    
In dieser Version wurde DirectQuery für tabellarische 1200-Modelle erheblich erweitert. Zusammenfassung:    
-   DirectQuery generiert jetzt einfachere Abfragen, die eine höhere Leistung bieten.    
-   Die Funktion bietet zusätzliche Kontrolle über das Definieren von Beispieldatasets, die zum Entwerfen und Testen von Modellen verwendet werden.    
-   Sicherheit auf Zeilenebene (Row Level Security, RLS) wird jetzt im DirectQuery-Modus für tabellarische 1200-Modelle unterstützt. Zuvor hat das Vorhandensein von RLS verhindert, dass ein tabellarisches Modell im DirectQuery-Modus ausgeführt werden konnte.    
-   Berechnete Spalten werden nun für tabellarische 1200-Modelle im DirectQuery-Modus nicht unterstützt. Zuvor hat das Vorhandensein von berechneten Spalten verhindert, dass ein tabellarisches Modell im DirectQuery-Modus ausgeführt werden konnte.    
-   Die Leistungsoptimierung umfasst auch die Beseitigung redundanter Verknüpfungen für VertiPaq und DirectQuery. 

### <a name="new-data-sources-for-directquery-mode"></a>Neue Datenquellen für den DirectQuery-Modus    
 Jetzt für tabellarische 1200-Modelle im DirectQuery-Modus unterstützte Datenquellen umfassen, Oracle, Teradata und Microsoft Analytics Platform (ehemals Parallel Data Warehouse).    
    
Weitere Informationen finden Sie unter [DirectQuery-Modus &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).    

## <a name="see-also"></a>Siehe auch
[Analysis Services-Teamblog](http://blogs.msdn.microsoft.com/analysisservices/)    
[Neues in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)    
     

