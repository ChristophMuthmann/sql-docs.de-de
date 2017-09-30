---
title: "Verwendungsszenarios für den Abfragespeicher | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Query Store, usage scenarios
ms.assetid: f5309285-ce93-472c-944b-9014dc8f001d
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 231a1a6204c9010ec5c4895b7cb7506d3b4159ff
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="query-store-usage-scenarios"></a>Verwendungsszenarien für den Abfragespeicher
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Der Abfragespeicher kann in einer großen Bandbreite von Szenarien eingesetzt werden, wenn das Nachverfolgen und Sicherstellen einer vorhersagbaren Arbeitsleistung entscheidend ist. Diese Beispiele dienen zur Veranschaulichung:  
  
-   Bestimmen und Reparieren von Abfragen mit Planauswahlregression  
  
-   Erkennen und Optimieren der Abfragen mit dem höchsten Ressourcenverbrauch  
  
-   A/B-Tests  
  
-   Aufrechterhalten einer stabilen Leistung während des Upgrades auf das neuere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Erkennen und Verbessern von Ad-hoc-Arbeitsauslastungen  
  
## <a name="pinpoint-and-fix-queries-with-plan-choice-regressions"></a>Bestimmen und Reparieren von Abfragen mit Planauswahlregression  
 Im Rahmen der normalen Abfrageausführung kann der Abfrageoptimierer die Entscheidung für einen anderen Plan treffen, da sich wichtige Eingangsparameter geändert haben: die Datenkardinalität hat sich geändert, es wurden Indizes erstellt, geändert oder gelöscht, Statistikinformationen wurden aktualisiert usw.  Meistens funktioniert der neu gewählte Plan besser oder in etwa gleich gut wie der zuvor verwendete. Es gibt jedoch Fälle, in denen der neue Plan deutlich schlechter funktioniert – diese Situation wird als Planauswahl-Änderungsregression bezeichnet. Vor der Einführung des Abfragespeichers war das ein sehr schwer zu erkennendes und behebendes Problem, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keinen integrierten Datenspeicher bereitstellte, in dem Benutzer nach Ausführungsplänen suchen konnten, die im Lauf der Zeit verwendet worden waren.  
  
 Mit dem Abfragespeicher lassen sich diese Aufgaben schnell lösen:  
  
-   Identifizieren aller Abfragen, deren Ausführungsmetrik im interessierenden Zeitraum (letzte Stunde, letzter Tag, letzte Woche usw.) heruntergestuft wurde. Verwendung von **Zurückgestellten Abfragen** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zum Beschleunigen der Analyse.  
  
-   Unter den zurückgestellten Abfragen lassen sich leicht diejenigen identifizieren, die mehrere Pläne aufwiesen und aufgrund schlechter Planauswahl heruntergestuft wurden. Verwenden Sie den Bereich **Planzusammenfassung** in **Zurückgestellte Abfragen** , um alle Pläne für eine zurückgestellte Abfrage und ihre Abfrageleistung im zeitlichen Verlauf darzustellen.  
  
-   Setzen Sie die Verwendung des im Verlauf vorhergehenden Plans durch, wenn der sich als besser erwiesen hat. Verwenden Sie die Schaltfläche **Plan erzwingen** in **Zurückgestellte Abfragen**, um die Verwendung des ausgewählten Plans für die Abfrage durchzusetzen.  
  
 ![Abfrage-Store-Nutzung-1](../../relational-databases/performance/media/query-store-usage-1.png "query-store-usage-1")  
  
 Eine detaillierte Beschreibung des Szenarios finden Sie im Blog [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/) (Abfragespeicher: Ein Flugdatenschreiber für Ihre Datenbank).  
  
