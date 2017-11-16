---
title: "Database Consistency Checker (DBCC) für Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 28714c32-718f-4f31-a597-b3289b04b864
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2e8ecc3c51619c7f1ebbe5b109f0710500184a27
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="database-consistency-checker-dbcc-for-analysis-services"></a>Datenbankkonsistenzprüfung (DBCC) für Analysis Services
  DBCC ermöglicht bei Bedarf Datenbanküberprüfungen für mehrdimensionale und tabellarische Datenbanken auf einer Analysis Services-Instanz. Sie können DBCC in einem MDX- oder XMLA-Abfragefenster in SQL Server Management Studio (SSMS) ausführen und die DBCC-Ausgabe in SQL Server Profiler- oder XEvent-Sitzungen in SSMS verfolgen.  
Der Befehl verwendet eine Objektdefinition und gibt ein leeres Resultset oder ausführliche Fehlerinformationen zurück, wenn das Objekt beschädigt ist.   In diesem Artikel erfahren Sie, wie Sie den Befehl ausführen, die Ergebnisse analysieren und auftretende Probleme behandeln.  
  
 Bei tabellarischen Datenbanken entsprechen die von DBCC ausgeführten Konsistenzprüfungen der integrierten Überprüfung, die automatisch jedes Mal auftritt, wenn Sie eine Datenbank erneut laden, synchronisieren oder wiederherstellen.  Im Gegensatz dazu fallen Konsistenzprüfungen für mehrdimensionale Datenbanken nur an, wenn Sie DBCC bei Bedarf ausführen.  
  
 Der Umfang der Überprüfungen hängt vom Modus ab, wobei tabellarische Datenbanken einem breiteren Spektrum von Überprüfungen unterzogen werden.  
 Die Merkmale einer DBCC-Arbeitsauslastung variieren zudem je nach Servermodus. Überprüfungsvorgänge für mehrdimensionale Datenbanken umfassen das Lesen von Daten vom Datenträger und das Erstellen temporärer Indizes für den Vergleich mit tatsächlichen Indizes – alles Vorgänge, die erheblich mehr Zeit in Anspruch nehmen.  
  
 Die Befehlssyntax für DBCC verwendet die Objektmetadaten, die für den Typ der überprüften Datenbank spezifisch sind:  
  
-   Mehrdimensionale Datenbanken und tabellarische Datenbanken vor SQL Server 2016-Kompatibilitätsgrad 1100 oder 1103 sind in mehrdimensionalen Modellierungskonstrukten wie **cubeID**, **measuregroupID**und **partitionID**beschrieben.  
  
-   Metadaten für neue Tabellenmodell-Datenbanken mit Kompatibilitätsgrad 1200 oder höher bestehen aus Deskriptoren wie **TableName** und **PartitionName**.  
  
 DBCC für Analysis Services kann für eine Analysis Services-Datenbank mit jedem Kompatibilitätsgrad ausgeführt, solange die Datenbank auf einer SQL Server 2016-Instanz ausgeführt wird. Achten Sie darauf, dass Sie die richtige Befehlssyntax für die einzelnen Datenbanktypen verwenden.  
  
> [!NOTE]  
>  Wenn Sie mit [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md) vertraut sind, werden Sie schnell feststellen, dass DBCC in Analysis Services einen wesentlich geringeren Umfang hat. DBCC in Analysis Services ist ein einzelner Befehl, der ausschließlich Datenbeschädigungen in der gesamten Datenbank oder für einzelne Objekte angibt. Wenn Sie noch andere Aufgaben ausführen möchten, z. B. das Sammeln von Informationen, verwenden Sie stattdessen AMO PowerShell- oder XMLA-Skripts. Links zu weiteren Informationen finden Sie unter [Monitor an Analysis Services Instance](../../analysis-services/instances/monitor-an-analysis-services-instance.md) .  
  
