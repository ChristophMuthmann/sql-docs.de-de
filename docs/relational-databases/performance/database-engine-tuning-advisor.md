---
title: Datenbankoptimierungsratgeber | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dta.general.f1
ms.assetid: 50dd0a0b-a407-4aeb-bc8b-b02a793aa30a
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4f0b031b0c98dd9f7708aebd13984f22403f3de1
ms.lasthandoff: 04/11/2017

---
# <a name="database-engine-tuning-advisor"></a>Datenbankoptimierungsratgeber
  Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Datenbankoptimierungsratgeber (DTA) analysiert Datenbanken und gibt Empfehlungen zum Optimieren der Abfrageleistung. Mit dem Datenbankoptimierungsratgeber können Sie einen optimalen Satz von Indizes, indizierten Sichten oder Tabellenpartitionen auswählen und erstellen, auch wenn Sie nicht über detaillierte Kenntnisse bezüglich der Datenbankstruktur oder der internen Mechanismen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verfügen. Mit dem DTA können Sie die folgenden Aufgaben ausführen:  
  
-   Beheben der Leistungsprobleme einer bestimmten Problemabfrage  
  
-   Optimieren eines großen Satzes von Abfragen auf mehreren Datenbanken  
  
-   Ausführen einer explorativen Was-wäre-wenn-Analyse der potenziellen Änderungen des physischen Entwurfs  
  
-   Verwalten des Speicherplatzes  
  
## <a name="database-engine-tuning-advisor-benefits"></a>Vorteile des Datenbankoptimierungsratgebers:  
 Die Optimierung der Abfrageleistung kann sich ohne umfassende Kenntnisse bzgl. der Datenbankstruktur und der für die Datenbank ausgeführten Abfragen schwierig gestalten. Der Datenbankoptimierungsratgeber kann diese Aufgabe durch Analysieren des aktuellen Abfrageplancache oder einer Arbeitsauslastung der erstellten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfragen und Empfehlen eines entsprechenden physischen Entwurfs erleichtern. Für erfahrenere Datenbankadministratoren stellt DTA einen leistungsstarken Mechanismus zum Ausführen explorativer Was-wäre-wenn-Analysen verschiedener Alternativen physischer Entwürfe bereit. Der DTA kann die folgenden Informationen bereitstellen:  
  
-   Empfehlen der besten Mischung aus Rowstore- und [Columnstore](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)-Indizes für Datenbanken mithilfe des Abfrageoptimierers zur Analyse von Abfragen in einer Arbeitsauslastung.  
  
-   Empfehlen von ausgerichteten oder nicht ausgerichteten Partitionen für Datenbanken, auf die in einer Arbeitsauslastung verwiesen wird.  
  
-   Empfehlen von indizierten Sichten für Datenbanken, auf die in einer Arbeitsauslastung verwiesen wird.  
  
-   Analysieren der Auswirkungen vorgeschlagener Änderungen, einschließlich Indexverwendung, Verteilung von Abfragen auf Tabellen und Leistung von Abfragen in der Arbeitsauslastung.  
  
-   Empfehlen von Verfahren zur Optimierung der Datenbank für eine kleine Gruppe problematischer Abfragen.  
  
-   Ermöglichen der Anpassung der Empfehlungen durch die Angabe weiterer Optionen, wie z. B. Datenträgereinschränkungen.  
  
-   Bereitstellen von Berichten, in denen die Auswirkungen der Implementierung von Empfehlungen für eine bestimmte Arbeitsauslastung zusammengefasst sind.  

-   Berücksichtigen von Alternativen, bei denen Sie mögliche Entwurfsoptionen in Form von hypothetischen Konfigurationen liefern, die vom Datenbankoptimierungsratgeber bewertet werden sollen.

-  Optimieren von Arbeitsauslastungen aus einer Vielzahl von Quellen, wie SQL Server-Abfragespeicher, Plancache, SQL Server Profiler-Ablaufverfolgungsdatei oder -tabelle oder SQL-Datei.

  
 Der Datenbankoptimierungsratgeber ist für die folgenden Typen von Abfragearbeitsauslastungen ausgelegt:  
  
-   Nur OLTP-Abfragen (Online Transaction Processing, Onlinetransaktionsverarbeitung)  
  
-   Nur OLAP-Abfragen (Online Analytical Processing, analytische Onlineverarbeitung)  
  
-   Gemischte OLTP- und OLAP-Abfragen  
  
-   Abfrageintensive Arbeitsauslastungen (mehr Abfragen als Datenänderungen)  
  
-   Updateintensive Arbeitsauslastungen (mehr Datenänderungen als Abfragen)  
  
