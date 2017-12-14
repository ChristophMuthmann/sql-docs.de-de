---
title: "Bewährte Methoden für den Abfragespeicher | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Query Store, best practices
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8692566abced072b25d931a9b133c0fb7cd7f51d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="best-practice-with-the-query-store"></a>Bewährte Methoden für den Abfragespeicher
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In diesem Thema werden die bewährten Methoden für den Einsatz eines Abfragespeichers bei Ihrer Arbeitsauslastung vorgestellt.  
  
##  <a name="SSMS"></a> Verwenden des neuesten [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verfügt über mehrere Benutzeroberflächen, die zum Konfigurieren des Abfragespeichers sowie zur Nutzung der gesammelten Daten über Ihre Arbeitsauslastung konzipiert wurden.  
Laden Sie die neueste Version von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] [hier](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) herunter.  
  
 Eine kurze Beschreibung zur Verwendung des Abfragespeichers bei Fehlerbehebungen finden Sie auf den [@AzureBlogs zu Abfragespeichern](https://azure.microsoft.com/en-us/blog/query-store-a-flight-data-recorder-for-your-database/).  
  
##  <a name="Insight"></a> Verwenden von Query Performance Insight in Azure SQL-Datenbank  
 Wenn Sie Abfragespeicher in [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ausführen, können Sie mit **Query Performance Insight** den DTU-Verbrauch im Verlauf der Zeit analysieren.  
Sie können zwar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] verwenden, um detaillierte Ressourcenverbrauchswerte für alle Ihre Abfragen abzurufen (CPU, Arbeitsspeicher, E/A usw.), Query Performance Insight bietet Ihnen jedoch eine schnelle und effiziente Möglichkeit, um deren Auswirkung auf den DTU-Verbrauch Ihrer Datenbank insgesamt zu ermitteln.  
Weitere Informationen finden Sie unter [Query Performance Insight für Azure SQL-Datenbank](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/).    

##  <a name="using-query-store-with-elastic-pool-databases"></a>Verwenden von Abfragespeicher mit elastischen Pooldatenbanken
Sie können den Abfragespeicher bedenkenlos in allen Datenbanken verwenden, selbst in dicht gepackten Pools. Alle mit übermäßiger Ressourcennutzung zusammenhängenden Probleme, die bei der Aktivierung des Abfragespeichers für die große Anzahl Datenbanken in elastischen Pools auftreten konnten, wurden behoben.

##  <a name="Configure"></a> Dauerhafte Abfragespeicheranpassung an Ihre Arbeitsauslastung  
 Konfigurieren Sie Abfragespeicher basierend auf den Anforderungen hinsichtlich der Arbeitsauslastung und der Behandlung von Leistungsproblemen.   
Die Standardparameter sind gut für einen schnellen Einstieg geeignet; Sie sollten jedoch das Verhalten von Abfragespeicher im Verlauf der Zeit überwachen und die Konfiguration entsprechend anpassen:  
  
 ![abfrage-speicher-eigenschaften](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")  
  
 Hier sind einige Richtlinien zum Festlegen der Parameterwerte:  
  
 **Maximale Größe (MB):** Gibt den Grenzwert für den Datenbereich an, den Abfragespeicher innerhalb der Datenbank einnimmt.  Dies ist die wichtigste Einstellung, die sich direkt auf den Betriebsmodus des Abfragespeichers auswirkt.  
  
 Während der Abfragespeicher Abfragen, Ausführungspläne und Statistiken sammelt, wächst die Datenbank an, bis dieser Grenzwert erreicht ist. In diesem Fall ändert der Abfragespeicher automatisch den Betriebsmodus in schreibgeschützt und beendet die Erfassung von neuen Daten, sodass die Leistungsanalyse nicht mehr korrekt ist.  
  
 Der Standardwert (100 MB) reicht möglicherweise nicht aus, wenn die Arbeitsauslastung eine große Anzahl unterschiedlicher Abfragen und Pläne generiert oder wenn der Abfrageverlauf einen längeren Zeitraum aufbewahrt werden soll. Verfolgen Sie den aktuellen Speicherplatz und erhöhen Sie die maximale Größe (MB), um zu verhindern, dass der Abfragespeicher in den schreibgeschützten Modus übergeht.  Verwenden Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , oder führen Sie das folgende Skript aus, um aktuelle Informationen zur Größe des Abfragespeichers zu erhalten:  
  
```tsql 
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason  
FROM sys.database_query_store_options;  
```  
  
 Im folgenden Skript wird eine neue maximale Größe (MB) festgelegt:  
  
```tsql  
ALTER DATABASE [QueryStoreDB]  
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);  
```  
  
 **Statistiksammlungsintervall:** Definiert den Grad der Granularität während der gesammelten Laufzeitstatistik (der Standardwert ist 1 Stunde). Ziehen Sie einen niedrigeren Wert in Betracht, wenn Sie eine geringere Granularität oder weniger Zeit benötigen, um Probleme zu erkennen und zu mindern. Denken Sie jedoch daran, dass dies unmittelbar die Größe der Abfragespeicherdaten beeinflusst. Verwenden Sie SSMS oder Transact-SQL, um einen anderen Wert für das Statistiksammlungsintervall festzulegen:  
  
```tsql  
ALTER DATABASE [QueryStoreDB] SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 60);  
```  
  
 **Schwellenwert für veraltete Abfrage (Tage):** Zeitbasierte Cleanuprichtlinie, die die Aufbewahrungsdauer für persistente Laufzeitstatistiken und inaktive Abfragen steuert.  
Standardmäßig ist der Abfragespeicher so konfiguriert, dass Daten 30 Tage lang gespeichert werden. Dies ist möglicherweise für Ihr Szenario unnötig lange.  
  
 Vermeiden Sie es, Verlaufsdaten aufzubewahren, die Sie nicht mehr verwenden möchten. Dies reduziert die Wahrscheinlichkeit für Änderungen in den schreibgeschützten Status. Die Größe der Abfragespeicherdaten sowie die Zeit, um Probleme zu erkennen und zu mindern, lassen sich besser vorhersagen. Verwenden Sie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oder das folgende Skript, um die zeitbasierte Cleanuprichtlinie zu konfigurieren:  
  
```tsql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 90));  
```  
  
 **Größenbasierter Bereinigungsmodus:** Gibt an, ob das automatische Cleanup ausgeführt wird, wenn der Umfang der Abfragespeicherdaten den Grenzwert erreicht.  
  
 Es wird dringend empfohlen, das größenbasierte Cleanup zu aktivieren, um sicherzustellen, dass der Abfragespeicher immer im Lese-/ Schreibmodus ausgeführt wird und die neuesten Daten erfasst.  
  
```tsql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);  
```  
  
 **Erfassungsmodus für den Abfragespeicher:** Gibt die Abfrageerfassungsrichtlinie für den Abfragespeicher an.  
  
-   **All** : Erfasst alle Abfragen. Diese Option ist die Standardeinstellung.  
  
-   **Auto** : Seltenere Abfragen und Abfragen mit unbedeutender Kompilierungs- und Ausführungsdauer werden ignoriert. Die Schwellenwerte für die Dauer der Ausführungsanzahl, Kompilierung und Laufzeit werden intern bestimmt.  
  
-   **None** : Der Abfragespeicher beendet die Erfassung neuer Abfragen.  
  
 Das folgende Skript legt den Abfrageerfassungsmodus auf Auto fest:  
  
```tsql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="how-to-start-with-query-performance-troubleshooting"></a>So beginnen Sie mit der Behandlung von Leistungsproblemen  
 Der Problembehandlungsworkflow mit Abfragespeicher ist einfach, wie im folgenden Diagramm dargestellt:  
  
 ![abfrage-speicher-problembehandlung](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")  
  
 Aktivieren Sie Abfragespeicher mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , wie im vorherigen Abschnitt beschrieben, oder führen Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung aus:  
  
```tsql  
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;  
```  
  
 Es dauert einige Zeit, bis Abfragespeicher das Dataset erfasst, das Ihre Arbeitsauslastung präzise darstellt. In der Regel reicht ein Tag, selbst bei sehr komplexen Arbeitsauslastungen. Sie können jedoch unmittelbar nach Aktivierung der Funktion damit beginnen, die Daten zu untersuchen und Abfragen zu identifizieren, die Ihre Aufmerksamkeit erfordern.   
Navigieren Sie zu dem Abfragespeicher-Unterordner unter dem Datenbankknoten im Objekt-Explorer von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , um Problembehandlungsansichten für bestimmte Szenarien zu öffnen.   
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] -Abfragespeicheransichten arbeiten mit dem Satz von Ausführungsmetriken, die alle als eine der folgenden Statistikfunktionen ausgedrückt werden:  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version|Ausführungsmetrik|Statistikfunktion|  
|----------------------|----------------------|------------------------|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|CPU-Zeit, Dauer, Ausführungsanzahl, logische Lesevorgänge, logische Schreibvorgänge, Speicherverbrauch, physische Lesevorgänge, CLR-Zeit, Parallelitätsgrad (Degree of Parallelism DOP) und Zeilenanzahl|Durchschnitt, Maximum, Minimum, Standardabweichung, Gesamt|
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|CPU-Zeit, Dauer, Ausführungsanzahl, logische Lesevorgänge, logische Schreibvorgänge, Speicherverbrauch, physische Lesevorgänge, CLR-Zeit, Parallelitätsgrad (Degree of Parallelism, DOP), Zeilenanzahl, Protokollspeicher, TempDB-Speicher und Wartezeiten|Durchschnitt, Maximum, Minimum, Standardabweichung, Gesamt|
  
 Die folgende Grafik veranschaulicht, wie Sie die Abfragespeicheransichten suchen:  
  
 ![abfrage-speicher-ansicht](../../relational-databases/performance/media/query-store-views.png "query-store-views")  
  
 In der folgenden Tabelle wird erläutert, wann Sie die einzelnen Abfragespeicheransichten verwenden sollten:  
  
|SSMS-Ansicht|Szenario|  
|---------------|--------------|  
|Rückläufige Abfragen|Identifizieren von Abfragen, bei denen die Ausführungsmetriken vor kurzem rückläufig waren (d. h. sich verschlechtert haben). <br />Verwenden Sie diese Ansicht, um beobachtete Leistungsprobleme in Ihrer Anwendung mit den tatsächlichen Abfragen zu korrelieren, die korrigiert oder verbessert werden müssen.|  
|Gesamter Ressourcenverbrauch|Analysieren Sie den Gesamtressourcenverbrauch für die Datenbank für eine der Ausführungsmetriken.<br />Verwenden Sie diese Ansicht, um Ressourcenmuster zu identifizieren (tägliche im Vergleich zu nächtlichen Arbeitsauslastungen), und optimieren Sie den Gesamtverbrauch für Ihre Datenbank.|  
|Abfragen mit höchstem Ressourcenverbrauch|Wählen Sie die gewünschte Ausführungsmetrik, und identifizieren Sie Abfragen mit den extremsten Werten für ein angegebenes Zeitintervall. <br />Verwenden Sie diese Ansicht, um Ihre Aufmerksamkeit auf die relevantesten Abfragen zu konzentrieren, die die größte Auswirkung auf den Ressourcenverbrauch der Datenbank haben.|  
|Abfragen mit erzwungenen Plänen|Zeigt vorherige erzwungene Pläne durch Verwendung des Abfragespeichers an. <br />Verwenden Sie diese Ansicht, um schnell auf alle aktuell erzwungenen Pläne zuzugreifen.|  
|Abfragen mit hoher Variation|Analysieren Sie Abfragen mit hoher Ausführungsvariation in Verbindung mit allen verfügbaren Dimensionen wie Dauer, CPU-Zeit, E/A und Speicherauslastung im gewünschten Zeitintervall.<br />Verwenden Sie diese Ansicht, um Abfragen mit stark abweichender Leistung zu identifizieren, die die Benutzerfreundlichkeit in Ihren Anwendungen beeinträchtigen können.|  
|Nachverfolgte Abfragen|Verfolgen Sie die Ausführung der wichtigsten Abfragen in Echtzeit. In der Regel verwenden Sie diese Ansicht, wenn Sie über Abfragen mit erzwungenen Plänen verfügen und Sie sicherstellen möchten, dass die Abfrageleistung stabil ist.|
  
> [!TIP]  
>  Eine ausführliche Beschreibung dazu, wie Sie mit [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] die Abfragen mit dem größten Ressourcenverbrauch identifizieren und diejenigen Abfragen korrigieren können, die aufgrund der Änderung der Planauswahl zurückgestellt wurden, finden Sie unter [Query Store @Azure Blogs](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).  
  
 Wenn Sie eine Abfrage mit nicht optimaler Leistung identifiziert haben, richtet sich das weitere Vorgehen nach der Art des Problems.  
  
-   Wenn die Abfrage mit mehreren Plänen ausgeführt wurde und der letzte Plan signifikant schlechter ist als der vorherige, können Sie den Planerzwingungsmechanismus verwenden, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] so zu konfigurieren, dass bei zukünftiger Ausführung immer der optimale Plan verwendet wird.  
  
     ![abfrage-speicher-erzwingungs-plan](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")  

> [!NOTE]  
> Die Abbildung oben kann verschiedene Formen für bestimmte Abfragepläne aufweisen, wobei die möglichen Status folgende Bedeutungen haben:<br />  
> |Form|Bedeutung|  
> |-------------------|-------------|
> |Circle|Abfrage abgeschlossen (reguläre Ausführung erfolgreich abgeschlossen)|
> |Square|Abgebrochen (vom Client initiierter Abbruch der Ausführung)|
> |Triangle|Fehlgeschlagen (durch abgebrochene Ausführung ausgelöste Ausnahme)|
> Darüber hinaus gibt die Größe der Form Aufschluss über die Anzahl von Abfrageausführungen innerhalb des angegebenen Zeitintervalls. Die Größe der Form nimmt mit zunehmender Anzahl von Ausführungen zu.  

-   Sie können daraus schließen, dass der Abfrage ein Index für optimale Ausführung fehlt. Diese Informationen werden innerhalb des Abfrageausführungsplans eingeblendet. Erstellen Sie den fehlenden Index, und überprüfen Sie die Abfrageleistung mit dem Abfragespeicher.  
  
     ![abfrage-speicher-anzeige-plan](../../relational-databases/performance/media/query-store-show-plan.png "abfrage-speicher-anzeige-plan")  
  
     Wenn Sie Ihre Arbeitsauslastung auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)]ausführen, registrieren Sie sich für den [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Indexratgeber, um automatisch Indexempfehlungen zu erhalten.  
  
-   In einigen Fällen können Sie eine statistische Neukompilierung erzwingen, wenn Sie feststellen, dass der Unterschied zwischen der geschätzten und der tatsächlichen Anzahl der Zeilen im Ausführungsplan maßgeblich ist.  
  
-   Schreiben Sie problematische Abfragen um, beispielsweise, um die Vorteile der Abfrageparametrisierung nutzen zu können oder um eine bessere Logik zu implementieren.  
  
##  <a name="Verify"></a> Überprüfen, ob der Abfragespeicher kontinuierlich Abfragedaten erfasst  
 Der Abfragespeicher kann den Betriebsmodus automatisch ändern. Überwachen Sie regelmäßig den Status des Abfragespeichers, um sicherzustellen, dass der Abfragespeicher funktioniert, und um Maßnahmen zu ergreifen, um Ausfälle aufgrund von vermeidbaren Ursachen zu verhindern. Führen Sie die folgende Abfrage aus, um den Betriebsmodus zu ermitteln und die wichtigsten Parameter anzuzeigen:  
  
```tsql
USE [QueryStoreDB];  
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 Der Unterschied zwischen `actual_state_desc` und `desired_state_desc` weist darauf hin, dass automatisch eine Änderung des Betriebsmodus aufgetreten ist. Die häufigste Änderung besteht darin, dass der Abfragespeicher im Hintergrund in den schreibgeschützten Modus wechselt. In sehr seltenen Fällen kann der Abfragespeicher den Fehlerstatus aufgrund von internen Fehlern annehmen.  
  
 Wenn der tatsächliche Status schreibgeschützt ist, verwenden Sie die **readonly_reason** -Spalte, um die Ursache zu ermitteln. In der Regel werden Sie feststellen, dass der Abfragespeicher in den schreibgeschützten Modus gewechselt hat, da das Kontingent überschritten wurde. In diesem Fall wird **readonly_reason** auf 65536 festgelegt. Andere Gründe finden Sie unter [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).  
  
 Ziehen Sie die folgenden Schritte in Betracht, um den Abfragespeicher in den schreibgeschützten Modus zu schalten und die Datensammlung zu aktivieren:  
  
-   Erhöhen Sie die maximale Speichergröße mithilfe der **MAX_STORAGE_SIZE_MB** -Option von **ALTER DATABASE**.  
  
-   Bereinigen Sie die Abfragespeicherdaten mithilfe der folgenden Anweisung:  
  
    ```tsql  
    ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;  
    ```  
  
Wenden Sie einen oder beide der folgenden Schritte an, indem Sie die folgende Anweisung ausführen, die den Betriebsmodus explizit wieder in den Lese-/ Schreibzugriff zurücksetzt:  
  
```tsql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);  
```  
  
 Gehen Sie proaktiv folgendermaßen vor:  
  
-   Sie können die automatischen Änderungen des Betriebsmodus durch Anwenden bewährter Methoden verhindern. Wenn Sie sicherstellen, dass die Abfragespeichergröße immer unterhalb des maximal zulässigen Werts ist, sinkt die Wahrscheinlichkeit des Übergangs in den schreibgeschützten Modus maßgeblich. Aktivieren Sie die größenbasierte Richtlinie, wie im Abschnitt zum [Konfigurieren von Abfragespeicher](#Configure) beschrieben, sodass der Abfragespeicher die Daten automatisch bereinigt, wenn sich die Größe dem Grenzwert nähert.  
  
-   Um sicherzustellen, dass die aktuellsten Daten beibehalten werden, konfigurieren Sie die zeitbasierte Richtlinie, um regelmäßig veraltete Informationen zu entfernen.  
  
-   Nicht zuletzt sollten Sie es in Betracht ziehen, den Abfrageerfassungsmodus auf Auto einzustellen, da dadurch Abfragen herausgefiltert werden, die in der Regel weniger relevant für Ihre Arbeitsauslastung sind.  
  
### <a name="error-state"></a>Fehlerzustand  
 Zum Wiederherstellen des Abfragespeichers versuchen Sie explizit den Lese-/Schreibmodus einzustellen, und prüfen Sie den tatsächlichen Status erneut.  
  
```tsql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
 Wenn das Problem weiterhin besteht, bedeutet dies, dass die beschädigten Abfragespeicherdaten auf dem Datenträger beibehalten werden.
 
 Der Abfragedatenspeicher konnte durch die Ausführung der gespeicherten Prozedur **sp_query_store_consistency_check** innerhalb der betroffenen Datenbank wiederhergestellt werden.
 
 Falls dieser Schritt nicht erfolgreich war, versuchen Sie, den Abfragespeicher zu löschen, bevor Sie den Lese-/Schreibmodus anfordern.  
  
```tsql  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE CLEAR;  
GO  
  
ALTER DATABASE [QueryStoreDB]   
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);    
GO  
  
SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,   
    max_storage_size_mb, readonly_reason, interval_length_minutes,   
    stale_query_threshold_days, size_based_cleanup_mode_desc,   
    query_capture_mode_desc  
FROM sys.database_query_store_options;  
```  
  
## <a name="set-the-optimal-query-capture-mode"></a>Festlegen des optimalen Abfrageerfassungsmodus  
 Behalten Sie die relevantesten Daten im Abfragespeicher. Die folgende Tabelle beschreibt die typischen Szenarios für jeden Abfrageerfassungsmodus:  
  
|Abfrageerfassungsmodus|Szenario|  
|------------------------|--------------|  
|All|Analysieren Sie Ihre Arbeitsauslastung sorgfältig im Hinblick auf alle Abfrageformen und deren Ausführungshäufigkeit und andere Statistiken.<br /><br /> Identifizieren Sie neue Abfragen in Ihrer Arbeitsauslastung.<br /><br /> Ermitteln Sie, ob Ad-hoc-Abfragen verwendet werden, um Chancen auf eine Benutzerparametrisierung oder eine automatische Parametrisierung zu identifizieren.|  
|Auto|Konzentrieren Sie sich auf relevante und handlungsbedürftige Abfragen, sprich auf jene Abfragen, die regelmäßig ausgeführt werden oder einen erheblichen Ressourcenverbrauch aufweisen.|  
|None|Sie haben bereits den Abfragesatz erfasst, den Sie in Laufzeit überwachen möchten, und möchten nun Ablenkungen beseitigen, die durch andere Abfragen entstehen können.<br /><br /> „Keine“ ist für Testzwecke geeignet sowie für Benchmarking-Umgebungen.<br /><br /> „Keine“ eignet sich auch für Softwareanbieter, die bei Auslieferung die Abfragespeicherkonfiguration so festlegen, dass die Anwendungsauslastung überwacht wird.<br /><br /> „Keine“ sollte mit Bedacht verwendet werden, da Sie womöglich die Chance verpassen, wichtige neue Abfragen nachzuverfolgen und zu optimieren. Vermeiden Sie den Einsatz von „Keine“, es sei denn es ist für ein bestimmtes Szenario erforderlich.|  
  
## <a name="keep-the-most-relevant-data-in-query-store"></a>Aufbewahren der relevantesten Daten im Abfragespeicher  
 Konfigurieren Sie den Abfragespeicher so, dass nur die relevanten Daten enthalten sind. Dann wird es kontinuierlich ausgeführt, was ein überragendes Problembehandlungserlebnis bietet bei minimalen Auswirkungen auf die normale Arbeitsauslastung.  
Die folgende Tabelle enthält bewährte Methoden:  
  
|Bewährte Methoden|Einstellung|  
|-------------------|-------------|  
|Begrenzen der Menge von beibehaltenen Verlaufsdaten.|Konfigurieren Sie die zeitbasierte Richtlinie, um das automatische Cleanup zu aktivieren.|  
|Herausfiltern von nicht relevanten Abfragen.|Konfigurieren Sie den Abfrageerfassungsmodus als Auto.|  
|Löschen von weniger relevanten Abfragen, wenn die maximale Größe erreicht ist.|Aktivieren Sie die größenbasierte Cleanuprichtlinie.|  
  
##  <a name="Parameterize"></a> Vermeiden des Einsatzes von nicht parametrisierten Abfragen  
 Der Einsatz von nicht parametrisierten Abfragen, wenn diese nicht unbedingt erforderlich sind (z.B. bei Ad-hoc-Analysen), wird nicht empfohlen.  Zwischengespeicherte Pläne können nicht wiederverwendet werden, sodass der Abfrageoptimierer gezwungen ist, Abfragen für jeden eindeutigen Abfragetext zu kompilieren. Weitere Informationen zu diesem Thema finden Sie unter [Richtlinien für die Verwendung der erzwungenen Parametrisierung](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide).  
  Abfragespeicher kann darüber hinaus schnell die Kontingentgröße aufgrund einer potenziell großen Anzahl von verschiedenen Abfragetexten und somit einer großen Anzahl von verschiedenen Ausführungsplänen mit ähnlicher Form überschreiten.  
Daher wird die Leistung Ihrer Arbeitsauslastung suboptimal sein, und der Abfragespeicher wechselt möglicherweise in den schreibgeschützten Modus oder löscht kontinuierlich die Daten, um mit den eingehenden Abfragen Schritt zu halten.  
  
 Ziehen Sie die folgenden Optionen in Betracht:  

  -   Parametrisieren Sie Abfragen, sofern möglich, indem Sie z.B. Abfragen innerhalb einer gespeicherten Prozedur oder sp_executesql umschließen. Weitere Informationen zu diesem Thema finden Sie unter [Parameter und Wiederverwendung von Ausführungsplänen](../../relational-databases/query-processing-architecture-guide.md#PlanReuse).    
  
-   Verwenden Sie die Option [**Für Ad-hoc-Arbeitsauslastungen optimieren**](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md), wenn Ihre Arbeitsauslastung viele einmalige Ad-hoc-Batches mit anderen Abfrageplänen enthält.  
  
    -   Vergleichen Sie die Anzahl der unterschiedlichen query_hash-Werte mit der Gesamtanzahl von Einträgen in sys.query_store_query. Ist das Verhältnis nahe 1, generiert Ihre Ad-hoc-Arbeitsauslastung verschiedene Abfragen.  
  
-   Wenden Sie die[**erzwungene Parametrisierung**](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) auf die Datenbank oder auf eine Teilmenge der Abfragen an, wenn die Anzahl der unterschiedlichen Abfragepläne nicht groß ist.  
  
    -   Verwenden Sie die [Planhinweisliste](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md), um die Parametrisierung nur für die ausgewählte Abfrage zu erzwingen.  
  
    -   Konfigurieren Sie die erzwungene Parametrisierung wie die Verwendung des Befehls der [Datenbankoption „Parametrization“](../../relational-databases/databases/database-properties-options-page.md#miscellaneous), sofern es eine kleine Anzahl verschiedener Abfragepläne in Ihrer Arbeitsauslastung gibt: wenn das Verhältnis zwischen der Anzahl unterschiedlicher query_hash und die Gesamtzahl der Einträge in sys.query_store_query viel weniger als 1 it.  
  
-   Legen Sie den **Abfrageerfassungsmodus** auf AUTO fest, um Ad-hoc-Abfragen mit geringem Ressourcenverbrauch automatisch herauszufiltern.  
  
##  <a name="Drop"></a> Vermeiden des DROP- und CREATE-Musters beim Verwalten von enthaltenen Objekten für Abfragen  
 Der Abfragespeicher ordnet einen Abfrageeintrag einem enthaltenen Objekt zu (gespeicherte Prozedur, Funktion und Trigger).  Wenn Sie ein enthaltenes Objekt neu erstellen, wird ein neuer Abfrageeintrag für den gleichen Abfragetext generiert. Dies verhindert die Nachverfolgung der Leistungsstatistiken für diese Abfrage im Verlauf der Zeit und diesen Nutzungsplanerzwingungsmechanismus. Um dies zu vermeiden, verwenden Sie den `ALTER <object>` -Prozess, um die Definition des enthaltenen Objekts nach Möglichkeit zu ändern.  
  
##  <a name="CheckForced"></a> Regelmäßiges Überprüfen des Status der erzwungenen Pläne  

 Die Planerzwingung ist ein nützlicher Mechanismus zur Behandlung von Leistungsproblemen für kritische Abfragen, um sie besser vorhersagbar zu machen. Wie bei Planhinweisen und Planhinweislisten ist das Erzwingen eines Plans jedoch keine Garantie dafür, dass er in späteren Ausführungen verwendet wird. Wenn das Datenbankschema sich derart ändert, dass Objekte, auf die der Ausführungsplan verweist, geändert oder gelöscht werden, beginnt das Erzwingen eines Plans in der Regel zu scheitern. In diesem Fall greift [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf eine Neukompilierung der Abfrage zurück, während die tatsächliche Ursache für den Fehler beim Erzwingen in [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) eingeblendet wird. Die folgende Abfrage gibt Informationen zu erzwungenen Plänen zurück:  
  
```tsql  
USE [QueryStoreDB];  
GO  
  
SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,  
    force_failure_count, last_force_failure_reason_desc  
FROM sys.query_store_plan AS p  
JOIN sys.query_store_query AS q on p.query_id = q.query_id  
WHERE is_forced_plan = 1;  
```  
  
 Eine vollständige Liste der Gründe finden Sie unter [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). Sie können auch das **query_store_plan_forcing_failed** -XEvent verwenden, um Fehler bei der Problembehandlung der Planerzwingung nachzuverfolgen.  
  
##  <a name="Renaming"></a> Vermeiden der Umbenennung von Datenbanken bei Abfragen mit erzwungenen Plänen  

 Ausführungspläne verweisen auf Objekte mithilfe von dreiteiligen Namen `database.schema.object`.   

Wenn Sie eine Datenbank umbenennen, wird das Erzwingen eines Plans fehlschlagen, wodurch bei allen nachfolgenden Abfrageausführungen eine Neukompilierung durchgeführt wird.  

##  <a name="Recovery"></a> Verwenden von Ablaufverfolgungsflags für unternehmenswichtige Server zur effizienteren Notfallwiederherstellung
 
  Die globalen Ablaufverfolgungsflags 7745 und 7752 können zur Leistungsoptimierung des Abfragespeichers in HADR-Szenarios verwendet werden. Weitere Informationen hierzu finden Sie unter [Ablaufverfolgungsflags](../..//t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
  
  Das Ablaufverfolgungsflag 7745 verhindert, dass der Abfragespeicher standardmäßig Daten auf den Datenträger schreibt, bevor SQL Server beendet werden kann.
  
  Das Ablaufverfolgungsflag 7752 ermöglicht das asynchrone Laden eines Abfragespeichers und erlaubt SQL Server die Ausführung von Abfragen, bevor der Abfragespeicher vollständig geladen wurde. Der Abfragespeicher verhindert standardmäßig, dass Abfragen ausgeführt werden, bevor der Abfragespeicher wiederhergestellt wurde.

## <a name="see-also"></a>Siehe auch  
 [Katalogsichten des Abfragespeichers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Gespeicherte Prozeduren für den Abfragespeicher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [Verwenden des Abfragespeichers mit In-Memory-OLTP](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)   
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [Handbuch zur Architektur der Abfrageverarbeitung](../../relational-databases/query-processing-architecture-guide.md)  
  
