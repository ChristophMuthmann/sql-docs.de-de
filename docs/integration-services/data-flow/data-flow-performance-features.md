---
title: "Funktionen für die Datenflussleistung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Integration Services packages, performance
- performance [Integration Services]
- data flow [Integration Services], troubleshooting
- SQL Server Integration Services packages, performance
- loading data
- control flow [Integration Services], troubleshooting
- SSIS packages, performance
- packages [Integration Services], performance
- queries [Integration Services], troubleshooting
- sorting data [Integration Services]
- aggregations [Integration Services]
ms.assetid: c4bbefa6-172b-4547-99a1-a0b38e3e2b05
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 508d0f2774033dee83ba600036ab09efd39eaa58
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="data-flow-performance-features"></a>Data Flow Performance Features
  Dieses Thema bietet Vorschläge, wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete entworfen werden müssen, damit allgemeine Leistungsprobleme vermieden werden. Dieses Thema enthält zudem Informationen zu Funktionen und Tools, die Sie verwenden können, um Leistungsprobleme von Paketen zu beheben.  
  
## <a name="configuring-the-data-flow"></a>Konfigurieren des Datenflusses  
 Wenn Sie den Datenflusstask für eine bessere Leistung konfigurieren möchten, können Sie die Eigenschaften des Tasks konfigurieren, die Puffergröße anpassen und das Paket für die parallele Ausführung konfigurieren.  
  
### <a name="configure-the-properties-of-the-data-flow-task"></a>Konfigurieren der Eigenschaften des Datenflusstasks  
  
> [!NOTE]  
>  Die in diesem Abschnitt behandelten Eigenschaften müssen für jeden Datenflusstask in einem Paket einzeln festgelegt werden.  
  
 Sie können die folgenden leistungsbeeinflussenden Eigenschaften des Datenflusstasks konfigurieren:  
  
-   Geben Sie den Speicherort für die temporäre Speicherung von Pufferdaten (BufferTempStoragePath-Eigenschaft) sowie von Spalten an, die BLOB-Daten (Binary Large Object) (BLOBTempStoragePath-Eigenschaft) enthalten. Standardmäßig enthalten diese Eigenschaften die Werte der Umgebungsvariablen TEMP und TMP. Sie können andere Ordner auf einem anderen oder schnelleren Festplattenlaufwerk zum Speichern der temporären Dateien angeben oder die Dateien auf mehrere Laufwerke verteilt speichern. Sie können mehrere Verzeichnisse angeben, indem Sie die Verzeichnisnamen durch Semikolons voneinander trennen.  
  
-   Definieren Sie die Standardgröße des Puffers, den der Task verwendet, mithilfe der DefaultBufferSize-Eigenschaft und die maximale Anzahl von Zeilen im Puffer mithilfe der DefaultBufferMaxRows-Eigenschaft. Legen Sie die AutoAdjustBufferSize-Eigenschaft fest, um anzugeben, ob die Standardgröße des Puffers automatisch aus dem Wert der DefaultBufferMaxRows-Eigenschaft berechnet wird. Die Standardpuffergröße beträgt 10 Megabytes, die maximale Puffergröße 2^31-1 Bytes. Der Standardwert für die maximale Anzahl von Zeilen beträgt 10.000.  
  
-   Legen Sie über die EngineThreads-Eigenschaft die Anzahl von Threads fest, die der Task während der Ausführung verwenden kann. Die Eigenschaft liefert dem Datenflussmodul einen Vorschlag für die Anzahl der zu verwendenden Threads. Der Standardwert ist 10 mit einem Mindestwert von 3. Unabhängig von dem für diese Eigenschaft festgelegten Wert verwendet das Modul jedoch nie mehr Threads als notwendig. Das Modul verwendet bei Bedarf auch mehr Threads, als in der Eigenschaft angegeben, um Parallelitätsprobleme zu vermeiden.  
  
-   Geben Sie an, ob der Datenflusstask im optimierten Modus ausgeführt werden soll (RunInOptimizedMode-Eigenschaft). Der optimierte Modus verbessert die Leistung, indem nicht verwendete Spalten, Ausgaben und Komponenten aus dem Datenfluss entfernt werden.  
  
    > [!NOTE]  
    >  Die gleichnamige Eigenschaft RunInOptimizedMode kann in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] auf Projektebene festgelegt werden, um anzugeben, dass der Datenflusstask beim Debuggen im optimierten Modus ausgeführt werden soll. Diese Eigenschaft überschreibt die RunInOptimizedMode-Eigenschaft von Datenflusstasks zur Entwurfszeit.  
  
