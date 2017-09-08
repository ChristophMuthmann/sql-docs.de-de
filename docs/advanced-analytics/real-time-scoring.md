---
title: Bewerten von Realtime | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
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
ms.openlocfilehash: c4d15a7f605f130ff4f93c7da66ca9a103195c17
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---

# <a name="realtime-scoring"></a>Echtzeit-Bewertung

In diesem Thema wird beschrieben, ein Feature in SQL Server 2016 und SQL Server-2017, der Machine Learning-Modellen in beinahe in Echtzeit unterstützt Bewertung verfügbar.

> [!TIP]
> Systemeigene bewerten ist eine spezielle Implementierung der Echtzeit-Bewertung, verwendet die systemeigene VORHERZUSAGEN, T-SQL-Funktion für sehr schnell bewerten und steht nur in SQL Server-2017. Weitere Informationen finden Sie unter [Native Bewertung](sql-native-scoring.md).

## <a name="how-realtime-scoring-works"></a>Funktionsweise der Echtzeit-Bewertung

Echtzeit-Bewertung wird für bestimmte Modelltypen mit Tabellenparameter "revoscaler" oder MicrosoftML Algorithmen erstellt wurden in SQL Server-2017 und SQL Server 2016 unterstützt. Er verwendet die systemeigene C++-Bibliotheken zum Generieren von Bewertungen, basierend auf Benutzereingaben bereitgestellt, um ein Machine learning-Modell in einem speziellen binären Format gespeichert.

Da einem trainierten Modell für die Bewertung ohne eine externe Sprachlaufzeit Aufruf verwendet werden kann, wird der Aufwand von mehreren Prozessen reduziert. Dadurch wird eine schnellere vorhersageleistung für die Produktion Bewertung Szenarien unterstützt. Da die Daten niemals SQL Server verlässt, können Ergebnisse generiert und in eine neue Tabelle ohne jegliche Daten Übersetzung zwischen R und SQL eingefügt werden.

Echtzeit bewerten ist ein mehrstufiger Prozess:

1. Die gespeicherte Prozedur, die Bewertung ist, muss regelmäßig pro Datenbank aktiviert sein.
2. Sie laden das vortrainierte Modell im Binärformat.
3. Geben Sie neue Eingabedaten, tabellarische oder einzelne Zeilen als Eingabe für das Modell.
4. Generieren von Bewertungen, rufen Sie die Sp_rxPredict Prozedur enthält.

## <a name="get-started"></a>Erste Schritte

Codebeispiele und Anleitungen finden Sie unter [wie systemeigene Bewertung oder Echtzeit Bewertung](r/how-to-do-realtime-scoring.md).

