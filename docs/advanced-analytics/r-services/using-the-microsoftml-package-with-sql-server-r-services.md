---
title: "Verwenden des MicrosoftML-Pakets mit SQL Server R Services | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Verwenden des MicrosoftML-Pakets mit SQL Server R Services
Das **MicrosoftML**-Paket, das in Microsoft R Server und SQL Server vNext CTP 1.0 enthalten ist, beinhaltet mehrere von Microsoft entwickelte Algorithmen für Machine Learning, die Verarbeitung auf mehreren CPU-Kernen und schnelles Streaming von Daten unterstützen. Das Paket enthält auch die Transformationen für Textverarbeitung und -featurebereitstellung.

### <a name="new-machine-learning-algorithms"></a>Neue Machine Learning-Algorithmen


-  **Schnell linear.** Ein lineares Lernmodul, das auf doppeltem stochastischem Koordinatenanstieg basiert und für die binäre Klassifikation oder Regression verwendet werden kann. Das Modell unterstützt L1- und L2-Regularisierung.

- **Schneller Baum.** Ein verstärkter (geboosteter) Entscheidungsbaumalgorithmus, der ursprünglich als FastRank bezeichnet wurde und für die Verwendung in Bing entwickelt wurde. Es ist eins der schnellsten und am häufigsten verwendeten Lernmodule. Es unterstützt binäre Klassifizierung und Regression.

- **Schneller Forest.** Ein logistisches Regressionsmodell, das auf der Random Forest-Methode basiert. Es ähnelt der `rxLogit`-Funktion in RevoScaleR, unterstützt aber L1- und L2-Regularisierung. Es unterstützt binäre Klassifizierung und Regression.

- **Logistische Regression.** Ein logistisches Regressionsmodell ähnlich der `rxLogit`-Funktion in RevoScaleR mit zusätzlicher Unterstützung für L1- und L2-Regularisierung. Unterstützt binäre und Mehrklassenklassifizierung.

- **Neurales Netz.** Ein neurales Netzwerkmodell für binäre Klassifikation, Mehrklassenklassifikation und Regression. Unterstützt GPU-Beschleunigung und anpassbare Convoluted Networks.

- **Einklassiger SVM.** Ein Modell zur Erkennung von Anomalien, das auf der SVM-Methode basiert und für die binäre Klassifikation in unsymmetrischen Datasets verwendet werden kann.

## <a name="transformation-functions"></a>Transformationsfunktionen

Das **MicrosoftML**-Paket enthält außerdem die folgenden Funktionen, die zum Transformieren von Daten und Extrahieren von Features verwendet werden können.

- `featurizeText()`
 
  Generiert die Anzahl von ngrams in einer angegebenen Textzeichenfolge. 

  Diese Funktion schließt die Optionen zum Erkennen der verwendeten Sprache, zum Durchführen von Texttokenisierung und -normalisierung, zum Entfernen von Stoppwörtern und zum Erzeugen von Features aus Text ein. 

- `categorical()`

  Erstellt ein Wörterbuch aus Kategorien und transformiert jede Kategorie in Indikatorvektor. 
 
- `categoricalHash()`

  Konvertiert kategorische Werte durch Hashen des Werts und Verwendung des Hashs als Index in der Bag in ein Indikatorarray.  

- `selectFeatures()` 

  Wählt eine Teilmenge der Funktionen aus der angegebenen Variable aus, entweder durch Zählen von nicht dem Standard entsprechenden Werten oder durch Berechnen eines gegenseitigen Informationspunktestands im Hinblick auf die Bezeichnung. 

Genauere Informationen zu diesen neuen Funktionen finden Sie unter [MicrosoftML functions (Microsoft ML-Funktionen)](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml).

## <a name="support-for-microsoftml-in-r-services"></a>Unterstützung für MicrosoftML in R-Services

Das **MicrosoftML**-Paket ist vollständig in die vom **RevoScaleR**-Paket verwendete Datenverarbeitungspipeline integriert. Derzeit können Sie das **MicrosoftML**-Paket in beliebigen Windows-basierten Rechenkontexten verwenden, einschließlich SQL Server R Services.



## <a name="see-also"></a>Siehe auch


[RevoScaleR Function Reference](https://msdn.microsoft.com/microsoft-r/scaler/scaler) (RevoScaleR-Funktionen – Verweis)