### <a name="adjust-the-sizing-of-buffers"></a>Anpassen der Puffergrößenanpassung  
 Zum Anpassen der Puffergrößen schätzt das Datenflussmodul zuerst die Größe einer einzelnen Datenzeile. Dann multipliziert es die Größe der Zeile mit dem Wert von DefaultBufferMaxRows, um einen vorläufigen Arbeitswert für die Puffergröße zu erhalten.  
  
-   Wenn AutoAdjustBufferSize auf TRUE festgelegt ist, verwendet das Datenflussmodul den berechneten Wert als Puffergröße und der Wert von DefaultBufferSize wird ignoriert.  
  
-   Wenn AutoAdjustBufferSize auf FALSE festgelegt ist, bestimmt das Datenflussmodul die Puffergröße anhand der folgenden Regeln.  
  
    -   Wenn das Ergebnis größer ist als der Wert von DefaultBufferSize, verringert das Modul die Anzahl der Zeilen.  
  
    -   Wenn das Ergebnis kleiner ist als die intern berechnete minimale Puffergröße, vergrößert das Modul die Anzahl der Zeilen.  
  
    -   Wenn das Ergebnis zwischen der minimalen Puffergröße und dem Wert von DefaultBufferSize liegt, nähert das Modul die Größe des Puffers so gut wie möglich an das Produkt aus geschätzter Zeilengröße und Wert von DefaultBufferMaxRows an.  
  
 Verwenden Sie beim Testen der Leistung Ihrer Datenflusstasks zu Anfang die Standardwerte für DefaultBufferSize und DefaultBufferMaxRows. Aktivieren Sie die Protokollierung für den Datenflusstask, und wählen Sie das BufferSizeTuning-Ereignis aus, um festzustellen, wie viele Zeilen jeder Puffer enthält.  
  
 Bevor Sie mit dem Anpassen der Puffergrößenanpassung beginnen, sollten Sie die Größe jeder Datenspalte verringern, indem Sie nicht benötigte Spalten entfernen und die Datentypen entsprechend konfigurieren. Dies ist die wichtigste Verbesserungsmöglichkeit, die Sie vornehmen können.  
  
 Probieren Sie zum Bestimmen der optimalen Pufferanzahl und -größe verschiedene Wert für DefaultBufferSize und DefaultBufferMaxRows aus. Überwachen Sie dabei die Leistung und die vom BufferSizeTuning-Ereignis gemeldeten Informationen.  
  
 Erhöhen Sie die Puffergröße nicht bis zu dem Punkt, an dem die Auslagerung auf den Datenträger beginnt. Die Auslagerung auf den Datenträger beeinträchtigt die Leistung mehr als eine nicht optimierte Puffergröße. Überwachen Sie den Leistungsindikator „Gespoolte Puffer“ im Leistungs-Snap-In der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Management Console (MMC), um zu bestimmen, ob eine Auslagerung auftritt.  
  
