---
title: Systemeigene Bewertung | Microsoft Docs
ms.custom: 
ms.date: 09/19/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 9fdd033a2e3ad05e06acb64ad38587782153a7c0
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="native-scoring"></a>Systemeigene Bewertung

Dieses Thema beschreibt die für Features, die sich in SQL Server-2017 Bewertung auf Machine Learning-Modellen in beinahe in Echtzeit zur Verfügung.

+ Was ist die systemeigene Bewertung im Vergleich zu Echtzeit-Bewertung
+ Funktionsweise
+ Unterstützte Plattformen und Anforderungen

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>Was ist native bewerten und wie es vom Echtzeit abweicht Bewertung?

In SQL Server 2016 erstellt Microsoft ein Extensibility Framework, die R-Skripts, die von T-SQL ausgeführt werden kann. Dieses Framework unterstützt jeder Vorgang, die in R, von einfachen Funktionen bis hin zu komplexen Training-Machine learning-Modellen ausgeführt werden kann. Dual-Process-Architektur erfordert jedoch Aufrufen eines externen R-Prozess für jeden Aufruf, unabhängig von der Komplexität des Vorgangs. Wenn Sie ein vortrainiertes Modell aus einer Tabelle und Daten bereits in SQL Server Bewertung laden, stellt der Aufwand des Aufrufs des externen Prozess von R eine unnötige Leistungseinbuße dar.

_Bewertung_ ist ein zweistufiger Prozess. Geben Sie Sie zunächst ein vortrainiertes Modell aus einer Tabelle zu laden. Zweitens, übergeben Sie neue Eingabedaten an die Funktion zum Generieren der Vorhersagewerte (oder _Bewertungen_). Die Eingabe kann ein tabellarisches oder einzelne Zeilen. Sie können auswählen, die Ausgabe eines einzelne Spalte-Wert, eine Wahrscheinlichkeit darstellt, oder Sie möglicherweise mehrere Werte, z. B. ein Konfidenzintervall, Fehler oder andere nützliche Ergänzung mit der Vorhersage ausgegeben.

Wenn die Eingabe viele Datenzeilen enthält, in der Regel schneller ausgeführt wird und eine Tabelle als Teil der Bewertungsprozess Vorhersagewerte einzufügen.  Generieren ein einzelnes Ergebnis ist ein häufiger in einem Szenario, in dem Sie Eingabewerte von einer Form oder Benutzer-Anforderung abrufen und das Ergebnis an eine Clientanwendung zurück. Zum Verbessern der Leistung beim Generieren von aufeinander folgenden Bewertungen möglicherweise SQL Server das Modell zwischengespeichert, sodass erneut in den Arbeitsspeicher geladen werden kann.

Zur schnellen Bewertung zu unterstützen, bieten SQL Server-Machine Learning-Services (und Microsoft Machine Learning-Server) integrierte bewerteten Bibliotheken, die in R oder in T-SQL zu arbeiten. Sie haben verschiedene Optionen, je nachdem, welche, die Version Sie haben.

**Native Bewertung**

+ Die PREDICT-Funktion in Transact-SQL unterstützt _native Bewertung_ in einer beliebigen Instanz von SQL Server-2017. Es ist nur erforderlich, dass Sie ein Modell bereits trainiert haben, die Sie aufrufen können mithilfe des T-SQL. Systemeigene bewerten mithilfe des T-SQL-hat folgende Vorteile:

    + Es ist keine zusätzliche Konfiguration erforderlich.
    + Die R-Laufzeit wird nicht aufgerufen. Besteht keine Notwendigkeit zum Installieren von r

**Echtzeit-Bewertung**

+ **Sp_rxPredict** ist eine gespeicherte Prozedur für Echtzeit-Bewertung, Generieren von Bewertungen aus jedem unterstützten Modelltyp ohne Aufrufen der R-Laufzeit verwendet werden kann.

  Diese gespeicherte Prozedur wird auch in SQL Server 2016 verfügbar, wenn Sie R-Komponenten, die das eigenständige Installationsprogramm von Microsoft R Server aktualisieren. Sp_rxPredict wird auch in SQL Server-2017 unterstützt. Aus diesem Grund können Sie diese Funktion verwenden, beim Generieren von Bewertungen mit einem Modelltyp, der von der PREDICT-Funktion nicht unterstützt.

+ Die RxPredict-Funktion kann verwendet werden, zur schnellen Bewertung in R-Code.

