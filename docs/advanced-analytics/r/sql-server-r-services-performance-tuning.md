---
title: "Leistungsoptimierung für SQL Server R Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf6f3b7d-f9f9-4e45-b0d1-07850b53e0c5
caps.latest.revision: "20"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 536d493ba199ff4cdc808c5463cb260926f106f5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Optimieren der Leistung für R in SQL Server

In diesem Artikel wird die erste Aufgabe in einer Reihe von vier Artikeln, die zur leistungsoptimierung für R-Services, basierend auf zwei Fallstudien zu beschreiben:

- Leistungstests durchgeführt, die für das Produktentwicklungsteam So überprüfen Sie das Leistungsprofil von R-Lösungen

- Leistungsoptimierung durch das Microsoft Data Science-Team für eine bestimmte Machine Learning-Szenario von Kunden häufig angeforderte.

Das Ziel dieser Reihe ist, bieten eine Anleitung zu den Arten von leistungsoptimierungstechniken, die besonders hilfreich für die Ausführung von R-Aufträge in SQL Server sind.

+ Dieses (erste) Thema enthält eine Übersicht über die Architektur und einige allgemeine Probleme, bei der Optimierung für Data Science-Aufgaben.
+ Der zweite Artikel behandelt bestimmte Hardware- und SQL Server-Optimierungen.
+ Der dritte Artikel werden die Optimierungen in R-Code sowie Ressourcen für operationalisierung behandelt.
+ Der vierte Artikel beschreibt Testmethoden im Detail, und Berichte Ergebnisse und Schlussfolgerungen.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="performance-goals-and-targeted-scenarios"></a>Leistungsziele und Zielszenarien

Die R-Services-Funktion wurde in SQL Server 2016, um die Ausführung von R-Skripts unterstützen von SQL Server eingeführt. Wenn Sie diese Funktion verwenden, wird die R-Laufzeit arbeitet in einem separaten Prozess vom Datenbankmodul, aber tauscht Daten sicher mit dem Datenbankmodul mithilfe von Server-Ressourcen und Dienste, die Interaktion mit SQL Server, z. B. das vertrauenswürdige Launchpad.

In SQL Server 2017 wurde Unterstützung angekündigt, zum Ausführen von Python-Skripts verwenden die gleiche Architektur mit zusätzlichen Sprache, in Zukunft zu folgen.

Mit steigender Anzahl der unterstützten Versionen und Language ist es wichtig, dass der Datenbankadministrator und der datenbankarchitekt das Potenzial für Ressourcenkonflikte auf Machine Learning-Aufträge zur Kenntnis genommen haben und sie können für die Serverkonfiguration zur Unterstützung die neue Arbeitslasten. Obwohl unsichere datenbewegungen Analysen in der Nähe der Daten beibehalten eliminiert werden, wird auch analytische arbeitsauslastungen aus der Data Scientist und wieder auf dem Hostserver für die Daten Laptop verschoben.

Leistungsoptimierung für Machine Learning ist nicht eindeutig eine allgemeingültige nutzen. Die folgenden allgemeinen Aufgaben möglicherweise sehr unterschiedliche Leistungsprofile:

- Aufgaben zu trainieren: Erstellen und Trainieren ein Regressionsmodell im Vergleich zu trainieren eines neuronalen Netzwerks
- Feature Engineering mithilfe von R im Vergleich zu merkmalsextraktion mit T-SQL
- Auf einzelne Zeilen oder kleine Batches, Vergleich mit Bulk Bewertung mit tabellarischen Eingaben bewerten
- Bewertung in R und Bereitstellen von Modellen bis hin zur Produktion auf SQL Server in gespeicherten Prozeduren ausführen
- Ändern von R-Code zum Minimieren der Datenübertragung oder Entfernen von kostspielige Datentransformationen
- Aktivieren von automatisierten Tests und Umschulung von Modellen

Da die Wahl des Optimierungstechniken, hängt davon ab, welche Aufgabe für Ihre Anwendung oder ein Anwendungsfall wichtig ist, behandelt Fallstudien sowohl allgemeinen Leistungstipps und Leitfäden zum Optimieren für ein bestimmtes Szenario, Optimierung für die batchbewertung.

+ **Einzelne Optimierungsoptionen in SQL Server**

    In der ersten Fallstudie Leistung wurden mehrere Tests auf einem einzelnen Dataset, das einen Typ von Modell ausführen. Der Algorithmus RxLinMod im "revoscaler" wurde zum Erstellen eines Modells und Bewertungen daraus erstellen verwendet, aber der Code als auch die zugrunde liegenden Datentabellen systematisch zum Testen der Auswirkungen der einzelnen Änderungen geändert wurden.

    Beispielsweise wurde in einem Testlauf, der R-Code geändert, damit ein Vergleich zwischen Feature Engineering mit einer Transformationsfunktion im Vergleich zu vor berechnen die Funktionen und dem anschließenden Laden von Funktionen aus einer Tabelle durchgeführt werden konnte. In einem anderen Testlauf wurde Training modellleistung zwischen der Verwendung einer indizierten Standardtabelle im Vergleich zu Daten in einer Tabelle mit verschiedenen Typen von Komprimierung oder neue Indextypen verglichen.

