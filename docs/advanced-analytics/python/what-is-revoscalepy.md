---
title: "Einführung in Revoscalepy | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 65a9924c70cdcdc86ce855b62caa23d19b72dc6d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="introducing-revoscalepy"></a>Einführung in revoscalepy

**Revoscalepy** ist eine neue Bibliothek, sofern von Microsoft zur Unterstützung verteilter Datenverarbeitung, compute Remote Kontexte und hohe Leistung Algorithmen für Python.

Es basiert auf der **"revoscaler"** -Paket für R, die in Microsoft R Server und SQL Server R Services und zielt auf die gleichen Funktionen bieten bereitgestellt wurde:

+ Unterstützt mehrere rechenkontexte, Remote- und lokale
+ Bietet Funktionen entsprechen denen im "revoscaler" für die Datentransformation und Visualisierung
+ Stellt Python-Versionen von "revoscaler" Machine Learning-Algorithmen für die verteilte oder parallele Verarbeitung
+ Verbesserte Leistung, einschließlich der Verwendung von der mathematische Intel-Bibliotheken

Außerdem werden für R und Python MicrosoftML Pakete bereitgestellt. Weitere Informationen finden Sie unter [MicrosoftML verwenden, in SQL Server](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>Versionen und unterstützte Plattformen

Die **Revoscalepy** Modul steht nur wenn Sie eine der folgenden Microsoft-Produkte installieren:

+ Machine Learning-Dienste in der SQLServer 2017
+ Machine Learning-Server Microsoft 9.2.0 oder höher

Um die neueste Version der Revoscalepy zu erhalten, installieren Sie kumulative Update 1 für SQL Server-2017 aus. Er umfasst viele Verbesserungen in Python, einschließlich:

+ Eine neue Funktion mit Python `rx_create_col_info`, Schemainformationen aus einer SQL Server-Datenquelle, z. B. abruft [RxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) für 
+ Verbesserungen an [Rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) zur Unterstützung paralleler Szenarien, die mit der `RxLocalParallel` computekontext. 

## <a name="supported-functions-and-data-types"></a>Unterstützte Funktionen und Datentypen

Dieser Abschnitt enthält eine Übersicht über die Python-Datentypen und die neue Python-Funktionen, die unterstützt die **Revoscalepy** ab Version von SQL Server 2017 CTP 2.0-Modul. 

Die aktuelle Liste der Funktionen in den Python-Bibliotheken, die bisher veröffentlichten finden Sie unter folgenden Links:

+ [Revoscalepy für Python](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [Microsoftml für Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>Datentypen, Datenquellen und rechenkontexte

SQL Server und Python verwenden unterschiedliche Datentypen in einigen Fällen. Eine Liste der Zuordnungen zwischen SQL und Python-Datentypen, finden Sie unter [Python-Bibliotheken und Datentypen](python-libraries-and-data-types.md).

Für maschinelles Lernen mit Python in SQL Server unterstützte Datenquellen enthält ODBC-Datenquellen, die SQL Server-Datenbank und die lokalen Dateien, einschließlich XDF-Dateien.

Sie erstellen das Datenquellenobjekt mithilfe von Funktionen, die in der folgenden Tabelle aufgeführt. Nach dem Definieren der Datenquelle an, Sie laden oder Transformieren von Daten mit einer entsprechenden [ETL-Funktion](#bkmk_etl).

> [!IMPORTANT]
> Viele Funktionsnamen wurden seit der Erstveröffentlichung von Python in CTP 2.0 geändert.

**SQL Server-Daten**

+ Verwendung [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) zum Definieren einer Datenquelle aus einer Abfrage oder eine Tabelle
+ Verwendung [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver) zum Erstellen einer SQL Server-computekontext.
+ Verwendung [RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata) So erstellen Sie eine Datenquelle aus einer ODBC-Verbindung

**Revoscalepy** unterstützt auch die [XDF-Datenquelle](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata), die für das Verschieben von Daten zwischen Arbeitsspeicher und andere Datenquellen verwendet.

> [!TIP]
> Wenn Sie mit der Idee von Datenquellen nicht vertraut sind oder von remotecomputekontexten, es wird empfohlen, Sie, indem Themen zu verteilten IT Works für maschinelles lernen starten ["revoscaler"](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction).


### <a name="bkmk_algorithms"></a>Machine Learning und Zusammenfassungsfunktionen

Die folgenden Machine Learning-Algorithmen und Zusammenfassungsfunktionen vom "revoscaler" werden in SQL Server 2017 ab CTP 2.0 enthalten.

| Funktion| Description|Hinweise|
| ------ | ------ |------ |
|`rx_btrees` | Passen Sie stochastic gradient Entscheidungsbäume|`rx_btrees_ex`in CTP 2.0|
|`rx_dforest` | Passen Sie die Klassifizierung und Regression entscheidungswälder|`rx_dforest_ex`in CTP 2.0|
|`rx_dtree` | Anpassen der Klassifizierung und Regression Strukturen |`rx_dtree_ex`in CTP 2.0|
|`rx_lin_mod` | Erstellen Sie ein Lineares Modell|`rx_lin_mod_ex`in CTP 2.0|
|`rx_logit` | Erstellen eines logistischen Regressionsmodells|`rx_logit_ex`in CTP 2.0|
|`rx_predict` | Vorhersagen von einem trainierten Modell generieren|`rx_predict_ex`in CTP 2.0|
|`rx_summary` | Generieren Sie eine Zusammenfassung des Modells||

Neue Machine Learning-Algorithmen werden ebenfalls bereitgestellt, von der Python-Version von [MicrosoftML](https://docs.microsoft.com/en-us/r-server/python-reference/microsoftml/microsoftml-package):

| Funktion| Description|
| ------ | ------ |
|`rx_fast_forest` |Erstellen Sie ein Entscheidungsstruktur-Gesamtstrukturmodell|
|`rx_fast_linear` | Lineare Regression mit stochastischen duale-Koordinate (Versalhöhe)|
|`rx_fast_trees` | Erstellen Sie ein verstärkten Strukturmodell |
|`rx_logistic_regression` | Erstellen eines logistischen Regressionsmodells|
|`rx_neural_network` | Erstellen eines anpassbaren neuronalen Netzwerkmodells |
|`rx_oneclass_svm` | Erstellt ein SVM-Modell von einem unausgeglichenen Dataset, für die Verwendung in der Erkennung von Anomalien|

> [!TIP]
> Viele der folgenden Algorithmen werden bereits als Module in Azure Machine Learning bereitgestellt.

MicrosoftML für Python enthält auch eine Reihe von Transformationen und Hilfsfunktionen, z. B.:

+ `rx_predict`Vorhersagen von einem trainierten Modell generiert und kann verwendet werden, für die Echtzeit-Bewertung
+ Image merkmalbereitstellung-Funktionen
+ Funktionen für die Verarbeitung und die Stimmungslage Ausdrucksextrahierung

Weitere Informationen finden Sie unter [Einführung in MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> Die Python-Community verwendet Codierungskonventionen, die möglicherweise unterscheidet, was Sie zur einschließlich alle Kleinbuchstaben und Unterstriche enthalten und nicht als Kamel-Schreibweise für Parameternamen sind. Darüber hinaus vielleicht haben Sie bemerkt, die die **Revoscalepy** Bibliothek ist immer Kleinbuchstaben. Das stimmt! Eine andere Python-Konvention.
> 
> Sehen Sie sich die Tipps für die Python-Referenzdokumentation für die Microsoft-R: [Python-Funktion Help][Python Funktionen](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>Beispiele

Sie können Code ein ausführen **Revoscalepy** Funktionen entweder lokal oder in einem remote-computekontext. Sie können auch Python in SQL Server ausführen, durch das Einbetten von Python-Code in einer gespeicherten Prozedur.

Wenn lokal ausgeführt wird, Sie in der Regel ein Python-Skript ausführen, über die Befehlszeile oder aus einer Entwicklungsumgebung Python und geben Sie einen SQL Server-computekontext mithilfe eines der der **Revoscalepy** Funktionen. Sie können die remote-computekontext für den gesamten Code oder für einzelne Funktionen verwenden. Sie möchten z. B. Auslagern modelltrainings zum Server, der die neuesten Daten verwenden und Verschieben von Daten zu vermeiden.

Wenn Sie ein vollständiges Python-Skript in der gespeicherten Prozedur platzieren möchten [Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), es wird empfohlen, die als einzelne Funktion den Code so umschreiben, die Eingaben und Ausgaben klar definiert wurde. Eingaben und Ausgaben muss **Pandas** Datenrahmen. Nachdem dies geschehen ist, können Sie rufen Sie die gespeicherte Prozedur von jedem beliebigen Client, der T-SQL unterstützt, einfach SQL-Abfragen als Eingaben übergeben und die Ergebnisse in SQL-Tabellen speichern. Ein Beispiel finden Sie unter [In-Database Python-Analyse für SQL-Entwickler](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-remote-compute-contexts"></a>Verwenden remote rechenkontexte

+ [Erstellen eines Modells mithilfe von revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md)

  In diesem Beispiel wird veranschaulicht, wie zum Ausführen von Python mit einer Instanz von SQL Server als computekontext.

### <a name="using-a-stored-procedure"></a>Verwenden von gespeicherten Prozeduren

+ [Ausführen von Python mit T-SQL](../tutorials/run-python-using-t-sql.md)

  Dieses Beispiel veranschaulicht die grundlegenden Mechanismus des Aufrufs von Python-Skript, das in einer gespeicherten Prozedur eingebettet ist.

### <a name="using-revoscalepy-with-microsoftml"></a>Verwenden von Revoscalepy mit MicrosoftML

Die Python-Funktionen für MicrosoftML integriert die rechenkontexte und Datenquellen, die in Revoscalepy bereitgestellt werden. Sie könnten daher verwenden einen Algorithmus MicrosoftML definieren und Trainieren Sie ein Modell in Python und verwenden Sie die Revoscalepy Funktionen zum Ausführen von Python-Code entweder lokal oder in einer SQl Server-computekontext.

Importieren Sie die Module in Ihrem Python-Code, und verweisen Sie auf den einzelnen Funktionen, die Sie benötigen.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>Anforderungen

Zum Ausführen von Python-Code in SQL Server muss installiert sein 2017 von SQL Server zusammen mit der Funktion **Machine Learning Services**, und die Sprache Python aktiviert. Python-Integration wird von frühere Versionen von SQL Server nicht unterstützt.

> [!NOTE]
> Python-Open Source-Distributionen unterstützt rechenkontexte für SQL Server nicht. Wenn Sie zum Veröffentlichen und Nutzen von Python-Anwendungen in Windows müssen, können Sie Microsoft Machine Learning-Server installieren, ohne Installation von SQL Server. Weitere Informationen finden Sie unter [a Standalone R Server erstellen](../r/create-a-standalone-r-server.md)

## <a name="get-more-help"></a>Weitere Hilfe

Vollständige Dokumentation für diese APIs sind verfügbar, wenn das Produkt veröffentlicht wird. In der Zwischenzeit wird empfohlen, dass Sie die entsprechende Funktion in den Bibliotheken "revoscaler" oder MicrosoftML verweisen.

+ ["Revoscaler"](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

Erhalten Sie Hilfe für eine beliebige Python-Funktion, durch Importieren des Moduls, und dem anschließenden Aufrufen `help()`. Z. B. Ausführung `help(revoscalepy)` aus Python-IDE gibt eine Liste aller Funktionen im Modul Revoscalepy mit ihren Signaturen zurück.

Bei Verwendung von Python-Tools für Visual Studio können Sie IntelliSense verwenden, um die Syntax und Argumenten Hilfe zu erhalten. Weitere Informationen finden Sie unter [Python-Unterstützung in Visual Studio](http://docs.microsoft.com/visualstudio/python/installation), und Laden Sie die Erweiterung, die Ihrer Version von Visual Studio entspricht. Sie können mit Visual Studio 2015 und 2017 Python oder früheren Versionen verwenden.

## <a name="see-also"></a>Siehe auch

[Python-Tutorials](../tutorials/sql-server-python-tutorials.md)