Für all diese Bewertungsmethode verwenden müssen Sie ein Modell verwenden, die mithilfe eines der unterstützten Algorithmen "revoscaler" oder MicrosoftML trainiert wurde.

Ein Beispiel für Echtzeit-Bewertung in Aktion, finden Sie unter [End-to-End Loan ChargeOff Vorhersage erstellt mithilfe von Azure HDInsight Spark-Cluster und SQL Server 2016-R-Dienst](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>Wie systemeigene Works Bewertung

Systemeigene Bewertung verwendet systemeigene C++-Bibliotheken von Microsoft, die das Modell aus einem speziellen binären Format lesen können, und Generieren von Bewertungen. Da ein Modell veröffentlicht und für die Bewertung ohne Aufruf von R-Interpreter verwendet werden kann, wird der Aufwand von Interaktionen an mehrere Prozess reduziert. Daher unterstützt systemeigene Bewertung eine schnellere vorhersageleistung in Produktionsszenarien Enterprise.

Zum Generieren von Bewertungen, die diese Bibliothek verwenden, rufen Sie die bewertungs-Funktion, und übergeben die folgenden erforderlichen Eingaben:

+ Ein Modell, kompatibel. Finden Sie unter der [Anforderungen](#Requirements) Abschnitt Weitere Informationen.
+ Eingabedaten, in der Regel als eine SQL-Abfrage definiert.

Die Funktion gibt die Vorhersagen für die Eingabedaten, sowie alle Spalten der Quelldaten, denen durchlaufen werden sollen.

Codebeispiele zusammen mit Anweisungen zum Vorbereiten der Modelle im Binärformat erforderlich ist, finden Sie im Artikel:

+ [Zum Ausführen der Echtzeit-Bewertung](r/how-to-do-realtime-scoring.md)

Eine vollständige Lösung, die systemeigene Bewertung enthält, finden Sie diese Beispiele von der SQL Server-Entwicklungsteam:

+ Ihr ML-Skript bereitstellen: [mithilfe eines Modells Python](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/step/3.html)
+ Ihr ML-Skript bereitstellen: [mithilfe eines R-Modells](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/step/3.html)

## <a name="requirements"></a>Anforderungen

Unterstützte Plattformen sind wie folgt aus:

+ SQL Server 2017 Machine Learning Services (einschließlich Microsoft R Server 9.1.0)
    
    Systemeigene Bewertung VORHERSAGEN mit erfordert SQL Server-2017.
    Er kann für eine beliebige Version von SQL Server-2017, einschließlich Linux.

    Sie können auch ausführen, Echtzeit Bewertung mit Sp_rxPredict. Verwenden Sie diese gespeicherte Prozedur erfordert die Aktivierung von [SQL Server-CLR-Integration](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).

+ SQL Server 2016

   Bewertung mit Sp_rxPredict Echtzeit mit SQL Server 2016 möglich ist, und kann auch auf Microsoft R Server ausgeführt werden. Diese Option erfordert das SQLCLR aktiviert werden soll, und die Installation von Upgrades für den Microsoft R Server.
   Weitere Informationen finden Sie unter [Echtzeit Bewertung](Real-time-scoring.md)

### <a name="model-preparation"></a>Modell zur Vorbereitung

+ Das Modell muss im voraus mit einer der unterstützten trainiert **Rx** Algorithmen. Weitere Informationen finden Sie unter [Algorithmen unterstützt](#bkmk_native_supported_algos).
+ Das Modell muss gespeichert werden, mithilfe der neuen Serialisierungsfunktion, die in Microsoft R Server 9.1.0 bereitgestellt. Die Serialisierungsfunktion wird optimiert, um schnelle Bewertung unterstützen.

### <a name="bkmk_native_supported_algos"></a>Algorithmen, die systemeigene Bewertung unterstützen

+ "Revoscaler"-Modelle

  + [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)
  + [der rxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Wenn Sie Modelle auf der Grundlage MicrosoftML verwenden müssen, verwenden Sie Echtzeit-batchbewertung mit Sp_rxPredict.

### <a name="restrictions"></a>Restrictions

Die folgenden Modelltypen werden nicht unterstützt:

+ Modelle, die mit anderen, nicht unterstützte Arten von R-Transformationen
+ Modelle mit der `rxGlm` oder `rxNaiveBayes` Algorithmen in "revoscaler"
+ PMML-Modelle
+ Mit anderen R-Bibliotheken von CRAN oder anderen Repositorys erstellte Modelle
+ Modelle, die mit anderen R-transformation