## <a name="identify-and-tune-top-resource-consuming-queries"></a>Erkennen und Optimieren der Abfragen mit dem höchsten Ressourcenverbrauch  
 Zwar können im Rahmen Ihrer Arbeitsauslastung Tausende Abfragen generiert werden, normalerweise verwendet jedoch nur eine Handvoll den größten Teil der Systemressourcen und erfordert daher Ihre Aufmerksamkeit. Unter den Abfragen mit dem größten Ressourcenverbrauch finden sich üblicherweise zurückgestellte Abfragen oder solche, die mit weiterer Optimierung verbessert werden können.  
  
 Die Untersuchung lässt sich am einfachsten durch Öffnen von **Abfragen mit dem höchsten Ressourcenverbrauch** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]beginnen. Die Benutzeroberfläche ist in drei Bereiche unterteilt: Ein Histogramm, das die Abfragen mit dem höchsten Ressourcenverbrauch darstellt (links), eine Planzusammenfassung für die ausgewählte Abfrage (rechts) und eine visuellen Abfrageplan für den ausgewählten Plan (unten). Klicken Sie auf die Schaltfläche **Konfigurieren** , um die Anzahl der zu analysierenden Abfragen und das untersuchte Zeitintervall zu steuern. Darüber hinaus können Sie unter verschiedenen Dimensionen des Ressourcenverbrauchs (Dauer, CPU, Arbeitsspeicher, E/A, Anzahl der Ausführungen) und der Baseline (Mittel, Min, Max, Summe, Standardabweichung) wählen.  
  
 ![Abfrage-Store-Nutzung-2](../../relational-databases/performance/media/query-store-usage-2.png "query-store-usage-2")  
  
 Betrachten Sie die Planzusammenfassung auf der rechten Seite, um den Ausführungsverlauf zu analysieren und sich über die verschiedenen Pläne und ihre Laufzeitstatistik zu informieren. Verwenden Sie den unteren Bereich, um die verschiedenen Pläne zu untersuchen oder sie nebeneinander visuell zu vergleichen (mithilfe der Schaltfläche „Vergleichen“).  
  
 Wenn Sie eine Abfrage mit nicht optimaler Leistung identifiziert haben, richtet sich das weitere Vorgehen nach der Art des Problems:  
  
1.  Wenn die Abfrage mit mehreren Plänen ausgeführt wurde und der letzte Plan signifikant schlechter ist als der vorherige, können Sie den Planerzwingungsmechanismus verwenden, um sicherzustellen, dass bei zukünftigen Ausführungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] immer der optimale Plan verwendet wird.  
  
2.  Überprüfen Sie, ob der Optimierer Hinweise auf fehlende Indizes im XML-Plan gibt. Wenn das der Fall ist, erstellen Sie den fehlenden Index, und verwenden Sie den Abfragespeicher, um die Abfrageleistung nach erfolgter Indexerstellung zu bewerten  
  
3.  Vergewissern Sie sich, dass die Statistikinformationen für die von der Abfrage verwendeten zugrundeliegenden Tabellen auf dem aktuellen Stand sind.  
  
4.  Überprüfen Sie, ob die von der Abfrage verwendeten Indizes defragmentiert sind.  
  
5.  Ziehen Sie bei aufwändigen Abfragen eine Neuerstellung in Erwägung. Nutzen Sie beispielsweise die Vorteile der Abfrageparametrisierung, und verringern Sie den Einsatz von dynamischem SQL. Implementieren Sie nach dem Lesen der Daten die optimale Logik (führen Sie Datenfilterung auf der Datenbankseite statt auf der Anwendungsseite aus).  
  
## <a name="ab-testing"></a>A/B-Tests  
 Verwenden Sie den Abfragespeicher, um die Arbeitsleistung vor und nach der beabsichtigten Änderung der Anwendung zu vergleichen. Die folgende Liste enthält eine Reihe von Beispielen, für die der Abfragespeicher eingesetzt werden kann, um den Einfluss der Umgebungs- oder Anwendungsänderung auf die Arbeitsleistung zu beurteilen:  
  
-   Einführen einer neuen Anwendungsversion.  
  
-   Hinzufügen neuer Hardware auf dem Server.  
  
-   Erstellen von fehlenden Indizes für Tabellen, auf die aufwändige Abfragen verweisen.  
  
-   Anwenden einer Filterrichtlinie für Sicherheit auf Zeilenebene. Weitere Details finden Sie unter [Optimizing Row Level Security with Query Store](http://blogs.msdn.com/b/sqlsecurity/archive/2015/07/21/optimizing-rls-performance-with-the-query-store.aspx)(Optimieren von Sicherheit auf Zeilenebene mithilfe des Abfragespeichers).  
  
-   Hinzufügen von temporaler Verwaltung durch das System zu Tabellen, die häufigen Änderungen durch OLTP-Anwendungen unterliegen.  
  
 Wenden Sie für jedes dieser Szenarien den folgenden Arbeitsablauf an:  
  
1.  Führen Sie Ihre Arbeitsauslastung mit dem Abfragespeicher vor der geplanten Änderung aus, um die Basislinie für die Leistung zu erstellen.  
  
2.  Wenden Sie die Anwendungsänderung zum vorgesehen Zeitpunkt an.  
  
3.  Führen Sie die Arbeitsauslastung danach für einen ausreichend langen Zeitraum aus, um ein Leistungsbild des Systems nach der Änderung zu erstellen  
  
4.  Vergleichen Sie die Ergebnisse von Nr. 1 und Nr. 3.  
  
    1.  Öffnen Sie **Datenbank Gesamtverbrauch**, um den Einfluss auf die gesamte Datenbank zu bestimmen.  
  
    2.  Öffnen Sie **Abfragen mit dem höchsten Ressourcenverbrauch** (oder Ihre eigene Analyse mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)]), um den Einfluss der Änderung auf die wichtigsten Abfragen zu analysieren.  
  
