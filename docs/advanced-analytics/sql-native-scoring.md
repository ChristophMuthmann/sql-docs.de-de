---
title: Systemeigene Bewertung | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1cb06223e5274c1fa439eb9f7d82a005e93a47d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---

# <a name="native-scoring"></a>Systemeigene Bewertung

Dieses Thema beschreibt die für Features, die sich in SQL Server-2017 Bewertung auf Machine Learning-Modellen in beinahe in Echtzeit zur Verfügung.

+ Was ist die systemeigene Bewertung im Vergleich zu Echtzeit-Bewertung
+ Funktionsweise
+ Unterstützte Plattformen und Anforderungen

## <a name="what-is-native-scoring-and-how-is-it-different-from-realtime-scoring"></a>Was ist native bewerten und wie es vom Echtzeit abweicht Bewertung?

In SQL Server 2016 erstellt Microsoft ein Extensibility Framework, die R-Skripts, die von T-SQL ausgeführt werden kann. Dieses Framework unterstützt jeder Vorgang, die in R, von einfachen Funktionen bis hin zu komplexen Training-Machine learning-Modellen ausgeführt werden kann. Dual-Process-Architektur, die mit SQL Server R-Paaren bedeutet jedoch, dass externe R-Prozesse für jeden Aufruf, unabhängig von der Komplexität des Vorgangs aufgerufen werden müssen. Wenn Sie ein vortrainiertes Modell aus einer Tabelle und Daten bereits in SQL Server Bewertung laden, stellt der Aufwand des Aufrufs des externen Prozess von R eine unnötige Leistungseinbuße dar.

_Bewertung_ ist ein zweistufiger Prozess: ein vortrainiertes Modell wird aus einer Tabelle geladen, und neue Eingabedaten, tabellarische oder einzelne Zeilen an das Modell, das neue Werte generiert übergeben werden (oder _Bewertungen_). Die Ausgabe kann es sich um eine einzelne Spalte-Wert, eine Wahrscheinlichkeit darstellt, oder mehrerer Werte, z. B. ein Konfidenzintervall, Fehler oder andere nützliche Ergänzung mit der Vorhersage sein.

Wenn viele Zeilen mit Daten zu bewerten, werden die neuen Werte in der Regel in einer Tabelle als Teil der bewertungs-Prozedur eingefügt.  Sie können jedoch auch ein einzelnes Ergebnis in Echtzeit abrufen. Bei der Bewertung von aufeinander folgenden Eingaben möglicherweise das Modell zwischengespeichert werden, damit sie in den Arbeitsspeicher schnell erneut geladen werden kann.

Zur schnellen Bewertung zu unterstützen, bieten SQL Server-Machine Learning-Services (und Microsoft Machine Learning-Server) integrierte bewerteten Bibliotheken, die in R oder in T-SQL zu arbeiten. Sie haben verschiedene Optionen, je nachdem, welche, die Version Sie haben.

**Systemeigene Bewertung**

+ Der PREDICT-Funktion in Transact-SQL kann verwendet werden, für _native Bewertung_ in jeder Instanz von SQL Server-2017. Er erfordert nur, dass Sie ein Modell ist bereits trainiert und in einer Tabelle gespeichert haben oder über T-SQL aufgerufen werden kann. Es ist eine Art von Realtime Bewertung, die systemeigene T-SQL-Funktionen verwendet. keine zusätzliche Konfiguration erforderlich.

   Die R-Laufzeit wird nicht aufgerufen und muss nicht installiert werden.

**Echtzeit-Bewertung**

+ **Sp_rxPredict** ist eine gespeicherte Prozedur für Echtzeit-Bewertung, Generieren von Bewertungen aus jedem unterstützten Modelltyp ohne Aufrufen der R-Laufzeit verwendet werden kann.

  Diese Option, um die Echtzeit Bewertung verwenden, ist auch in SQL Server 2016 verfügbar, wenn Sie R-Komponenten, die das eigenständige Installationsprogramm von Microsoft R Server aktualisieren. Sp_rxPredict wird auch in SQL Server-2017 unterstützt und möglicherweise eine gute Wahl, wenn Sie einen Modelltyp, die nicht von der PREDICT-Funktion unterstützt bewerten.

+ Die RxPredict-Funktion kann verwendet werden, zur schnellen Bewertung in R-Code.

Für all diese Bewertungsmethode verwenden müssen Sie ein Modell verwenden, die mithilfe eines der unterstützten Algorithmen "revoscaler" oder MicrosoftML trainiert wurde.

Ein Beispiel für Echtzeit-Bewertung in Aktion, finden Sie unter [End-to-End Loan ChargeOff Vorhersage erstellt mithilfe von Azure HDInsight Spark-Cluster und SQL Server 2016-R-Dienst](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

## <a name="how-native-scoring-works"></a>Wie systemeigene Works Bewertung

Systemeigene Bewertung verwendet systemeigene C++-Bibliotheken von Microsoft, die das Modell aus einem speziellen binären Format lesen können, und Generieren von Bewertungen. Da ein Modell veröffentlicht und für die Bewertung ohne Aufruf von R-Interpreter verwendet werden kann, wird der Aufwand von Interaktionen an mehrere Prozess reduziert. Dadurch wird eine schnellere vorhersageleistung in Produktionsszenarien Enterprise unterstützt.

Zum Generieren von Bewertungen, die diese Bibliothek verwenden, rufen Sie die bewertungs-Funktion, und übergeben die folgenden erforderlichen Eingaben:

+ Ein Modell, kompatibel. Finden Sie unter der [Anforderungen](#Requirements) Abschnitt Weitere Informationen.
+ Eingabedaten, in der Regel als eine SQL-Abfrage definiert.

Die Funktion gibt die Vorhersagen für die Eingabedaten, sowie alle Spalten der Quelldaten, denen durchlaufen werden sollen.

Codebeispiele zusammen mit Anweisungen zum Vorbereiten der Modelle im Binärformat erforderlich ist, finden Sie im Artikel:

+ [Zum Ausführen der Echtzeit-Bewertung](r/how-to-do-realtime-scoring.md)

## <a name="requirements"></a>Anforderungen

Unterstützte Plattformen sind wie folgt aus:

+ SQL Server 2017 Machine Learning Services (einschließlich Microsoft R Server 9.1.0)
    
    Systemeigene Bewertung VORHERSAGEN mit erfordert SQL Server-2017.
    Er kann für eine beliebige Version von SQL Server-2017, einschließlich Linux.

    Sie können auch ausführen, Echtzeit Bewertung mit Sp_rxPredict, welches erfordert, dass SQL CLR-fähig sein.

+ SQL Server 2016

   Bewerten von mit Echtzeit Sp_rxPredict mit SQL Server 2016 möglich ist, und kann auch auf Microsoft R Server ausgeführt werden. Diese Option erfordert das SQLCLR aktiviert werden soll, und die Installation von Upgrades für den Microsoft R Server.
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
  + [rxdForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

Wenn Sie Modelle auf der Grundlage MicrosoftML verwenden müssen, verwenden Sie Echtzeit-batchbewertung mit Sp_rxPredict.

### <a name="restrictions"></a>Einschränkungen

Die folgenden Modelltypen werden nicht unterstützt:

+ Modelle, die mit anderen, nicht unterstützte Arten von R-Transformationen
+ Modelle mit der `rxGlm` oder `rxNaiveBayes` Algorithmen in "revoscaler"
+ PMML-Modelle
+ Mit anderen R-Bibliotheken von CRAN oder anderen Repositorys erstellte Modelle
+ Modelle, die eine beliebige andere Art von R-Transformation enthält.