### <a name="configure-the-package-for-parallel-execution"></a>Konfigurieren des Pakets zur parallelen Ausführung  
 Die parallele Ausführung verbessert die Leistung auf Computern, die über mehrere physische oder logische Prozessoren verfügen. Um die parallele Ausführung verschiedener Tasks im Paket zu unterstützen, verwendet [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zwei Eigenschaften: **MaxConcurrentExecutables** und **EngineThreads**.  
  
#### <a name="the-maxconcurrentexcecutables-property"></a>Die MaxConcurrentExecutables-Eigenschaft  
 Die **MaxConcurrentExecutables** -Eigenschaft ist eine Eigenschaft des Pakets selbst. Diese Eigenschaft definiert, wie viele Tasks gleichzeitig ausgeführt werden können. Der Standardwert ist -1, das bedeutet die Anzahl der physischen oder logischen Prozessoren plus 2.  
  
 Stellen Sie sich ein Beispielpaket mit drei Datenflusstasks vor, um zu verstehen, wie diese Eigenschaft funktioniert. Wenn Sie **MaxConcurrentExecutables** auf 3 festlegen, können alle drei Datenflusstasks gleichzeitig ausgeführt werden. Stellen Sie sich jedoch vor, dass jeder Datenflusstask über 10 Quelle-zu-Ziel-Ausführungsstrukturen verfügt. Wenn Sie **MaxConcurrentExecutables** auf 3 festlegen, wird nicht sichergestellt, dass die Ausführungsstrukturen innerhalb jedes Datenflusstasks parallel ausgeführt werden.  
  
#### <a name="the-enginethreads-property"></a>Die EngineThreads-Eigenschaft  
 Die **EngineThreads** -Eigenschaft ist eine Eigenschaft, die jeder Datenflusstask besitzt. Diese Eigenschaft definiert, wie viele Threads das Datenflussmodul erstellen und parallel ausführen kann. Die **EngineThreads** -Eigenschaft ist gleichermaßen für die Quellthreads, die das Datenflussmodul für Quellen erstellt, und für die Arbeitsthreads, die das Modul für Transformationen und Ziele erstellt, anwendbar. Durch das Festlegen von **EngineThreads** auf 10 kann das Modul bis zu zehn Quellthreads und bis zu zehn Arbeitsthreads erstellen.  
  
 Stellen Sie sich das Beispielpaket mit drei Datenflusstasks vor, um zu verstehen, wie diese Eigenschaft funktioniert. Jeder Datenflusstask enthält zehn Quelle-zu-Ziel-Ausführungsstrukturen. Wenn Sie die EngineThreads-Eigenschaft in jedem Datenflusstask auf 10 festlegen, können alle 30 Ausführungsstrukturen gleichzeitig ausgeführt werden.  
  
> [!NOTE]  
>  Eine Erläuterung von Threading würde den Rahmen dieses Themas sprengen. Als allgemeine Regel gilt jedoch, dass nie mehr Threads parallel ausgeführt werden sollten, als Prozessoren verfügbar sind. Wenn mehr Threads ausgeführt werden, als Prozessoren zur Verfügung stehen, kann dies durch häufige Kontextwechsel zwischen den Threads die Leistung beeinträchtigen.  
  
## <a name="configuring-individual-data-flow-components"></a>Konfigurieren von einzelnen Datenflusskomponenten  
 Es gibt einige allgemeine Richtlinien, die Sie befolgen können, um die Leistung einzelner Datenflusskomponenten durch Konfiguration zu erhöhen. Es gibt auch spezielle Richtlinien für jeden Typ von Datenflusskomponente: Quelle, Transformation und Ziel.  
  
### <a name="general-guidelines"></a>Allgemeine Richtlinien  
 Es gibt zwei allgemeine Richtlinien, die von der Datenflusskomponente unabhängig sind, die Sie befolgen sollten, um die Leistung zu erhöhen: Optimieren Sie Abfragen, und vermeiden Sie unnötige Zeichenfolgen.  
  
#### <a name="optimize-queries"></a>Optimieren von Abfragen  
 Zahlreiche Datenflusskomponenten verwenden Abfragen beim Extrahieren von Daten aus Quellen oder bei Suchvorgängen zum Erstellen von Verweistabellen. Die Standardabfrage verwendet die Syntax SELECT * FROM \<Tabellenname>. Bei diesem Abfragetyp werden alle Spalten in der Quelltabelle zurückgegeben. Wenn alle Spalten zur Entwurfszeit zur Verfügung stehen, ist es möglich, eine beliebige Spalte als Such-, Pass-Through- oder Quellspalte auszuwählen. Nachdem Sie die zu verwendenden Spalten ausgewählt haben, sollten Sie die Abfrage so ändern, dass sie nur diese ausgewählten Spalten enthält. Das Entfernen überflüssiger Spalten macht den Datenfluss in einem Paket effizienter, da durch weniger Spalten eine kleinere Zeile erstellt wird. Je kleiner eine Zeile ist, desto mehr Zeilen passen in einen Puffer und desto geringer ist der Aufwand für die Verarbeitung aller Zeilen im Dataset.  
  
 Wenn Sie eine Abfrage erstellen möchten, können Sie die Abfrage eingeben oder den Abfrage-Generator verwenden.  
  
> [!NOTE]  
>  Wenn Sie ein Paket in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]ausführen, werden auf der Registerkarte Status des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers Warnungen aufgelistet. Diese Warnungen umfassen die Identifizierung jeglicher Datenspalten, die dem Datenfluss von einer Quelle zur Verfügung gestellt werden, jedoch dann nicht von Downstream-Datenflusskomponenten verwendet werden. Sie können die **RunInOptimizedMode** -Eigenschaft verwenden, um diese Spalten automatisch zu entfernen.  
  
