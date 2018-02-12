---
title: Verwenden das Paket MicrosoftML mit SQLServer | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d6b3c17d4fadf639102c4090fceaabee37276bc2
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>Verwenden das Paket MicrosoftML mit SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Die [ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) Paket, das mit Microsoft R Server und SQL Server-2017 bereitgestellt wird, enthält mehrere Algorithmen für maschinelles lernen. Diese APIs wurden von Microsoft für interne Machine learning-Anwendungen entwickelt und wurden im Laufe der Jahre zur Unterstützung von hohen Leistung von big Data Mehrkern Verarbeitung und Fast Track-Data streaming mit. MicrosoftML enthält auch mehrere Transformationen für Text- und Image-Verarbeitung.

In SQL Server 2017 CTP 2.0 wurde Unterstützung für die Python-Sprache hinzugefügt. Die **Microsoftml** -Paket für Python entsprechen denen im Paket MicrosoftML Funktionen für r enthält. 

+ **MicrosoftML für R**

    Einführung und Paket-Referenz: [MicrosoftML: machine Learning R-Algorithmen](https://docs.microsoft.com/en-us/r-server/r-reference/microsoftml/microsoftml-package)

    Da R Groß-/Kleinschreibung beachtet wird, stellen Sie sicher, dass Sie den Namen ordnungsgemäß beim Laden des Pakets verweisen.

+ **Microsoftml für Python**

    Einführung und Paket-Referenz: [Microsoftml (Funktionsbibliothek für Python)](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package). 

## <a name="whats-in-microsoftml"></a>Was ist in der MicrosoftML

MicrosoftML enthält eine Vielzahl von Machine learning-Algorithmen und Transformationen, die für Leistung optimiert wurden.

### <a name="machine-learning-algorithms"></a>Machine Learning-Algorithmen

-  Linearen Modellen: `rxFastLinear` einer linearen Lernmodulen basieren auf stochastischen duale-Koordinate (Versalhöhe), die für binäre Klassifizierung oder Regression verwendet werden kann. Das Modell unterstützt L1- und L2-Regularisierung.

- Struktur und Entscheidung Gesamtstruktur Modelle Entscheidung: `rxFastTree` einem verstärkten Entscheidungsbaumalgorithmus als FastRank, die für die Verwendung in Bing entwickelt wurde ursprünglich bezeichnet wird. Es ist eins der schnellsten und am häufigsten verwendeten Lernmodule. Es unterstützt binäre Klassifizierung und Regression.

  `rxFastForest`basiert ein Logistisches Regressionsmodell auf die zufälligen Gesamtstruktur-Methode. Es ähnelt der `rxLogit` -Funktion in RevoScaleR, unterstützt aber L1- und L2-Regularisierung. Es unterstützt binäre Klassifizierung und Regression.

- Die logistische Regression: `rxLogisticRegression` ähnelt ein logistischen Regressionsmodell der `rxLogit` Funktion in "revoscaler", mit zusätzlicher Unterstützung für die L1- und L2-regularisierung. Binäre oder mehrklassige Klassifizierung wird unterstützt.

- Neuronale Netzwerke: die `rxNeuralNet` -Funktion unterstützt die binäre Klassifizierung, mehrklassige Klassifizierung und Regression neuronaler Netzwerke verwenden. Kompliziert Netzwerke mit GPU-Beschleunigung mit einer einzelnen GPU Customizable und unterstützt.

- Erkennung von Anomalien.  Die `rxOneClassSvm` Funktion basiert auf der SVM-Methode, jedoch ist für die binäre Klassifizierung in unausgeglichenen Datasets optimiert.

### <a name="transformation-functions"></a>Transformationsfunktionen

MicrosoftML umfasst zahlreiche spezielle Funktionen, die für das Transformieren von Daten und extrahieren Features eignen.

- Textverarbeitung-Replikate umfassen auch die `featurizeText` und `getSentiment` Funktionen. Sie können n-gramme zu zählen, erkennen die verwendete Sprache oder Text-Normalisierung durchzuführen. Sie können allgemeine Text Bereinigungsvorgänge wie z. B. Stoppwort Entfernung ausführen, oder ein Hashwert erstellt wurde oder Count based Features aus Text zu generieren.

- Funktionsauswahl und Transformation-Funktionen, wie z. B. feature `selectFeatures` oder `getSentiment`, Analysieren von Daten und Erstellen von Funktionen, die besonders für die Modellierung hilfreich sind.

- Arbeiten mit kategorievariablen wie z. B. mit `categorical` oder `categoricalHash`, die Kategoriewerte konvertieren Sie in indizierten Arrays für eine bessere Leistung.

- Spezielle Funktionen für die bildverarbeitung und Analysen, z. B. `extractPixels` oder `featurizeImage`, können Sie die meisten Informationen zu erhalten, Bilder und Bilder schneller verarbeiten.

Weitere Informationen finden Sie unter [MicrosoftML functions (Microsoft ML-Funktionen)](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml).

## <a name="how-to-use-microsoftml"></a>Gewusst wie: Verwenden von MicrosoftML

Dieser Abschnitt beschreibt, wie Suchen und Laden Sie das Paket in Ihrem R und Python-Code.

+ Das Paket MicrosoftML für R wird standardmäßig mit Microsoft R Server 9.1.0 und in SQL Server-2017 installiert.

    Es ist auch für die Verwendung mit SQL Server 2016 verfügbar, wenn Sie die R-Komponenten für die Instanz mithilfe der Microsoft R Server-Installation wie beschrieben hier aktualisieren: [Aktualisieren einer Instanz von SQL Server mithilfe der Bindung](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ Die **Microsoftml** -Paket für Python mit SQL Server-2017 standardmäßig installiert ist 

   Um dieses Paket zu verwenden, wird empfohlen, ein upgrade auf Release Candidate 2 oder höher. Eine frühere Version mit RC1 veröffentlicht wurde, aber die Bibliothek hat beträchtliche bzw. die Revision, einschließlich Änderungen an den Funktionsnamen unterzogen. 

Für R und Python, das Paket jedoch nicht standardmäßig geladen; Daher müssen Sie das Paket explizit als Teil des Codes mit seiner Funktionen laden.

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>Aufrufen von MicrosoftML Funktionen von R in SQL Server

R-Code laden Sie das Paket MicrosoftML, und rufen Sie ihre Funktionen, z. B. ein anderes Paket.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**Hinweise**

+ Das Paket MicrosoftML ist vollständig in die Datenverarbeitung-Pipeline, die von der "revoscaler"-Paket bereitgestellte integriert. Daher können Sie das Paket MicrosoftML in jedem Windows-basierten computekontext, einschließlich einer Instanz von SQL-Server, auf Machine Learning-Erweiterungen aktiviert ist.

    MicrosoftML erfordert jedoch ein Verweis auf "revoscaler" und ihre Funktionen, um remote verwenden von remotecomputekontexten.

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>Aufrufen von Microsoftml Funktionen aus Python in SQL Server

Importieren Sie zum Aufrufen von Funktionen aus dem Paket, in Ihrem Python-Code, der **Microsoftml** -Paket, und importieren Sie **Revoscalepy** remote rechenkontexte oder verknüpfte Verbindung oder die Datenquelle verwendet werden sollen -Objekte. Verweisen Sie dann die einzelnen Funktionen, die Sie benötigen.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**Hinweise**

+ In SQL Server 2017 **Microsoftml** ist ein Modul Python35 kompatibel. 

+ Die Funktionen im **Microsoftml** sind integriert, mit der Compute-Kontexte und Datenquellen, die von unterstützt werden **Revoscalepy**. Daher können Sie die **Microsoftml** Python-Paket erstellen und Bewerten von Modellen in eine beliebige Windows-basierten computekontext, einschließlich einer Instanz von SQL Server mit Machine Learning-Erweiterungen. Aktiviert.

    Allerdings **Microsoftml** für Python erforderlich, einen Verweis auf **Revoscalepy** und ihre Funktionen, um remote verwenden von remotecomputekontexten.

Weitere Informationen zu Revoscalepy finden Sie unter:

+ [Was ist Revoscalepy](python/what-is-revoscalepy.md)

+ [Revoscalepy Funktionsbibliothek](https://docs.microsoft.com/en-us/r-server/python-reference/revoscalepy/revoscalepy-package) 