Ein Beispiel für RxPredict wie kann für die Bewertung verwendet, finden Sie unter [End-to-End Loan ChargeOff Vorhersage erstellt mithilfe von Azure HDInsight Spark-Cluster und SQL Server 2016-R-Dienst](https://blogs.msdn.microsoft.com/rserver/2017/06/29/end-to-end-loan-chargeoff-prediction-built-using-azure-hdinsight-spark-clusters-and-sql-server-2016-r-service/)

> [!TIP]
> Wenn Sie ausschließlich in R-Code arbeiten, können Sie auch die [RxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) Funktion zur schnellen Bewertung.

## <a name="requirements"></a>Anforderungen

Echtzeit-Bewertung wird auf diesen Plattformen unterstützt:

+ SQL Server 2017 Machine Learning Services (einschließlich Microsoft R Server 9.1.0)
+ SQL Server R Services 2016 mit einer Aktualisierung der R-Services-Instanz für Microsoft R Server 9.1.0 oder höher
+ Microsoft-Machine Learning-Server (eigenständig)

Auf SQL Server müssen Sie die Funktion im Voraus Bewertung Echtzeit aktivieren. Dies ist, da die Funktion, die Installation der CLR-basierten Bibliotheken in SQL Server erfordert.

Informationen zu Echtzeit Bewertung in einer verteilten Umgebung basierend auf Microsoft R Server finden Sie auf der [PublishService](https://msdn.microsoft.com/microsoft-r/mrsdeploy/packagehelp/publishservice) Funktion zur Verfügung, in der [MrsDeploy Paket](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy), welche unterstützt Veröffentlichen von Modellen in Echtzeit Bewertung als neue einen Webdienst, der auf R-Server ausgeführt wird.

### <a name="restrictions"></a>Einschränkungen

+ Das Modell muss im voraus mit einer der unterstützten trainiert **Rx** Algorithmen. Weitere Informationen finden Sie unter [Algorithmen unterstützt](#bkmk_rt_supported_algos). Echtzeit-batchbewertung mit Sp_rxPredict unterstützt "revoscaler" und MicrosoftML Algorithmen.

+ Das Modell muss gespeichert werden, mithilfe der neuen Serialisierungsfunktion, die in Microsoft R Server 9.1.0 bereitgestellt. Die Serialisierungsmethode wurde optimiert, um schnelle Bewertung unterstützen.

+ Echtzeit-Bewertung wird ein R-Interpreter nicht verwendet werden. Daher wird keine Funktionen, die R-Interpreter möglicherweise während des Schritts bewerteten nicht unterstützt.  Hierzu gehören zum Beispiel:

  + Modelle mit der `rxGlm` oder `rxNaiveBayes` Algorithmen werden derzeit nicht unterstützt.

  + "Revoscaler"-Modelle, verwenden ein R-Transformationsfunktion oder eine Formel, die eine Transformation enthält, z. B. <code>A ~ log(B)</code> werden in Echtzeit Bewertung nicht unterstützt. Ein Modell für diesen Typ verwenden, empfiehlt es sich, dass das Ausführen der Transformations für die Eingabe von Daten vor der Übergabe an die Echtzeit-Bewertung.

+ Echtzeit-Bewertung ist zurzeit für schnelle Vorhersagen in kleinere Datasets, die im Bereich von ein paar Zeilen bis Hunderte von tausend Zeilen optimiert. Für sehr große Datasets kann die Bewertung in R über RxPredict schneller sein.

### <a name="a-namebkmkrtsupportedalgosalgorithms-that-support-realtime-scoring"></a><a name="bkmk_rt_supported_algos">Algorithmen, die Echtzeit-Bewertung unterstützen

+ "Revoscaler"-Modelle

  + [RxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)\*
  + [RxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)\*
  + [RxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)\*
  + [der RxDtree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)\*
  + [RxdForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)\*
  
  Modelle mit markierten \* unterstützen auch die systemeigenen batchbewertung mit der PREDICT-Funktion.

+ MicrosoftML Modelle

  + [rxFastTrees](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxfastlinear)

+ Transformationen von MicrosoftML bereitgestellten

  + [featurizeText](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxfasttrees)
  + [concat](https://docs.microsoft.com/r-server/r-reference/microsoftml/concat)
  + ["categorical"](https://docs.microsoft.com/r-server/r-reference/microsoftml/categorical)
  + [categoricalHash](https://docs.microsoft.com/r-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](https://docs.microsoft.com/r-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>Nicht unterstützte Modelltypen

Die folgenden Modelltypen werden nicht unterstützt:

+ Modelle, die mit anderen, nicht unterstützte Arten von R-Transformationen
+ Modelle mit der `rxGlm` oder `rxNaiveBayes` Algorithmen in "revoscaler"
+ PMML-Modelle
+ Mit anderen R-Bibliotheken von CRAN oder anderen Repositorys erstellte Modelle
+ Modelle, die eine beliebige andere Art von R-Transformation, andere als die hier aufgeführten enthält

### <a name="known-issues"></a>Bekannte Probleme

+ `sp_rxPredict`Gibt eine fehlerhafte Nachricht zurück, wenn ein NULL-Wert wie das Modell übergeben wird: "System.Data.SqlTypes.SqlNullValueException:Data in Null".

## <a name="next-steps"></a>Nächste Schritte

[Wie Sie Echtzeit-Bewertung](r/how-to-do-realtime-scoring.md)
