---
title: R-Modelle erstellen | Microsoft Docs
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: a195d5e2-72e2-4dd6-bf43-947312e4a52a
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 50176ffbdaa8631f6f928bd6ecd23ab0feb28839
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-r-models"></a>Erstellen Sie R-Modelle

Sie haben die Trainingsdaten nun erweitert und können zum Analysieren der Daten die lineare Regression verwenden. Lineare Modelle sind ein wichtiges Tool in der Welt von Vorhersageanalysen. Das **RevoScaleR** -Paket in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] enthält hierfür einen leistungsfähigen, skalierbaren Algorithmus.

## <a name="create-a-linear-regression-model"></a>Erstellen eines linearen Regressionsmodells

Sie erstellen ein einfaches lineares Modell, das den Kreditkartensaldo eines Kunden mithilfe der unabhängigen Variablen in den Spalten *gender* und *creditLine* schätzt.
  
Zu diesem Zweck verwenden Sie die neue Funktion **rxLinMod** , die Remotecomputekontexte unterstützt.
  
1. Erstellen Sie eine R-Variable, um das fertige Modell zu speichern, und rufen Sie die Funktion *rxLinMod* auf, um eine geeignete Formel zu übergeben.
  
    ```R
    linModObj <- rxLinMod(balance ~ gender + creditLine,  data = sqlFraudDS)
    ```
  
2. Um eine Zusammenfassung der Ergebnisse anzuzeigen, rufen Sie einfach die R-Standardfunktion *summary* für das Modellobjekt auf.
  
     ```R
     summary(linModObj)
     ```

Es mag Ihnen seltsam erscheinen, dass eine einfache R-Funktion wie **summary** hier funktioniert, da Sie im vorherigen Schritt den Server als Computekontext festgelegt haben. Auch wenn die Funktion **rxLinMod** den Remotecomputekontext zum Erstellen des Modells verwendet, gibt sie auch ein Objekt zurück, das das Modell für Ihre lokale Arbeitsstation enthält und es im freigegebenen Verzeichnis speichert.

Daher können Sie R-Standardbefehle für das Modell ausführen, als ob es mithilfe des „lokalen“ Kontexts erstellt wurde.

**Ergebnisse**

*Linear Regression Results for: balance ~ gender + creditLineData: sqlFraudDS (RxSqlServerData Data Source)*

*Dependent variable(s): balance*

*Total independent variables: 4 (Including number dropped: 1)*

*Number of valid observations: 10000*

*Number of missing observations: 0*

*Coefficients: (1 not defined because of singularities)*

*Estimate Std. Fehlerwert t Pr (> | t |) (Intercept)*

*3253.575 71.194 45.700 2.22e-16*

*gender=Male -88.813 78.360 -1.133 0.257*

*gender=Female Dropped Dropped Dropped Dropped*

*creditLine 95.379 3.862 24.694 2.22e-16*

*Signif. codes: 0  0.001  0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1*

*Residual standard error: 3812 on 9997 degrees of freedom*

*Multiple R-squared: 0.05765*

*Adjusted R-squared: 0.05746*

*F-statistic: 305.8 on 2 and 9997 DF, p-value: < 2.2e-16*

*Condition number: 1.0184*

## <a name="create-a-logistic-regression-model"></a>Erstellen eines logistischen Regressionsmodells

Nun erstellen Sie ein logistisches Regressionsmodell, das angibt, ob ein bestimmter Kunde ein Betrugs-Risiko ist. Verwenden Sie die Funktion *rxLogit* (enthalten im **RevoScaleR** -Paket), die die Anpassung der logistischen Regressionsmodelle in Remotecomputekontexten unterstützt.

1.  Lassen Sie den Computekontext wie er ist. Sie werden weiterhin auch die gleiche Datenquelle verwenden.

2.  Rufen Sie die Funktion **rxLogit** auf, und übergeben Sie die Formel, die zum Definieren des Modells erforderlich ist.

    ```R
    logitObj <- rxLogit(fraudRisk ~ state + gender + cardholder + balance +      numTrans + numIntlTrans + creditLine, data = sqlFraudDS,      dropFirst = TRUE)
    ```
  
    Da es ein großes Modell mit 60 unabhängigen Variablen ist, einschließlich der drei Dummy-Variablen, die gelöscht werden, müssen Sie möglicherweise ein paar Minuten warten, bis der Computekontext das Objekt zurückgibt.
    
    Der Grund für die Größe des Modells ist, dass in R und im **RevoScaleR** -Paket alle Ebenen einer kategorischen Faktor-Variable automatisch als separate Dummyvariablen behandelt werden.
  
3.  Rufen Sie die **summary** -Funktion von R auf, um eine Zusammenfassung des zurückgegebenen Modells anzuzeigen.
  
    ```R
    summary(logitObj)
    ```
  
**Teilergebnisse**

*Logistic Regression Results for: fraudRisk ~ state + gender +     cardholder + balance + numTrans + numIntlTrans + creditLine*

*Data: sqlFraudDS (RxSqlServerData Data Source)*

*Dependent variable(s): fraudRisk*

*Total independent variables: 60 (Including number dropped: 3)*

*Anzahl der gültigen Beobachtungen: 10000-2*

*LogLikelihood: 2032.8699 (Residual deviance on 9943 degrees of freedom)*

*Coefficients:*

*Estimate Std. Error z value Pr(>|z|)     (Intercept)*

*-8.627e+00  1.319e+00  -6.538 6.22e-11*

*state=AK                Dropped    Dropped Dropped  Dropped*

*state=AL             -1.043e+00  1.383e+00  -0.754   0.4511*

*(other states omitted)*

*gender=Male             Dropped    Dropped Dropped  Dropped*

*gender=Female         7.226e-01  1.217e-01   5.936 2.92e-09*

*cardholder=Principal    Dropped    Dropped Dropped  Dropped*

*Karteninhabern = sekundäre 5.635e-3.403e 01-01 1.656 0.0977*

*balance               3.962e-04  1.564e-05  25.335 2.22e-16*

*numTrans              4.950e-02  2.202e-03  22.477 2.22e-16*

*numIntlTrans          3.414e-02  5.318e-03   6.420 1.36e-10*

*creditLine            1.042e-01  4.705e-03  22.153 2.22e-16*

*---*

*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*

*Condition number of final variance-covariance matrix: 3997.308*

*Number of iterations: 15*

## <a name="next-step"></a>Nächster Schritt

[Neue Bewertungsdaten](../../advanced-analytics/tutorials/deepdive-score-new-data.md)

## <a name="previous-step"></a>Vorheriger Schritt

[Visualisieren von SQL Server-Daten mithilfe von R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)