## <a name="dta-components-and-concepts"></a>DTA-Komponenten und -Konzepte  
 Grafische Benutzeroberfläche des Datenbankoptimierungsratgebers  
 Eine benutzerfreundliche Schnittstelle, über die Sie die Arbeitsauslastung angeben und verschiedene Optimierungsoptionen aktivieren können.  
  
 **dta** -Hilfsprogramm  
 Die Befehlszeilenversion des Datenbankoptimierungsratgebers. Mit dem Hilfsprogramm **dta** soll es Ihnen ermöglicht werden, die Funktionalität des Datenbankoptimierungsratgebers in Anwendungen und Skripts zu verwenden.  
  
 Arbeitsauslastung  
 Eine Transact-SQL-Skriptdatei, Ablaufverfolgungsdatei oder Ablaufverfolgungstabelle, die eine repräsentative Arbeitsauslastung für die zu optimierenden Datenbanken enthält. Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie den Plancache als Arbeitsauslastung angeben.  Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] können Sie [den Abfragespeicher als Arbeitsauslastung angeben](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md). 
  
 XML-Eingabedatei  
 Eine Datei im XML-Format, mit der der Datenbankoptimierungsratgeber Arbeitsauslastungen optimieren kann. Die XML-Eingabedatei unterstützt erweiterte Optimierungsoptionen, die weder über die GUI noch im Hilfsprogramm **dta** verfügbar sind.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Für den Datenbankoptimierungsratgeber gelten die folgenden Einschränkungen:  
  
-   Er kann keine eindeutigen Indizes bzw. Indizes, die PRIMARY KEY- oder UNIQUE-Einschränkungen erzwingen, hinzufügen oder löschen.  
  
-   Er kann keine Datenbank analysieren, die auf den Einzelbenutzermodus festgelegt ist.  
  
-   Wenn der angegebene maximale Datenträgerspeicher für Optimierungsempfehlungen den tatsächlichen verfügbaren Speicherplatz überschreitet, verwendet der Datenbankoptimierungsratgeber den von Ihnen angegebenen Wert. Wenn Sie jedoch das Empfehlungsskript ausführen, um die Empfehlungen zu implementieren, erzeugt das Skript möglicherweise einen Fehler, wenn nicht vorher zusätzlicher Datenträgerspeicher hinzugefügt wird. Sie können den maximalen Datenträgerspeicher über die Option **-B** des **dta** -Hilfsprogramms angeben oder indem Sie einen Wert in das Dialogfeld **Erweiterte Optimierungsoptionen** eingeben.  
  
-   Aus Sicherheitsgründen kann der Datenbankoptimierungsratgeber eine Arbeitsauslastung in einer Ablaufverfolgungstabelle, die sich auf einem Remoteserver befindet, nicht optimieren. Zum Umgehen dieser Einschränkung können Sie eine Ablaufverfolgungsdatei anstelle einer Ablaufverfolgungstabelle verwenden oder die Ablaufverfolgungstabelle auf den Remoteserver kopieren.  
  
-   Wenn Sie Einschränkungen festlegen, indem Sie z.B. (über die Option **-B** oder das Dialogfeld **Erweiterte Optimierungsoptionen** ) den maximalen Datenträgerspeicher für Optimierungsempfehlungen angeben, ist der Datenbankoptimierungsratgeber u.U. gezwungen, bestimmte vorhandene Indizes zu löschen. In diesem Fall enthält die Empfehlung des Datenbankoptimierungsratgebers möglicherweise eine negative erwartete Verbesserung.  
  
-   Wenn Sie eine Einschränkung hinsichtlich der Optimierungszeit angeben (indem Sie die Option **-A** des **dta** -Hilfsprogramms verwenden oder das Kontrollkästchen **Optimierungszeit begrenzen** auf der Registerkarte **Optimierungsoptionen** aktivieren), überschreitet der Datenbankoptimierungsratgeber möglicherweise das Zeitlimit für eine akkurate erwartete Verbesserung, und die Analyse gibt einen Bericht für den bislang verarbeiteten Teil der Arbeitsauslastung aus.  
  
-   In den folgenden Situationen erstellt der Datenbankoptimierungsratgeber möglicherweise keine Empfehlungen:  
  
    1.  Die Tabelle, die optimiert werden soll, umfasst weniger als 10 Datenseiten.  
  
    2.  Die empfohlenen Indizes würden gegenüber dem aktuellen physischen Datenbankentwurf nicht genügend Verbesserungen bei der Abfrageleistung bieten.  
  
    3.  Der Benutzer, der den Datenbankoptimierungsratgeber ausführt, ist kein Mitglied der Datenbankrolle **db_owner** oder der festen Serverrolle **sysadmin** . Die Abfragen in der Arbeitsauslastung werden im Sicherheitskontext des Benutzers analysiert, der den Datenbankoptimierungsratgeber ausführt. Der Benutzer muss ein Mitglied der Datenbankrolle **db_owner** sein.  
  
-   Der Datenbankoptimierungsratgeber speichert Daten zu Optimierungssitzungen und andere Informationen in der **msdb** -Datenbank. Wenn an der **msdb** -Datenbank Änderungen vorgenommen werden, besteht das Risiko, dass Optimierungssitzungsdaten verloren gehen. Um dieses Risiko zu umgehen, müssen Sie für die **msdb** -Datenbank eine geeignete Sicherungsstrategie implementieren.  
  