#### <a name="avoid-unnecessary-sorting"></a>Vermeiden unnötiger Sortierungen  
 Die Sortierung ist generell ein langsamer Vorgang. Durch Vermeiden unnötiger Sortierungen kann die Leistung des Paketdatenflusses verbessert werden.  
  
 Manchmal sind die Quelldaten bereits sortiert, bevor sie von einer Downstreamkomponente verwendet werden. Eine solche Vorsortierung kann auftreten, wenn die SELECT-Abfrage eine ORDER BY-Klausel verwendet hat oder wenn die Daten in sortierter Reihenfolge in die Quelle eingefügt wurden. Für solche vorsortierten Quelldaten können Sie einen Hinweis angeben, dass die Daten sortiert sind, und so die Verwendung einer Transformation zum Sortieren vermeiden, die anderenfalls zum Erfüllen der Sortieranforderungen von bestimmten Downstream-Transformationen erforderlich wäre. (Beispielsweise erfordern die Transformationen für Zusammenführen und Zusammenführungsjoin sortierte Eingaben.) Wenn Sie einen Hinweis geben möchten, dass die Daten sortiert sind, müssen Sie die folgenden Aufgaben ausführen:  
  
-   Legen Sie die **IsSorted** -Eigenschaft auf der Ausgabe einer Upstreamdatenfluss-Komponente auf **True**fest.  
  
-   Geben Sie die Sortierschlüsselspalten an, in denen die Daten sortiert werden.  
  
 Weitere Informationen finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Wenn die Daten im Datenfluss sortiert werden müssen, können Sie die Leistung verbessern, indem Sie den Datenfluss so entwerfen, dass so wenig Sortiervorgänge wie möglich verwendet werden. Beispielsweise verwendet der Datenfluss eine Multicasttransformation, um das Dataset zu kopieren. Sortieren Sie das Dataset einmal, bevor die Multicasttransformation ausgeführt wird, anstatt mehrere Ausgaben nach der Transformation zu sortieren.  
  
 Weitere Informationen finden Sie unter [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md), [Merge Transformation](../../integration-services/data-flow/transformations/merge-transformation.md), [Merge Join Transformation](../../integration-services/data-flow/transformations/merge-join-transformation.md)und [Multicast Transformation](../../integration-services/data-flow/transformations/multicast-transformation.md).  
  
### <a name="sources"></a>Quellen  
  
#### <a name="ole-db-source"></a>OLE DB-Quelle  
 Wenn Sie eine OLE DB-Quelle verwenden, um Daten aus einer Sicht abzurufen, wählen Sie "SQL-Befehl" als Datenzugriffsmodus aus, und geben Sie eine SELECT-Anweisung ein. Der Zugriff auf Daten mit einer SELECT-Anweisung bietet eine bessere Leistung als die Auswahl von "Tabelle oder Sicht" als Datenzugriffsmodus.  
  
### <a name="transformations"></a>Transformationen  
 Verbessern Sie mithilfe der Vorschläge in diesem Abschnitt die Leistung der Transformation für das Aggregieren, für Fuzzysuche, Fuzzygruppierung, Suche, Zusammenführungsjoin und für langsam veränderliche Dimensionen.  
  
#### <a name="aggregate-transformation"></a>Transformation für das Aggregieren  
 Die Transformation für das Aggregieren enthält die **Keys**-, die **KeysScale**-, die **CountDistinctKeys**- und die **CountDistinctScale** -Eigenschaften. Diese Eigenschaften dienen einer verbesserten Leistung, indem es der Transformation ermöglicht wird, den zum Zwischenspeichern von Daten benötigten Speicher zuzuordnen. Wenn Sie die genaue oder ungefähre Anzahl von Gruppen kennen, die als Ergebnis eines **Group by** -Vorgangs erwartet werden, legen Sie die **Keys** -Eigenschaft bzw. die **KeysScale** -Eigenschaft fest. Wenn Sie die genaue oder ungefähre Anzahl der unterschiedlichen Werte kennen, die als Ergebnis eines **Distinct count** -Vorgangs erwartet werden, legen Sie die **CountDistinctKeys** -Eigenschaft bzw. die **CountDistinctScale** -Eigenschaft fest.  
  
 Wenn Sie in einem Datenfluss mehrere Aggregationen erstellen müssen, sollten Sie diese mit einer einzigen Transformation für das Aggregieren erstellen, anstatt mehrere Transformationen zu verwenden. Durch diesen Ansatz wird die Leistung verbessert, wenn eine Aggregation eine Untergruppe einer anderen Aggregation ist, da die Transformation den internen Speicher optimieren kann und die Eingangsdaten nur einmal durchsuchen muss. Wenn eine Aggregation z. B. eine GROUP BY-Klausel und eine AVG-Aggregation verwendet, kann die Leistung dadurch verbessert werden, dass sie in eine Transformation kombiniert werden. Das Ausführen mehrerer Aggregationen innerhalb einer Transformation für das Aggregieren serialisiert jedoch die Aggregationsvorgänge und verbessert daher möglicherweise nicht die Leistung, wenn mehrere Aggregationen unabhängig voneinander berechnet werden müssen.  
  