5.  Entscheiden Sie, ob die Änderung beibehalten oder ein Rollback für den Fall ausgeführt werden soll, dass die neue Leistung nicht akzeptabel ist.  
  
 In der folgenden Abbildung ist die Abfragespeicheranalyse (Schritt 4) im Fall eines fehlenden, nicht erstellten Index dargestellt. Öffnen Sie den **Bereich Abfragen mit dem höchsten Ressourcenverbrauch** /Planzusammenfassung, um diese Ansicht für die Abfrage zu erstellen, auf die sich die Indexerstellung auswirken soll:  
  
 ![Abfrage-Store-Nutzung-3](../../relational-databases/performance/media/query-store-usage-3.png "query-store-usage-3")  
  
 Darüber hinaus können Sie Pläne vor und nach der Indexerstellung vergleichen, indem Sie sie nebeneinander anzeigen. (Symbolleistenoption „Vergleichen Sie die Pläne für die ausgewählte Abfrage in einem separaten Fenster“, die auf der Symbolleiste mit einem roten Quadrat gekennzeichnet ist.)  
  
 ![Abfrage-Store-Nutzung-4](../../relational-databases/performance/media/query-store-usage-4.png "query-store-usage-4")  
  
 Der Plan (plan_id = 1, oben) enthält vor der Indexerstellung einen Hinweis auf einen fehlenden Index, und Sie können durch die Untersuchung bestätigen, dass „Clustered Index Scan“ der Operator mit dem höchsten Ressourcenverbrauch in der Abfrage war (rotes Rechteck).  
  
 Der Plan verwendet nach der Erstellung des fehlenden Index (plan_id = 15, unten ) jetzt „Index Seek (Nonclustered)“, wodurch sich der Gesamtaufwand der Abfrage verringert und die Leistung verbessert (grünes Rechteck).  
  
 Auf der Grundlage der Analyse ist wohl wahrscheinlich, dass Sie den Index beibehalten möchten, da sich die Abfrageleistung verbessert hat.  
  