+ **Optimierung für ein bestimmtes bewerteten hohem Volumen-Szenario**

    Machine Learning-Aufgaben in der zweiten Fallstudie umfasst viele Lebensläufe für mehrere Positionen übermittelt, und suchen die besten Kandidaten für die einzelnen Positionen Auftrag verarbeitet. Machine Learning-Modells selbst wird als ein binäres klassifikationsproblem formuliert: sie eine Beschreibung der fortsetzen und Auftrag als Eingabe akzeptiert und die Wahrscheinlichkeit für jedes Paar Resume-Job generiert. Da das Ziel ist die beste Übereinstimmung gefunden, wird ein benutzerdefinierte wahrscheinlichkeitsschwellenwert verwendet, weiter zu filtern und nur die guten Übereinstimmungen abrufen.

    Für diese Lösung war das Hauptziel bei der Bewertung mit geringer Latenz zu erreichen. Allerdings ist diese Aufgabe rechenintensive auch während der bewertet werden, da jeder neuer Auftrag mit Millionen von Lebensläufen innerhalb eines angemessenen Zeitraums abgeglichen werden muss. Darüber hinaus den Feature engineering über 2000 Funktionen pro Auftrag fortsetzen oder den erzeugt und einen erheblichen Leistungsengpass wird.

Es wird empfohlen, dass Sie überprüfen Sie alle Ergebnisse aus der ersten Fallstudie, um zu bestimmen, welche Techniken zur Projektmappe gelten, und wiegen ihre potenziellen Auswirkungen.

Überprüfen Sie die Ergebnisse des bewerteten Optimierung Fallstudie zu sehen, wie der Autor verschiedene Techniken angewendet und den Server zur Unterstützung einer bestimmten arbeitsauslastung optimiert.

## <a name="performance-optimization-process"></a>Leistung Optimierungsprozess

Konfiguration und Optimierung der Leistung benötigt, erstellen eine solide Grundlage für die Ebene Optimierungen für bestimmte arbeitsauslastungen konzipiert:

- Wählen Sie einen geeigneten Server zum Host Analytics. In der Regel wird eine sekundäre reporting, Datawarehouse oder einen anderen Server, der bereits zu anderen Berichts- oder Analytics bevorzugt. Allerdings können in einer hybridlösung transaktionale analytischen Verarbeitung (HTAP) für operative Daten als Eingabe für R zur schnellen Bewertung verwendet werden.

- Konfigurieren Sie die SQL Server-Instanz Saldo Modul Datenbankvorgänge und R oder Python-skriptausführung mit passender. Dazu gehören das Ändern von SQL Server-Standardwerte für den Arbeitsspeicher und CPU-Nutzung, NUMA und prozessoraffinitätsoptionen und Erstellung von Ressourcengruppen.

- Optimieren Sie die Server-Computers für die effiziente Verwendung externer Skripts unterstützen. Dazu kann gehören, erhöhen die Anzahl der Konten, die zum Ausführen des externen Skripts, Aktivierung der paketverwaltung, und Zuweisen von Benutzern zu zugehörigen Sicherheitsrollen.

- Anwenden von Optimierungen, die bestimmte auf Speicherung und Übertragung in SQL Server, einschließlich der Indizierung und Statistiken Strategien, Abfrageentwurf und abfrageoptimierung und des Entwurfs von Tabellen, die für Machine Learning verwendet werden. Sie möglicherweise auch analysieren, Datenquellen und Daten transportieren von Methoden, oder ändern Sie die ETL-Prozesse für die merkmalsextraktion zu optimieren.

- Optimieren der Analysemodell Ineffizienz zu vermeiden. Der Bereich der Optimierungen, die möglich sind richten sich nach der Komplexität von R-Code-Pakete und die Daten, die Sie verwenden. Wichtige Aufgaben umfassen teure Datentransformationen eliminieren oder Auslagern der Daten zur Vorbereitung oder Feature engineering Aufgaben von R oder Python ETL-Prozesse oder SQL. Sie können auch Umgestalten von Skripts, beseitigen Inline-Paket installiert, unterteilen Sie R-Code in separate Verfahren für das Training, Bewertung und Auswertung verwendet, oder vereinfachen Code effizienter als eine gespeicherte Prozedur funktioniert.

## <a name="articles-in-this-series"></a>Artikel in dieser Serie

+ [Optimieren der Leistung für R in SQL Server - hardware](..\r\sql-server-configuration-r-services.md)

    Bietet einen Leitfaden zum Konfigurieren der Hardware, [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] installiert ist, auf, und klicken Sie zum Konfigurieren von SQL Server-Instanz, um externe Skripts besser zu unterstützen. Dies ist besonders nützlich für **Datenbankadministratoren**.

+ [Optimieren der Leistung für R in SQL Server - Code und die Optimierung](..\r\r-and-data-optimization-r-services.md)

    Bietet Tipps zum Optimieren der externen Skript aus, um bekannte Probleme zu vermeiden. Es eignet sich am besten zum **Datenanalysten**.

    [!NOTE]
    > Während der Großteil der Informationen in diesem Abschnitt für R im Allgemeinen gilt, sind einige Informationen speziell für RevoScaleR-Analysefunktionen. Leitfaden zur detaillierten Leistung ist nicht verfügbar für **Revoscalepy** und andere unterstützte Python-Bibliotheken.

+ [Optimieren der Leistung für R in SQL Server - Methoden und Ergebnisse](..\r\performance-case-study-r-services.md)

    Fasst Daten wurde verwendet, die zwei Fallstudien, wie die Leistung getestet wurde und wie die Optimierungen Ergebnisse auswirken.