## <a name="performance-considerations"></a>Leistungsaspekte  
 Der Datenbankmodul-Optimierungsratgeber kann bei der Analyse signifikante Prozessor- und Arbeitsspeicherressourcen belegen. Um zu vermeiden, dass die Leistung des Produktionsservers beeinträchtigt wird, wenden Sie eine der folgenden Strategien an:  
  
-   Optimieren Sie die Datenbanken, wenn der Server frei ist. Der Datenbankoptimierungsratgeber kann sich auf Wartungstasks auswirken.  
  
-   Verwenden Sie die Funktion für Testserver und Produktionsserver. Weitere Informationen finden Sie unter  [Reduzieren der Optimierungsauslastung des Produktionsservers](../../relational-databases/performance/reduce-the-production-server-tuning-load.md).  
  
-   Geben Sie nur die Strukturen für den physischen Datenbankentwurf an, die der Datenbankoptimierungsratgeber analysieren soll. Der Datenbankoptimierungsratgeber stellt zahlreiche Optionen zur Verfügung, gibt jedoch nur die wirklich erforderlichen an.  
  
## <a name="dependency-on-xpmsver-extended-stored-procedure"></a>Abhängigkeit von der erweiterten gespeicherten Prozedur xp_msver  
 Der Datenbankoptimierungsratgeber ist von der erweiterten gespeicherten Prozedur **xp_msver** abhängig, um vollständige Funktionalität bereitzustellen. Diese erweiterte gespeicherte Prozedur wird standardmäßig aktiviert. Der Datenbankoptimierungsratgeber verwendet diese erweiterte gespeicherte Prozedur, um die Anzahl der Prozessoren und den verfügbaren Speicher auf dem Computer abzurufen, auf dem sich die zu optimierende Datenbank befindet. Wenn **xp_msver** nicht verfügbar ist, übernimmt der Datenbankoptimierungsratgeber die Hardwaremerkmale des Computers, auf dem er ausgeführt wird. Wenn die Hardwaremerkmale des Computers, auf dem der Datenbankmodul-Optimierungsratgeber ausgeführt wird, nicht zur Verfügung stehen, geht der Ratgeber von einem Prozessor und 1024 MB (Megabyte) Speicher aus.  
  
 Diese Abhängigkeit hat Auswirkungen auf die Partitionierungsempfehlungen, da die Anzahl der empfohlenen Partitionen von diesen beiden Werten (Anzahl der Prozessoren und verfügbarer Speicher) abhängt. Diese Abhängigkeit hat auch Auswirkungen auf die Optimierungsergebnisse, wenn Sie einen Testserver verwenden, um Ihren Produktionsserver zu optimieren. In diesem Szenario verwendet der Datenbankoptimierungsratgeber **xp_msver** , um Hardwareeigenschaften vom Produktionsserver abzurufen. Nach dem Optimieren der Arbeitsauslastung auf dem Testserver verwendet der Datenbankoptimierungsratgeber diese Hardwareeigenschaften dazu, eine Empfehlung zu generieren. Weitere Informationen finden Sie unter [xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md).  
  
## <a name="database-engine-tuning-advisor-tasks"></a>Tasks des Datenbankoptimierungsratgebers  
 In der folgenden Tabelle sind allgemeine Datenbankoptimierungsratgeber-Aufgaben und die Themen aufgeführt, in denen sie beschrieben werden.  
  
|Datenbankoptimierungsratgeber-Aufgabe|Thema|  
|-----------------------------------------|-----------|  
|Initialisieren und Starten des Datenbankoptimierungsratgebers<br /><br /> Erstellen einer Arbeitsauslastung durch Angeben des Plancache, Erstellen eines Skripts oder Generieren einer Ablaufverfolgungsdatei oder Ablaufverfolgungstabelle<br /><br /> Optimieren einer Datenbank mithilfe der grafischen Benutzeroberfläche des Datenbankoptimierungsratgebers<br /><br /> Erstellen von XML-Eingabedateien zum Optimieren von Arbeitsauslastungen<br /><br /> Anzeigen von Beschreibungen für die Benutzeroberflächenoptionen des Datenbankoptimierungsratgebers|[Starten und Verwenden des Datenbankoptimierungsratgebers](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|Anzeigen der Ergebnisse des Datenbankoptimierungsvorgangs<br /><br /> Auswählen und Implementieren von Optimierungsempfehlungen<br /><br /> Durchführen einer Was-wäre-wenn-Analyse für die Arbeitsauslastung<br /><br /> Überprüfen vorhandener Optimierungssitzungen, Klonen von Sitzungen auf Grundlage vorhandener Sitzungen <br />oder Bearbeiten vorhandener Optimierungsempfehlungen zur weiteren Auswertung oder Implementierung<br /><br /> Anzeigen von Beschreibungen für die Benutzeroberflächenoptionen des Datenbankoptimierungsratgebers|[Anzeigen und Verwenden der Ausgabe des Datenbankoptimierungsratgebers](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)|  
  
  