## <a name="permission-requirements"></a>Berechtigungsanforderungen  
 Sie müssen Datenbank- oder Serveradministrator für Analysis Services (Mitglied der Serverrolle) sein, um den Befehl auszuführen. Anweisungen finden Sie unter [Erteilen von Datenbankberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) oder [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
## <a name="command-syntax"></a>Befehlssyntax 
 Höhere Kompatibilitätsgrade und tabellarische Datenbanken mit der 1200 verwenden tabellarische Metadaten für Objektdefinitionen. Im folgenden Beispiel wird die vollständige DBCC-Syntax für eine tabellarische Datenbank veranschaulicht, die auf einer SQL Server 2016-Funktionsebene erstellt wurde.  
  
 Die Hauptunterschiede zwischen den beiden Syntaxformen gehören einen neueren XMLA-Namespace nicht \<Objekt >-Element, und kein \<Modell >-Element (es gibt nach wie vor nur ein Modell pro Datenbank).  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2014/engine">  
     <DatabaseID>MyTabular1200DB_7811b5d8-c407-4203-8793-12e16c3d1b9b</DatabaseID>  
     <TableName>FactSales</TableName>  
     <PartitionName>FactSales 4</PartitionName>  
</DBCC>  
```  
  
 Sie benötigen keine untergeordneten Objekte wie Tabellen- oder Partitionsnamen, um das gesamte Schema zu überprüfen.  
  
 Sie können Objektnamen und DatabaseID über die Eigenschaftenseite des jeweiligen Objekts aus Management Studio abrufen.  
  
## <a name="command-syntax-for-multidimensional-and-tabular-110x-databases"></a>Befehlssyntax für mehrdimensionale und tabellarische 110x-Datenbanken  
 DBCC verwendet dieselbe Syntax für mehrdimensionale und tabellarische 1100- und 1103-Datenbanken. Sie können DBCC für bestimmte Datenbankobjekte ausführen, aber auch für die gesamte Datenbank. Weitere Informationen über die Objektdefinition finden Sie unter [Object-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md).  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2006</PartitionID>  
     </Object>  
</DBCC>  
  
```  
  
 Löschen Sie alle Objekt-ID-Elemente auf niedrigeren Ebenen, die Sie nicht benötigen, um DBCC für Objekte weiter oben in der Objektkette auszuführen:  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
     </Object>  
</DBCC>  
  
```  
  
 Bei tabellarischen 110x-Datenbanken wird die Syntax der Objektdefinition nach der Syntax des Process-Befehls modelliert (insbesondere bei der Zuordnung von Tabellen zu Dimensionen und Measuregruppen).  
  
-   **CubeID** entspricht der Modell-ID, dies ist **Model**.  
  
-   **MeasureGroupID** entspricht der Tabellen-ID.  
  
-   **PartitionID** entspricht der Partitions-ID.  
  
## <a name="usage"></a>Verwendung  
 In SQL Server Management Studio können Sie mithilfe eines MDX- oder XMLA-Abfragefensters DBCC aufrufen. Darüber hinaus können Sie mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Profiler oder Analysis Services XEvents die DBCC-Ausgabe anzeigen. Beachten Sie, dass SSAS DBCC-Meldungen nicht an das Windows-Anwendungsereignisprotokoll oder die Datei „msmdsrv.log“ übermittelt werden.  
  
 DBCC überprüft auf physische Datenbeschädigungen und auf logische Datenbeschädigungen, die auftreten, wenn verwaiste Elemente in einem Segment vorhanden sind. Vor dem Ausführen von DBCC muss eine Datenbank verarbeitet werden. Remotepartitionen, leere oder nicht verarbeitete Partitionen werden übersprungen.  
  
 Der Befehl wird in einer Lesetransaktion ausgeführt und kann daher durch „ForceCommitTimeout“ abgebrochen werden. Partitionsüberprüfungen werden parallel ausgeführt.  
  
 Der Neustart eines Diensts kann erforderlich sein, um eventuelle Datenbeschädigungen zu berücksichtigen, die seit dem letzten Neustart des Diensts aufgetreten sind. Das Wiederherstellen der Verbindung mit dem Server reicht nicht aus, um die Änderungen zu übernehmen.  
  
### <a name="run-dbcc-commands-in-management-studio"></a>Ausführen von DBCC-Befehlen in Management Studio  
 Öffnen Sie für Ad-hoc-Abfragen ein MDX- oder XMLA-Abfragefenster in SQL Server Management Studio. Klicken Sie dazu mit der rechten Maustaste auf die Datenbank, und wählen Sie **Neue Abfrage** | **XMLA**) aus, um den Befehl auszuführen und die Ausgabe zu lesen.  
  
 ![DBCC XML-Befehl in Management Studio](../../analysis-services/instances/media/ssas-dbcc-ssms.gif "XML DBCC-Befehl in Management Studio")  
  
 Auf der Registerkarte „Ergebnisse“ wird ein leeres Resultset dargestellt (siehe Screenshot), wenn keine Probleme erkannt wurden.  
  
 Die Registerkarte „Meldungen“ bietet detaillierte Informationen, ist jedoch für kleinere Datenbanken nicht immer zuverlässig. Statusmeldungen werden manchmal gekürzt, um anzugeben, dass der Befehl abgeschlossen wurde, jedoch ohne Meldungen zur Statusüberprüfung für jedes Objekt. Ein normaler Meldungsbericht kann dem in der folgenden Abbildung ähneln.  
  
 **Meldungsbericht von DBCC für die Cubeüberprüfung**  
  
```  
Executing the query ...  
READS, 0  
READ_KB, 0  
WRITES, 0  
WRITE_KB, 0  
CPU_TIME_MS, 0  
ROWS_SCANNED, 0  
ROWS_RETURNED, 0  
  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
<Object>  
<DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
<CubeID>Adventure Works</CubeID>  
</Object>  
</DBCC>  
Started checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2012' partition.  
Finished checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2013' partition.  
Finished checking segment indexes for the 'Internet_Sales_2012' partition.  
Started checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2011' partition.  
Finished checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2012' partition.  
Started checking segment indexes for the 'Internet_Orders_2013' partition.  
Finished checking segment indexes for the 'Internet_Orders_2012' partition.  
...   
Run complete  
  
```  
  
 **Ausgabe bei der Ausführung von DBCC für eine frühere Version von Analysis Services**  
  
 DBCC wird nur für Datenbanken auf einer [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanz unterstützt. Bei älteren Systemen wird beim Ausführen des Befehls der folgende Fehler zurückgegeben.  
  
```  
Executing the query ...  
The DBCC element at line 7, column 87 (namespace http://schemas.microsoft.com/analysisservices/2003/engine) cannot appear under Envelope/Body/Execute/Command.  
Execution complete  
  
```  
  
### <a name="trace-dbcc-output-in-sql-server-profiler-2016"></a>Verfolgen der DBCC-Ausgabe in SQL Server Profiler 2016  
 Sie können die DBCC-Ausgabe in einer Profiler-Ablaufverfolgung anzeigen, die Ereignisse von Fortschrittsberichten umfasst („Fortschrittsberichtsbeginn“, „Fortschrittsbericht aktuell“, „Fortschrittsberichtsende“ und „Fortschrittsberichtsfehler“).  
  
1.  Starten Sie eine Ablaufverfolgung. Unter [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md) finden Sie Hilfe zur Verwendung von SQL Server Profiler mit Analysis Services.  
  
2.  Wählen Sie **Command Begin** und **Command End** sowie einige oder alle der Ereignisse von **Fortschrittsberichten** aus.  
  
3.  Führen Sie den DBCC-Befehl in Management Studio in einem XMLA- oder MDX-Abfragefenster mit der Syntax aus, die in einem vorherigen Abschnitt bereitgestellt wurde.  
  
4.  DBCC-Aktivitäten werden in SQL Server Profiler über **Command** -Ereignisse mit einer Ereignisunterklasse von DBCC gekennzeichnet:  
  
     ![SSAS-Dbcc-Profiler-Eventsubclass](../../analysis-services/instances/media/ssas-dbcc-profiler-eventsubclass.PNG "Ssas-Dbcc-Profiler-Eventsubclass")  
  
     Der Ereigniscode 32 ist die DBCC-Ausführung.  
  
     Der Ereigniscode 64 ist ein DBCC-Fortschrittsbericht für einzelne Objekte.  
  
     Der Ereigniscode 63 ist eine Segmentprüfung für mehrdimensionale Objekte.  
  
     Prüfen Sie für beide Ereignisunterklassen **TextData** -Werte auf Meldungen, die von DBCC zurückgegeben wurden.  
  
     Statusmeldungen beginnen mit "Überprüfen der Konsistenz \<Objekt >", "Überprpfung \<Objekt >", oder "die Überprüfung abgeschlossen \<Objekt >".  
  
    > [!NOTE]  
    >  In CTP 3.0 werden Objekte durch interne Namen identifiziert. Beispielsweise wird eine Kategorienhierarchie als H$ Kategorien - formuliert\<ObjectID >. Interne Namen werden in einer zukünftigen CTP-Version durch für den Benutzer leicht zu merkende Namen ersetzt.  
  
     Fehlermeldungen sind weiter unten aufgeführt.  
  
### <a name="trace-dbcc-output-in-an-xevent-session-in-ssms"></a>Verfolgen der DBCC-Ausgabe in einer XEvent-Sitzung in SSMS  
 Sitzungen für erweiterte Ereignisse können Profiler-Ereignisse oder XEvents verwenden. Im vorherigen Abschnitt finden Sie eine Anleitung zum Hinzufügen von **Command** - und **Progress Report** -Ereignissen.  
  
1.  Starten Sie eine Sitzung, indem Sie mit der rechten Maustaste auf eine Datenbank klicken und anschließend **Verwaltung** >**Erweiterte Ereignisse** >  **Sitzungen** > **Neue Sitzung** auswählen. Weitere Informationen finden Sie unter  [Monitor Analysis Services with SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) .  
  
2.  Wählen Sie ein oder alle Ereignisse des **Fortschrittsberichts** für die Profiler-Ereigniskategorie oder **RequestProgress** -Ereignisse für die PureXevent-Kategorie aus.  
  
3.  Führen Sie den DBCC-Befehl in Management Studio in einem XMLA- oder MDX-Abfragefenster mit der Syntax aus, die in einem vorherigen Abschnitt bereitgestellt wurde.  
  
4.  Aktualisieren Sie in SSMS den Sitzungsordner. Klicken Sie mit der rechten Maustaste auf den Sitzungsnamen, und wählen Sie anschließend **Livedaten ansehen** aus.  
  
5.  Überprüfen Sie die TextData-Werte auf Meldungen, die von DBCC zurückgegeben wurden.  TextData ist eine Eigenschaft eines Ereignisfelds und zeigt Status- und Fehlermeldungen an, die vom Ereignis zurückgegeben werden.  
  
     Statusmeldungen beginnen mit "Überprüfen der Konsistenz \<Objekt >", "Überprpfung \<Objekt >", oder "die Überprüfung abgeschlossen \<Objekt >".  
  
     Fehlermeldungen sind weiter unten aufgeführt.  
  
## <a name="reference-consistency-checks-and-errors-for-multidimensional-databases"></a>Referenz: Konsistenzprüfungen und Fehler für mehrdimensionale Datenbanken  
 Bei mehrdimensionalen Datenbanken werden nur Partitionsindizes überprüft.  Während der Ausführung erstellt DBCC einen temporären Index für jede Partition und vergleicht ihn mit dem permanenten Index auf dem Datenträger.  Für das Erstellen eines temporären Index müssen alle Daten der Partitionsdaten auf dem Datenträger gelesen werden, und dann muss ein temporärer Index für Vergleiche im Arbeitsspeicher beibehalten werden. Angesichts der zusätzlichen Arbeitsauslastung können auf dem Server während der DBCC-Ausführung erheblich mehr Datenträger-E/A-Vorgänge und eine größere Arbeitsspeichernutzung auftreten.  
  
 Die Erkennung von mehrdimensionalen Indexfehler umfasst die folgenden Prüfungen. Fehler in dieser Tabelle werden in XEvent- oder Profiler-Ablaufverfolgungen für Fehler auf Objektebene angezeigt.  
  
||||  
|-|-|-|  
|**Objekt**|**Beschreibung der DBCC-Prüfung**|**Fehler beim Fehlschlagen**|  
|Partitionsindex|Überprüft Segmentstatistiken und -indizes.<br /><br /> Vergleicht die ID jedes Elements im temporären Partitionsindex mit den auf dem Datenträger gespeicherten Partitionsstatistiken.  Wenn im temporären Index ein Element mit einem Daten-ID-Wert außerhalb des Bereichs gefunden wird, der für die Partitionsindexstatistiken auf dem Datenträger gespeichert ist, werden die Statistiken für den Index als beschädigt betrachtet.|Die Partitionssegmentstatistiken sind beschädigt.|  
|Partitionsindex|Überprüft die Metadaten.<br /><br /> Stellt sicher, dass jedes Element im temporären Index in der Indexheaderdatei für das Segment auf dem Datenträger gefunden werden kann.|Das Partitionssegment ist beschädigt.|  
|Partitionsindex|Überprüft Segmente auf physische Beschädigungen.<br /><br /> Liest die Indexdatei auf dem Datenträger für jedes Element im temporären Index und stellt sicher, dass die Größe der Indexdatensätze übereinstimmt und dass die gleichen Datenseiten als Datenseiten mit Datensätzen für das aktuelle Element markiert sind.|Das Partitionssegment ist beschädigt.|  
  
## <a name="reference-consistency-checks-and-errors-for-tabular-databases"></a>Referenz: Konsistenzprüfungen und Fehler für tabellarische Datenbanken  
 In der folgenden Tabelle sind alle Konsistenzprüfungen, die für Tabellenobjekte ausgeführt werden, zusammen mit den Fehlern, die ausgelöst werden, wenn eine Prüfung eine Beschädigung angibt, aufgeführt. Fehler in dieser Tabelle werden in XEvent- oder Profiler-Ablaufverfolgungen für Fehler auf Objektebene angezeigt.  
  
||||  
|-|-|-|  
|**Objekt**|**Beschreibung der DBCC-Prüfung**|**Fehler beim Fehlschlagen**|  
|Datenbank|Überprüft die Anzahl von Tabellen in der Datenbank.  Ein Wert kleiner als null gibt eine Beschädigung an.|Beschädigung in der Speicherebene. Tabellensammlung in der Datenbank „%{parent/}“ ist beschädigt.|  
|Datenbank|Überprüft die interne Struktur, die zum Nachverfolgen der referenziellen Integrität verwendet wird, und löst einen Fehler aus, wenn die Größe nicht korrekt ist.|Die Datenbankdateien haben die Konsistenzprüfungen nicht bestanden.|  
|Tabelle|Überprüft den internen Wert, der verwendet wird, um zu bestimmen, ob die Tabelle eine Dimensions- oder Faktentabellen ist.  Ein Wert außerhalb des bekannten Bereichs gibt eine Beschädigung an.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Tabellenstatistik fehlgeschlagen.|  
|Tabelle|Überprüft, ob die Anzahl der Partitionen in der Segmentzuordnung für die Tabelle mit der Anzahl der für die Tabelle definierten Partitionen übereinstimmt.|Beschädigung in der Speicherebene. Partitionssammlung in der Tabelle „%{parent/}“ ist beschädigt.|  
|Tabelle|Wenn eine tabellarische Datenbank erstellt oder aus PowerPivot für Excel 2010 importiert wurde und eine Partitionsanzahl größer als eins aufweist, wird ein Fehler ausgelöst, da Partitionsunterstützung in höheren Versionen hinzugefügt wurde und dies auf eine Beschädigung hinweist.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Segmentzuordnung fehlgeschlagen.|  
|Partition|Überprüft für jede Partition, ob die Anzahl der Segmente von Daten und die Anzahl der Datensätze für jedes Segment von Daten im Segment mit den im Index für das Segment gespeicherten Werten übereinstimmt.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Segmentzuordnung fehlgeschlagen.|  
|Partition|Ein Fehler wird ausgelöst, wenn die Gesamtanzahl der Datensätze, Segmente oder Datensätze pro Segment ungültig ist (kleiner als null) oder wenn die Anzahl der Segmente nicht mit der berechneten Anzahl von Segmenten übereinstimmt, die basierend auf der Gesamtanzahl der Datensätze erforderlich sind.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Segmentzuordnung fehlgeschlagen.|  
|Beziehung|Ein Fehler wird ausgelöst, wenn die zum Speichern von Daten über die Beziehung verwendete Struktur keine Datensätze enthält oder wenn der Name der in der Beziehung verwendeten Tabelle leer ist.|Fehler bei Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Beziehungen.|  
|Beziehung|Es wird überprüft, ob die Namen der primären Tabelle, primären Spalte, Fremdtabelle und Fremdspalte festgelegt sind und ob auf die Spalten und Tabellen, die an der Beziehung beteiligt sind, zugegriffen werden kann.<br /><br /> Es wird überprüft, ob die beteiligten Spaltentypen gültig sind und ob der Index der Primärschlüssel-/Fremdschlüsselwerte eine gültige Suchstruktur ergibt.|Fehler bei Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Beziehungen.|  
|Hierarchy|Ein Fehler wird ausgelöst, wenn die Sortierreihenfolge für die Hierarchie kein gültiger Wert ist.|Fehler bei Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Hierarchie „%{hier/}“.|  
|Hierarchy|Die in der Hierarchie ausgeführten Prüfungen sind abhängig vom internen Typ des verwendeten Hierarchiezuordnungsschemas.<br /><br /> Alle Hierarchien werden auf den richtigen verarbeiteten Status, auf das Vorhandensein des Hierarchiespeichers und ggf. auf das Vorhandensein von Datenstrukturen, die für eine Konvertierung der Daten-ID in eine Hierarchieposition verwendet werden, überprüft.<br /><br /> Wenn alle Prüfungen erfolgreich sind, wird die Hierarchiestruktur durchlaufen, um sicherzustellen, dass jede Position in der Hierarchie auf das richtige Element verweist.<br />Wenn einer dieser Tests fehlschlägt, wird ein Fehler ausgelöst.|Fehler bei Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Hierarchie „%{hier/}“.|  
|Benutzerdefinierte Hierarchie|Überprüft, ob die Namen der Hierarchieebenen festgelegt wurden.<br /><br /> Wenn die Hierarchie verarbeitet wurde, wird überprüft, ob der interne Hierarchiedatenspeicher das richtige Format aufweist.  Es wird sichergestellt, dass der interne Hierarchiespeicher keine ungültigen Datenwerte enthält.<br /><br /> Wenn die Hierarchie als nicht verarbeitet gekennzeichnet ist, vergewissern Sie sich, dass dieser Status für alte Datenstrukturen gilt und dass alle Ebenen der Hierarchie als leer markiert sind.|Fehler bei Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Hierarchie „%{hier/}“.|  
|Column|Ein Fehler wird ausgelöst, wenn die für die Spalte verwendete Codierung nicht auf einen bekannten Wert festgelegt ist.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Spaltenstatistik fehlgeschlagen.|  
|Column|Es wird überprüft, ob die Spalte vom Modul im Speicher komprimiert wurde.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Spaltenstatistik fehlgeschlagen.|  
|Column|Der Typ der Komprimierung der Spalte wird auf bekannte Werte überprüft.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Spaltenstatistik fehlgeschlagen.|  
|Column|Wenn die „Tokenisierung“ der Spalte nicht auf einen bekannten Wert festgelegt ist, wird ein Fehler ausgelöst.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Spaltenstatistik fehlgeschlagen.|  
|Column|Wenn der für ein Datenwörterbuch für Spalten gespeicherte ID-Bereich nicht mit der Anzahl der Werte im Datenwörterbuch übereinstimmt oder außerhalb des zulässigen Bereichs liegt, wird ein Fehler ausgelöst.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens des Datenwörterbuchs fehlgeschlagen.|  
|Column|Es wird überprüft, ob die Anzahl der Datensegmente für eine Spalte mit der Anzahl der Datensegmente für die Tabelle, zu der sie gehört, übereinstimmt.|Beschädigung in der Speicherebene. Segmentsammlung in der Spalte „%{parent/}“ ist beschädigt.|  
|Column|Es wird überprüft, ob die Anzahl der Partitionen für eine Datenspalte mit der Anzahl der Partitionen für die Datensegmentzuordnung der Spalte übereinstimmt.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Segmentzuordnung fehlgeschlagen.|  
|Column|Es wird überprüft, ob die Anzahl der Datensätze in einem Spaltensegment mit der im Index für das Spaltensegment gespeicherten Anzahl der Datensätze übereinstimmt.|Beschädigung in der Speicherebene. Segmentsammlung in der Spalte „%{parent/}“ ist beschädigt.|  
|Column|Wenn eine Spalte keine Segmentstatistiken enthält, wird ein Fehler ausgelöst.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Segmentstatistik fehlgeschlagen.|  
|Column|Wenn eine Spalte keine Komprimierungsinformationen oder keinen Segmentspeicher enthält, wird ein Fehler ausgelöst.|Die Datenbankdateien haben die Konsistenzprüfungen nicht bestanden.|  
|Column|Ein Fehler wird gemeldet, wenn Segmentstatistiken für eine Spalte nicht mit den tatsächlichen Spaltenwerten für die minimale Daten-ID, die maximale Daten-ID, die Anzahl unterschiedlicher Werte, die Anzahl der Zeilen oder das Vorhandensein von NULL-Werten übereinstimmen.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Segmentstatistik fehlgeschlagen.|  
|ColumnSegment|Wenn die minimale Daten-ID oder die maximale Daten-ID kleiner als der vom System reservierte Wert für NULL ist, werden die Spaltensegmentinformationen als beschädigt markiert.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Segmentstatistik fehlgeschlagen.|  
|ColumnSegment|Wenn keine Zeilen für dieses Segment vorhanden sind, sollten die minimalen und maximalen Datenwerte für die Spalte auf den vom System reservierten Wert für NULL festgelegt werden.  Wenn der Wert nicht null ist, wird ein Fehler ausgelöst.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Segmentstatistik fehlgeschlagen.|  
|ColumnSegment|Wenn die Spalte Zeilen und mindestens einen Wert ungleich null aufweist, wird überprüft, ob die minimale und die maximale Daten-ID für die Spalte größer als der vom System reservierte Wert für NULL ist.|Datenbankkonsistenzprüfungen (DBCC) während des Überprüfens der Segmentstatistik fehlgeschlagen.|  
|Intern|Es wird überprüft, ob der Speicherhinweis für die Tokenisierung festgelegt wurde und ob gültige Zeiger für interne Tabellen vorhanden sind, wenn der Speicher verarbeitet wird.  Wenn der Speicher nicht verarbeitet wird, wird überprüft, ob alle Zeiger null sind.<br />Wenn dies nicht der Fall ist, wird ein generischer DBCC-Fehler zurückgegeben.|Die Datenbankdateien haben die Konsistenzprüfungen nicht bestanden.|  
|DBCC-Datenbank|Ein Fehler wird ausgelöst, wenn das Datenbankschema keine Tabellen aufweist oder wenn auf eine oder mehrere Tabellen nicht zugegriffen werden kann.|Beschädigung in der Speicherebene. Tabellensammlung in der Datenbank „%{parent/}“ ist beschädigt.|  
|DBCC-Datenbank|Ein Fehler wird ausgelöst, wenn eine Tabelle als temporär markiert ist oder einen unbekannten Typ aufweist.|Fehlerhafter Tabellentyp festgestellt.|  
|DBCC-Datenbank|Ein Fehler wird ausgelöst, wenn die Anzahl der Beziehungen für eine Tabelle einen negativen Wert hat oder wenn für eine Tabelle eine Beziehung definiert wurde und eine entsprechende Beziehungsstruktur nicht gefunden wurde.|Beschädigung in der Speicherebene. Beziehungssammlung in der Tabelle „%{parent/}“ ist beschädigt.|  
|DBCC-Datenbank|Wenn der Kompatibilitätsgrad für die Datenbank 1050 ist (SQL Server 2008 R2/PowerPivot v1.0) und die Anzahl der Beziehungen die Anzahl der Tabellen im Modell überschreitet, wird die Datenbank als beschädigt markiert.|Die Datenbankdateien haben die Konsistenzprüfungen nicht bestanden.|  
|DBCC-Tabelle|Für die validierte Tabelle wird überprüft, ob die Anzahl der Spalten kleiner ist als null. In dem Fall wird ein Fehler ausgelöst.  Ein Fehler tritt auch auf, wenn der Spaltenspeicher für eine Spalte in der Tabelle NULL ist.|Beschädigung in der Speicherebene. Spaltensammlung in der Tabelle „%{parent/}“ ist beschädigt.|  
|DBCC-Partition|Überprüft die Tabelle, zu der die Partition gehört, die validiert wird. Wenn die Anzahl der Spalten für die Tabelle kleiner als null ist, wird angegeben, dass die Spaltensammlung für die Tabelle beschädigt ist. Ein Fehler tritt auch auf, wenn der Spaltenspeicher für eine Spalte in der Tabelle NULL ist.|Beschädigung in der Speicherebene. Spaltensammlung in der Tabelle „%{parent/}“ ist beschädigt.|  
|DBCC-Partition|Durchläuft jede Spalte für die ausgewählte Partition und überprüft, ob jedes Segment für die Partition einen gültigen Link zu einer Spaltensegmentstruktur aufweist.  Wenn ein Segment einen NULL-Link enthält, wird die Partition als beschädigt betrachtet.|Beschädigung in der Speicherebene. Segmentsammlung in der Spalte „%{parent/}“ ist beschädigt.|  
|Column|Gibt einen Fehler zurück, wenn der Spaltentyp nicht gültig ist.|Fehlerhafter Segmenttypen festgestellt.|  
|Column|Gibt einen Fehler zurück, wenn eine Spalte eine negative Anzahl für die Anzahl der Segmente in einer Spalte aufweist oder wenn der Zeiger für die Spaltensegmentstruktur für ein Segment einen NULL-Link enthält.|Beschädigung in der Speicherebene. Segmentsammlung in der Spalte „%{parent/}“ ist beschädigt.|  
|DBCC-Befehl|Der DBCC-Befehl zeigt mehrere Meldungen an, während er den DBCC-Vorgang durchführt.  Er zeigt vor dem Start eine Statusmeldung an, die den Datenbank-, Tabellen- oder Spaltennamen des Objekts enthält, und eine weitere nach Abschluss der einzelnen Objektüberprüfungen.|Überprüfen der Konsistenz der \<Objectname > \<Objecttype >. Phase: vorab prüfen.<br /><br /> Überprüfen der Konsistenz der \<Objectname > \<Objecttype >. Phase: Nachprüfung.|  
  
## <a name="common-resolutions-for-error-conditions"></a>Allgemeine Lösungen für Fehlerbedingungen  
 Die folgenden Fehler werden in SQL Server Management Studio oder in „msmdsrv.log“-Dateien angezeigt. Diese Fehler treten auf, wenn mindestens eine Überprüfung nicht erfolgreich ausgeführt wird. Je nach Fehler ist die empfohlene Lösung ein Objekt zu verarbeiten, eine Lösung zu löschen und erneut bereitzustellen oder die Datenbank wiederherzustellen.  
  
|Fehler|Problem|Lösung|  
|-----------|-----------|----------------|  
|**Fehler im Metadaten-Manager**<br /><br /> Der Objektverweis "\<ObjectID >" ist ungültig. Er stimmt nicht mit der Struktur der Metadatenklassenhierarchie überein.|Falsch formatierter Befehl|Überprüfen Sie die Befehlssyntax. Wahrscheinlich haben Sie ein Objekt einer niedrigeren Ebene aufgenommen, ohne mindestens eines der übergeordneten Objekte anzugeben.|  
|**Fehler im Metadaten-Manager**<br /><br /> Entweder die \<Objekt > mit der ID "\<ObjectID >" ist nicht in der \<Parentobject > mit der ID "\<übergeordnetes >', oder der Benutzer verfügt nicht über die Berechtigungen zum Zugriff auf das.|Beschädigung des Index (mehrdimensional)|Verarbeiten Sie das Objekt und alle abhängigen Objekte erneut.|  
|**Fehler bei der Konsistenzprüfung der Partition**<br /><br /> Fehler beim Überprüfen der Konsistenz der \<Partitionsname > Partition der \<measuregruppenname > Measuregruppe für die \<Cubename > cube aus der \<Datenbankname > Datenbank. Dies können Sie möglicherweise beheben, indem die Partition oder die Indizes erneut verarbeitet werden.|Beschädigung des Index (mehrdimensional)|Verarbeiten Sie das Objekt und alle abhängigen Objekte erneut.|  
|**Partitionssegmentstatistiken beschädigt**|Beschädigung des Index (mehrdimensional)|Verarbeiten Sie das Objekt und alle abhängigen Objekte erneut.|  
|**Partitionssegment beschädigt**|Metadatenbeschädigung (mehrdimensional oder tabellarisch)|Löschen Sie das Projekt, und stellen Sie es erneut bereit, oder führen Sie eine Wiederherstellung aus einer Sicherung und eine erneute Verarbeitung durch.<br /><br /> Anweisungen finden Sie im Blogbeitrag [How to handle corruption in Analysis Services databases](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Behandeln von Beschädigungen in Analysis Services-Datenbanken).|  
|**Beschädigung von Tabellenmetadaten**<br /><br /> Tabelle \<Tabellenname > Datei mit Tabellenmetadaten beschädigt. Die Haupttabelle wurde unter dem DataFileList-Knoten nicht gefunden.|Metadatenbeschädigung (nur tabellarisch)|Löschen Sie das Projekt, und stellen Sie es erneut bereit, oder führen Sie eine Wiederherstellung aus einer Sicherung und eine erneute Verarbeitung durch.<br /><br /> Anweisungen finden Sie im Blogbeitrag [How to handle corruption in Analysis Services databases](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Behandeln von Beschädigungen in Analysis Services-Datenbanken).|  
|**Beschädigung in der Speicherebene**<br /><br /> Beschädigung in der Speicherebene: Auflistung von \<Type-Name > in \<übergeordneten-Name > \<übergeordneten Typ > ist beschädigt.|Metadatenbeschädigung (nur tabellarisch)|Löschen Sie das Projekt, und stellen Sie es erneut bereit, oder führen Sie eine Wiederherstellung aus einer Sicherung und eine erneute Verarbeitung durch.<br /><br /> Anweisungen finden Sie im Blogbeitrag [How to handle corruption in Analysis Services databases](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Behandeln von Beschädigungen in Analysis Services-Datenbanken).|  
|**Systemtabelle fehlt**<br /><br /> Systemtabelle \<Tabellenname > ist nicht vorhanden.|Objektbeschädigung (nur tabellarisch)|Verarbeiten Sie das Objekt und alle abhängigen Objekte erneut.|  
|**Tabellenstatistik ist beschädigt**<br /><br /> Statistiken der Tabelle \<Tabellenname > ist nicht vorhanden.|Metadatenbeschädigung (nur tabellarisch)|Löschen Sie das Projekt, und stellen Sie es erneut bereit, oder führen Sie eine Wiederherstellung aus einer Sicherung und eine erneute Verarbeitung durch.<br /><br /> Anweisungen finden Sie im Blogbeitrag [How to handle corruption in Analysis Services databases](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Behandeln von Beschädigungen in Analysis Services-Datenbanken).|  
  
## <a name="disable-automatic-consistency-checks-on-database-load-operations-through--the-msmdsrvini-configuration-file"></a>Deaktivieren automatischer Konsistenzprüfungen für Datenbankladevorgänge über die Konfigurationsdatei „msmdsrv.ini“  
 Es ist zwar nicht empfehlenswert, aber Sie können die integrierten Datenbankkonsistenzprüfungen deaktivieren, die automatisch bei Ereignissen beim Laden von Datenbanken auftreten (nur für tabellarische Datenbanken). Dazu müssen Sie eine Konfigurationseinstellung in der Datei „msmdsrv.ini“ ändern:  
  
```  
<ConfigurationSettings>  
     <Vertipaq />  
          <DisableConsistencyChecks />  
```  
  
 Diese Einstellung ist in der Konfigurationsdatei nicht vorhanden und muss manuell hinzugefügt werden.  
  
 Gültige Werte sind:  
  
-   **-2** (Standardeinstellung): DBCC ist aktiviert. Wenn der Server mit einem hohen Grad an Sicherheit den Fehler logisch auflösen kann, wird ein Fix automatisch angewendet. Andernfalls wird ein Fehler protokolliert.  
  
-   **-1** : DBCC ist teilweise aktiviert. DBCC ist für RESTORE-Überprüfungen und Überprüfungen vor dem Commit aktiviert, mit denen der Datenbankstatus am Ende einer Transaktion überprüft wird.  
  
-   **0** : DBCC ist teilweise aktiviert. Datenbankkonsistenzprüfungen werden während RESTORE-, IMAGELOAD-, LOCALCUBELOAD- und ATTACH-  
         Vorgängen ausgeführt.  
  
-   **1** : DBCC ist deaktiviert. Prüfungen der Datenintegrität sind deaktiviert, jedoch werden Deserialisierungsprüfungen weiterhin ausgeführt.  
  
> [!NOTE]  
>  Diese Einstellung hat keine Auswirkungen auf DBCC, wenn der Befehl nach Bedarf ausgeführt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Verarbeiten von Datenbank, Tabelle oder Partition &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [Verarbeiten eines mehrdimensionalen Modells &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Überwachen einer Instanz von Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)   
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  