#### <a name="fuzzy-lookup-and-fuzzy-grouping-transformations"></a>Transformationen für Fuzzysuche und Fuzzygruppierung  
 Informationen zur Leistungsoptimierung der Transformationen für die Fuzzysuche und Fuzzygruppierung finden Sie im Whitepaper [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604)(in Englisch).  
  
#### <a name="lookup-transformation"></a>Transformation für Suche  
 Minimieren Sie die Größe der Verweisdaten im Speicher, indem Sie eine SELECT-Anweisung eingeben, die nur die von Ihnen benötigten Spalten durchsucht. Diese Option bietet eine bessere Leistung als die Auswahl einer gesamten Tabelle oder Sicht, wodurch eine große Menge an unnötigen Daten zurückgegeben wird.  
  
#### <a name="merge-join-transformation"></a>Merge Join Transformation  
 Der Wert der **MaxBuffersPerInput** -Eigenschaft muss nicht mehr konfiguriert werden, da Microsoft Änderungen vorgenommen hat, die das Risiko einer übermäßigen Arbeitsspeicherbelegung bei der Transformation für Zusammenführungsjoins reduzieren. Dieses Problem trat in einigen Fällen auf, wenn durch die Eingaben des Zusammenführungsjoins unregelmäßige Daten erzeugt wurden.  
  
#### <a name="slowly-changing-dimension-transformation"></a>Transformation für langsam veränderliche Dimensionen  
 Der Assistent für langsam veränderliche Dimensionen und die Transformation für langsam veränderliche Dimensionen sind universell einsetzbare Tools, die die Anforderungen der meisten Benutzer erfüllen. Der vom Assistenten generierte Datenfluss ist jedoch nicht leistungsoptimiert.  
  
 In der Regel sind die langsamsten Komponenten in der Transformation für langsam veränderliche Dimensionen die Transformationen für OLE DB-Befehl, die UPDATEs für jeweils eine Zeile ausführen. Daher ist die effizienteste Methode zur Verbesserung der Leistung der Transformation für langsam veränderliche Dimensionen das Ersetzen der Transformationen für OLE DB-Befehl. Sie können diese Transformationen durch Zielkomponenten ersetzen, die alle zu aktualisierenden Zeilen in eine Stagingtabelle speichern. Sie können dann einen Task "SQL ausführen" hinzufügen, der für alle Zeilen gleichzeitig ein einzelnes setbasiertes Transact-SQL-UPDATE ausführt.  
  
 Fortgeschrittene Benutzer können für die Verarbeitung von langsam veränderlichen Dimensionen einen benutzerdefinierten Datenfluss entwerfen, der für große Dimensionen optimiert ist. Eine Erläuterung und ein Beispiel dieses Ansatzes finden Sie im Abschnitt "Unique dimension scenario" im Whitepaper [Project REAL: Business Intelligence ETL Design Practices](http://go.microsoft.com/fwlink/?LinkId=96602)(in Englisch).  
  
### <a name="destinations"></a>Ziele  
 Wenn Sie die Leistung von Zielen erhöhen möchten, sollten Sie ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ziel verwenden und die Leistung des Ziels testen.  
  
#### <a name="sql-server-destination"></a>SQL Server-Ziel  
 Wenn ein Paket Daten in eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf demselben Computer lädt, verwenden Sie ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ziel. Dieses Ziel ist für schnelles Massenladen optimiert.  
  
#### <a name="testing-the-performance-of-destinations"></a>Testen der Leistung von Zielen  
 Möglicherweise nimmt das Speichern von Daten in Zielen mehr Zeit als erwartet in Anspruch. Um herauszufinden, ob dies darauf zurückzuführen ist, dass das Ziel die Daten nicht schnell genug verarbeiten kann, können Sie das Ziel vorübergehend durch eine Transformation für Zeilenanzahl ersetzen. Sollte sich der Durchsatz wesentlich verbessern, ist wahrscheinlich das Ziel, das die Daten lädt, Ursache für die langsamere Verarbeitung.  
  
### <a name="review-the-information-on-the-progress-tab"></a>Überprüfen der Informationen auf der Registerkarte Status  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer werden zusätzliche Informationen zur Ablaufsteuerung und zum Datenfluss beim Ausführen von Paketen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Auf der Registerkarte **Status** werden Tasks und Container in der Ausführungsreihenfolge aufgeführt. Diese Registerkarte enthält außerdem die Start- und Beendigungszeiten, Warnungen und Fehlermeldungen für jeden Task, Container sowie das Paket selbst. Sie enthält außerdem eine nach Ausführungsreihenfolge sortierte Liste der Datenflusskomponenten, Angaben zum Fortschritt in Prozent sowie die Anzahl der verarbeiteten Zeilen.  
  
 Zum Aktivieren bzw. Deaktivieren der Anzeige von Meldungen auf der Registerkarte **Status** schalten Sie die Option **Debug-Statusbericht** im Menü **SSIS** um. Beim Ausführen eines komplexen Pakets in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]kann eine Deaktivierung der Statusberichterstellung zur Verbesserung der Leistung beitragen.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 **Artikel und Blogbeiträge**  
  