## <a name="CEUpgrade"></a> Aufrechterhalten einer stabilen Leistung während des Upgrades auf das neuere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Vor [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]waren Benutzer dem Risiko einer nachlassenden Leistung während des Upgrades auf die neueste Plattformversion ausgesetzt. Der Grund liegt darin, dass die neueste Version des Abfrageoptimierers sofort aktiviert wurde, sobald neue Teile installiert wurden.  
  
 Seit [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] sind alle Änderungen des Abfrageoptimierers an den neuesten [Datenbank-Kompatibilitätsgrad](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) gebunden, sodass Pläne nicht sofort im Moment des Upgrades geändert werden, sondern erst, wenn ein Benutzer `COMPATIBILITY_LEVEL` auf die neuste Version aktualisiert. Diese Möglichkeit gibt Ihnen in Kombination mit dem Abfragespeicher ein großes Maß an Kontrolle über die Abfrageleistung im Upgradeprozess. Der empfohlene Upgradeworkflow ist in der folgenden Abbildung dargestellt:  
  
 ![Abfrage-Store-Nutzung-5](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  
  
1.  Upgrade von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ohne den Datenbankkompatibilitätsgrad zu ändern Dadurch werden nicht die neuesten Änderungen des Abfrageoptimierer verfügbar gemacht. Gleichzeitig bietet es aber neuere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen, wie z.B. den Abfragespeicher.  
  
2.  Aktivieren des Abfragespeichers Weitere Informationen zu diesem Thema finden Sie unter [Keep Query Store adjusted to your workload (Dauerhafte Abfragespeicheranpassung an Ihre Arbeitsauslastung)](../../relational-databases/performance/best-practice-with-the-query-store.md#Configure).

3.  Erlauben Sie es dem Abfragespeicher, Abfragen und Pläne abzufangen, und legen Sie eine Baseline der Leistung mit dem Kompatibilitätsgrad der Quelle oder der vorherigen Datenbank fest. Bleiben Sie ausreichend lang in diesem Schritt, um alle Pläne zu erfassen und eine stabile Baseline zu erstellen. Dabei kann es sich um die Dauer eines üblichen Geschäftszyklus für eine Produktionsworkload handeln.  
  
4.  Umstieg auf den neuesten Datenbankkompatibilitätsgrad: Machen Sie die neuesten Änderungen des Abfrageoptimierers für Ihre Arbeitsauslastung verfügbar, und lassen Sie ihn der Möglichkeit nach neue Pläne erstellen.  
  
5.  Verwenden Sie den Abfragespeicher für die Analyse und Reparaturen mithilfe zurückgestellter Abfragen: Im Allgemeinen sollten die neuen Änderungen des Abfrageoptimierers bessere Pläne erzeugen. Jedoch verfügen Sie in Form des Abfragespeichers über eine einfache Möglichkeit, Planauswahlregressionen durchzuführen und falsche Entscheidungen mithilfe des Mechanismus zum Durchsetzen von Plänen zu korrigieren.  
  
## <a name="identify-and-improve-ad-hoc-workloads"></a>Erkennen und Verbessern von Ad-hoc-Arbeitsauslastungen  
 Einige Arbeitsauslastungen weisen keine dominierenden Abfragen auf, die sich optimieren lassen, um die Gesamtleistung der Anwendung zu verbessern. Diese Workloads zeichnen sich normalerweise durch eine relativ große Anzahl verschiedener Abfragen aus, von denen jede einen Teil der Systemressourcen beansprucht. Aufgrund ihrer Einzigartigkeit werden solche Abfragen nur sehr selten ausgeführt (normalerweise nur einmal, daher die Bezeichnung „ad-hoc“), daher ist ihr Ressourcenverbrauch zur Laufzeit nicht kritisch. Da andererseits die Anwendung unterm Strich ständig neue Abfragen generiert, wird ein erheblicher Teil der Systemressourcen für die Kompilierung von Abfragen aufgewendet, was nicht optimal ist. Das ist auch für den Abfragespeicher keine ideale Situation, da die große Anzahl an Abfragen und Plänen den vorgesehenen Speicherplatz schnell erschöpft und der Abfragespeicher so sehr bald in den schreibgeschützten Modus versetzt werden muss. Wenn Sie die **Richtlinie zur größenbasierten Bereinigung** ([dringend empfohlen](best-practice-with-the-query-store.md) , um den Abfragespeicher stets betriebsbereit zu halten) aktiviert haben, bereinigen Hintergrundprozesse während des größten Teils der Zeit die Strukturen des Abfragespeichers, was ebenfalls in erheblichem Maß Systemressourcen verbraucht.  
  
 Die Ansicht**Abfragen mit höchstem Ressourcenverbrauch** gibt Ihnen einen ersten Hinweis auf die Ad-hoc-Natur Ihrer Arbeitsauslastung:  
  
 ![Abfrage-Store-Nutzung-6](../../relational-databases/performance/media/query-store-usage-6.png "query-store-usage-6")  
  
 Verwenden Sie die Metrik **Ausführungsanzahl** , um zu analysieren, ob Ihre Abfragen mit dem höchsten Ressourcenverbrauch Ad-hoc-Abfragen sind (dafür müssen Sie den Abfragespeicher mit `QUERY_CAPTURE_MODE = ALL`ausführen). Im Diagramm oben können Sie sehen, dass 90% der **Abfragen mit höchstem Ressourcenverbrauch** nur einmal ausgeführt werden.  
  
 Alternativ können Sie ein [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript ausführen, um die Gesamtzahl der Abfragetexte, Abfragen und Pläne im System abzurufen und ihre Verschiedenheit durch den Vergleich ihres query_hash- und plan_hash-Werts zu bestimmen:  
  
```tsql  
/*Do cardinality analysis when suspect on ad-hoc workloads*/  
SELECT COUNT(*) AS CountQueryTextRows FROM sys.query_store_query_text;  
SELECT COUNT(*) AS CountQueryRows FROM sys.query_store_query;  
SELECT COUNT(DISTINCT query_hash) AS CountDifferentQueryRows FROM  sys.query_store_query;  
SELECT COUNT(*) AS CountPlanRows FROM sys.query_store_plan;  
SELECT COUNT(DISTINCT query_plan_hash) AS  CountDifferentPlanRows FROM  sys.query_store_plan;  
```  
  
 Dies ist ein potenzielles Ergebnis, das Sie bei Arbeitsauslastungen mit Ad-hoc-Abfragen erhalten können:  
  
 ![Abfrage-Store-Nutzung-7](../../relational-databases/performance/media/query-store-usage-7.png "query-store-usage-7")  
  
 Das Abfrageergebnis zeigt, dass trotz der großen Anzahl an Abfragen und Plänen im Abfragespeicher sich deren query_hash und plan_hash tatsächlich nicht unterscheiden. Das Verhältnis zwischen eindeutigen Abfragetexten und eindeutigem query_hash liegt erheblich über 1, und das ist ein Hinweis, dass die Arbeitsauslastung einen geeigneten Kandidaten für Parametrisierung darstellt, da der einzige Unterschied zwischen den Abfragen eine literale Konstante (Parameter) ist, die als Teil des Abfragetexts übergeben wird.  
  
 Normalerweise tritt diese Situation ein, wenn Ihre Anwendung Abfragen erstellt (statt gespeicherte Prozeduren oder parametrisierte Abfragen aufzurufen) oder auf objektrelationalen Zuordnungsframeworks basiert, die standardmäßig Abfragen generieren.  
  
 Wenn der Anwendungscode in Ihre Zuständigkeit fällt, können Sie eine Neuerstellung der Datenzugriffsschicht in Erwägung ziehen, um gespeicherte Prozeduren oder parametrisierte Abfragen zu verwenden. Diese Situation lässt sich aber auch ohne Änderung der Anwendung erheblich verbessern, indem die Abfrageparametrisierung für die gesamte Datenbank (alle Abfragen) oder für die individuellen Abfragevorlagen mit dem gleichen Abfragehash durchgesetzt wird.  
  
 Der Ansatz mit einzelnen Abfragevorlagen erfordert die Erstellung von Planhinweislisten:  
  
```tsql  
/*Apply plan guide for the selected query template*/  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'<your query text goes here>',  
    @stmt OUTPUT,   
    @params OUTPUT;  
  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION (PARAMETERIZATION FORCED)';  
```  
  
 Die Lösung mit Planhinweislisten ist genauer, erfordert aber mehr Arbeit.  
  
 Wenn alle Ihre Abfragen (oder eine Mehrheit davon) Kandidaten für automatische Parametrisierung sind, stellt das Ändern von `FORCED PARAMETERIZATION` für die gesamte Datenbank möglicherweise die bessere Option dar:  
  
```tsql  
/*Apply forced parameterization for entire database*/  
ALTER DATABASE <database name> SET PARAMETERIZATION  FORCED;  
```  

 > [!NOTE]
 > Weitere Informationen zu diesem Thema finden Sie unter [Richtlinien für die Verwendung der erzwungenen Parametrisierung](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide).

 Nach dem Ausführen eines dieser Schritte zeichnet **Abfragen mit höchstem Ressourcenverbrauch** ein anderes Bild Ihrer Arbeitsauslastung.  
  
 ![Abfrage-Store-Verwendung – 8](../../relational-databases/performance/media/query-store-usage-8.png "query-store-usage-8")  
  
 In manchen Fällen generiert Ihre Anwendung möglicherweise viele verschiedene Abfragen, die keine geeigneten Kandidaten für automatische Parametrisierung darstellen. In diesem Fall findet sich eine große Anzahl Abfragen im System, das Verhältnis zwischen eindeutigen Abfragen und eindeutigem Abfragehash `query_hash` liegt aber wahrscheinlich nahe bei 1.  
  
 In diesem Fall kann es sinnvoll sein die Serveroption [**Für Ad-Hoc-Workloads optimieren**](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) zu aktivieren, um die Verschwendung von Cachespeicher für Abfragen zu vermeiden, die wahrscheinlich nicht mehr ausgeführt werden. Um die Erfassung solcher Abfragen im Abfragespeicher zu verhindern, legen Sie `QUERY_CAPTURE_MODE` auf `AUTO`fest.  
  
```tsql  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
  
sp_configure 'optimize for ad hoc workloads', 1;  
GO  
RECONFIGURE;  
GO  
  
ALTER DATABASE  [QueryStoreTest] SET QUERY_STORE CLEAR;  
ALTER DATABASE  [QueryStoreTest] SET QUERY_STORE = ON   
    (OPERATION_MODE = READ_WRITE, QUERY_CAPTURE_MODE = AUTO);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Leistung mit dem Abfragespeicher](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [Bewährte Methoden für den Abfragespeicher](../../relational-databases/performance/best-practice-with-the-query-store.md)  
  
  

