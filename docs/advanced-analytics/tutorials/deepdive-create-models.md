---
title: Erstellen Sie R-Modelle (SQL und R deep Dive) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 97a773634bb4fd0fa5a78b57b2d8c182d2c66241
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="create-r-models-sql-and-r-deep-dive"></a>Erstellen Sie R-Modelle (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

Sie haben die Trainingsdaten nun erweitert und können zum Analysieren der Daten die lineare Regression verwenden. Lineare Modelle sind ein wichtiges Tool in der Welt von Vorhersageanalysen. Das **RevoScaleR** -Paket in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthält hierfür einen leistungsfähigen, skalierbaren Algorithmus.

## <a name="create-a-linear-regression-model"></a>Erstellen eines linearen Regressionsmodells

In diesem Schritt erstellen Sie ein einfaches Lineares Modell, das für die Kunden, verwenden als unabhängige Variablen die Werte in der Kreditkartensaldo schätzt die *Geschlecht* und *CreditLine* Spalten.
  
Verwenden Sie hierzu die [RxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) -Funktion, die remote rechenkontexte unterstützt.
  
1. Erstellen Sie eine R-Variable, und speichern Sie das abgeschlossene Modell, und rufen **RxLinMod**, übergeben eine entsprechende Formel.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. Rufen Sie zum Anzeigen einer Zusammenfassung der Ergebnisse der standardmäßige R `summary` Funktion in der Model-Objekts.
  
     ```R
     summary(linModObj)
     ```

Sie glauben sie spezielle, der eine einfache R-Funktion wie `summary` würde hier funktionieren, da im vorherigen Schritt des computekontexts mit dem Server festlegen. Auch wenn die Funktion **rxLinMod** den Remotecomputekontext zum Erstellen des Modells verwendet, gibt sie auch ein Objekt zurück, das das Modell für Ihre lokale Arbeitsstation enthält und es im freigegebenen Verzeichnis speichert.

Daher können Sie R-Standardbefehle für das Modell ausführen, als ob es mithilfe des „lokalen“ Kontexts erstellt wurde.

**Ergebnisse**

```
Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): balance
Total independent variables: 4 (Including number dropped: 1)
Number of valid observations: 10000
Number of missing observations: 0
Coefficients: (1 not defined because of singularities)

Estimate Std. Error t value Pr(>|t|) (Intercept)
3253.575 71.194 45.700 2.22e-16
gender=Male -88.813 78.360 -1.133 0.257
gender=Female Dropped Dropped Dropped Dropped
creditLine 95.379 3.862 24.694 2.22e-16
Signif. codes: 0  0.001  0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 3812 on 9997 degrees of freedom
Multiple R-squared: 0.05765
Adjusted R-squared: 0.05746
F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16
Condition number: 1.0184
```

## <a name="create-a-logistic-regression-model"></a>Erstellen eines logistischen Regressionsmodells

Als Nächstes erstellen Sie ein Logistisches Regressionsmodell, das angibt, ob ein bestimmter Kunde ein Betrug Risiko ist. Verwenden Sie die **"revoscaler"** [RxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) -Funktion, welche unterstützt die Anpassung der Modelle zur logistischen Regression in Remotebüros remotecomputekontexten.

1.  Lassen Sie den Computekontext wie er ist. Sie werden weiterhin auch die gleiche Datenquelle verwenden.

2.  Rufen Sie die Funktion **rxLogit** auf, und übergeben Sie die Formel, die zum Definieren des Modells erforderlich ist.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS, dropFirst = TRUE)
    ```
  
    Da es ein großes Modell mit 60 unabhängigen Variablen ist, einschließlich der drei Dummy-Variablen, die gelöscht werden, müssen Sie möglicherweise ein paar Minuten warten, bis der Computekontext das Objekt zurückgibt.
    
    Der Grund für die Größe des Modells ist, dass in R und im **RevoScaleR** -Paket alle Ebenen einer kategorischen Faktor-Variable automatisch als separate Dummyvariablen behandelt werden.
  
3.  Rufen Sie zum Anzeigen einer Zusammenfassung des zurückgegebenen Modells R `summary` Funktion.
  
    ```R
    summary(logitObj)
    ```
  
**Teilergebnisse**

```
Logistic Regression Results for: fraudRisk ~ state + gender + cardholder + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Dependent variable(s): fraudRisk
Total independent variables: 60 (Including number dropped: 3)
Number of valid observations: 10000 -2

LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)

Coefficients:
Estimate Std. Error z value Pr(>|z|)     (Intercept)
-8.627e+00  1.319e+00  -6.538 6.22e-11
state=AK                Dropped    Dropped Dropped  Dropped
state=AL             -1.043e+00  1.383e+00  -0.754   0.4511

(other states omitted)

gender=Male             Dropped    Dropped Dropped  Dropped
gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09
cardholder=Principal    Dropped    Dropped Dropped  Dropped
cardholder=Secondary  5.635e-01  3.403e-01   1.656   0.0977
balance               3.962e-04  1.564e-05  25.335 2.22e-16
numTrans              4.950e-02  2.202e-03  22.477 2.22e-16
numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10
creditLine            1.042e-01  4.705e-03  22.153 2.22e-16

Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1
Condition number of final variance-covariance matrix: 3997.308
Number of iterations: 15
```

## <a name="next-step"></a>Nächster Schritt

[Neue Bewertungsdaten](../../advanced-analytics/tutorials/deepdive-score-new-data.md)

## <a name="previous-step"></a>Vorherigen Schritt

[Visualisieren von SQL Server-Daten mit R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