-   Technischer Artikel [SQL Server 2005 Integration Services: Eine Leistungsstrategie](http://go.microsoft.com/fwlink/?LinkId=98899)auf technet.microsoft.com  
  
-   Technischer Artikel [Integration Services: Leistungsoptimierungstechniken](http://go.microsoft.com/fwlink/?LinkId=98900)auf technet.microsoft.com  
  
-   Technischer Artikel [Erhöhen des Durchsatzes von Pipelines durch Aufteilen synchroner Transformationen in mehrere Tasks](http://sqlcat.com/technicalnotes/archive/2010/08/18/increasing-throughput-of-pipelines-by-splitting-synchronous-transformations-into-multiple-tasks.aspx)auf sqlcat.com  
  
-   Technischer Artikel [The Data Loading Performance Guide (Leistungsleitfaden für das Laden von Daten)](http://go.microsoft.com/fwlink/?LinkId=220816)auf msdn.microsoft.com  
  
-   Technischer Artikel mit [Empfehlungen zum schnellen Laden großer Datenmengen (1 TB in 30 Minuten)](http://go.microsoft.com/fwlink/?LinkId=220817)auf msdn.microsoft.com  
  
-   Technischer Artikel mit den [Top 10-Empfehlungen für SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkId=220818)auf sqlcat.com  
  
-   Technischer Artikel und Beispiel zum [ausgeglichenen Datenverteiler für SSIS](http://go.microsoft.com/fwlink/?LinkId=220822)auf sqlcat.com  
  
-   Blogbeitrag [Beheben von Leistungsproblemen bei SSIS-Paketen](http://go.microsoft.com/fwlink/?LinkId=238156)auf blogs.msdn.com  
  
 **Videos**  
  
-   Videoserie zum [Entwerfen und Optimieren der Leistung von SSIS-Paketen im Unternehmen (SQL-Videoserie)](http://go.microsoft.com/fwlink/?LinkId=400878)  
  
-   Video [Tuning Your SSIS Package Data Flow in the Enterprise (SQL Server Video)](http://technet.microsoft.com/sqlserver/ff686901.aspx)(Optimieren des SSIS-Paketdatenflusses im Unternehmen) auf technet.microsoft.com  
  
-   Video [Understanding SSIS Data Flow Buffers (SQL Server Video)](http://technet.microsoft.com/sqlserver/ff686905.aspx)(Grundlegendes zu SSIS-Datenflusspuffern) auf technet.microsoft.com  
  
-   Video [Leistungsentwurfsmuster zu Microsoft SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkID=233698&clcid=0x409)auf channel9.msdn.com  
  
-   Präsentation zur [Nutzung der Verbesserungen am SQL Server 2008 SSIS-Datenflussmodul bei Microsoft IT](http://go.microsoft.com/fwlink/?LinkId=217660)auf sqlcat.com  
  
-   Video [Ausgeglichener Datenverteiler](http://go.microsoft.com/fwlink/?LinkID=226278&clcid=0x409)auf technet.microsoft.com  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Tools zur Problembehandlung für die Paketentwicklung](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Behandlung von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
