---
title: Verwenden von R-Funktionen mit SQL Server-Daten (R in SQL-Schnellstart) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 226712010118a54ac1c5350e128bf50cc261a128
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-r-functions-with-sql-server-data-r-in-sql-quickstart"></a>Verwenden von R-Funktionen mit SQL Server-Daten (R in SQL-Schnellstart)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Da Sie nun mit grundlegenden Vorgängen vertraut sind, ist es an der Zeit, R richtig zu nutzen. Zum Beispiel sind viele erweiterte statistische Funktionen mit T-SQL möglicherweise schwierig zu implementieren, erfordern jedoch nur eine einzige Zeile R-Code.  Mit R Services ist es einfach, Skripts für R-Hilfsprogramme in eine gespeicherte Prozedur einzubetten.

In diesen Beispielen werden Sie mathematische R-Funktionen und R-Hilfsfunktionen in eine gespeicherte SQL Server-Prozedur einbetten.

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>Erstellen einer gespeicherten Prozedur zum Generieren von Zufallszahlen

Der Einfachheit halber verwenden wir die R `stats` Paket, das installiert wird und standardmäßig mit R-Services geladen werden. Das Paket enthält Hunderte von Funktionen für allgemeine statistische Aufgaben, darunter die `rnorm`-Funktion, die eine bestimmte Anzahl von Zufallszahlen mithilfe der normalen Verteilung bei angegebener Standardabweichung und Mittelwert generiert.

Bei einer Standardabweichung von 3 gibt dieser R-Code beispielsweise 100 Zahlen mit einem Mittelwert von 50 zurück.

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

Führen Sie zum Aufrufen dieser R-Zeile von T-SQL sp_execute_external_script aus, und fügen Sie die R-Funktion wie folgt im R-Skriptparameter hinzu:

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

Sie möchten es vereinfachen, einen anderen Satz von Zufallszahlen zu generieren?

Das ist ganz einfach in Kombination mit SQL Server: Definieren Sie eine gespeicherte Prozedur, die die Argumente des Benutzers abruft. Übergeben Sie dann diese Argumente als Variablen an das R-Skript.

```sql
CREATE PROCEDURE MyRNorm (@param1 int, @param2 int, @param3 int)
AS
    EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
    WITH RESULT SETS (([Density] float NOT NULL));
```

+ Die erste Zeile definiert alle SQL-Eingabeparameter, die erforderlich sind, wenn die gespeicherte Prozedur ausgeführt wird.

+ Die Zeile, die mit `@params` beginnt, definiert alle vom R-Code verwendeten Variablen und die entsprechenden SQL-Datentypen.

+ Die unmittelbar folgenden Zeilen ordnen die SQL-Parameternamen den entsprechenden R-Variablennamen zu.

Nun haben Sie die R-Funktion in einer gespeicherten Prozedur eingeschlossen und können sie ganz einfach aufrufen und ihr andere Werte übergeben:

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="related-resources"></a>Verwandte Ressourcen

+ Möchten Sie weitere R-Pakete installieren, statistische Funktionen, um mehr erhalten erweiterte? Finden Sie unter [installieren und Verwalten von R-Paketen](../r/installing-and-managing-r-packages.md).

+ Damit können den eigenständigen R-Code in ein Format zu konvertieren, die leicht mit SQL Server gespeicherte Prozeduren parametrisiert werden können, hat das Team von Microsoft R ein neues R-Paket bereitgestellt **Sqlrutils**. Weitere Informationen finden Sie unter [zum Erstellen einer gespeicherten Prozedur mithilfe von Sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md).

## <a name="use-r-utility-functions-for-troubleshooting"></a>Verwenden von R-Hilfsfunktionen für die Problembehandlung

Eine Installation von R enthält standardmäßig den `utils` Paket, das eine Vielzahl von Hilfsfunktionen zum Untersuchen der aktuellen R-Umgebung bereitstellt. Dies kann nützlich sein, wenn Sie bei der Ausführung Ihres R-Codes in SQL Server und externen Umgebungen Diskrepanzen feststellen.

Sie können zum Beispiel die R-`memory.limit()`-Funktion verwenden, um Arbeitsspeicher für die aktuelle R-Umgebung abzurufen. Da das `utils`-Paket standardmäßig installiert, aber nicht geladen wird, müssen Sie es zuerst mit der `library()`-Funktion laden.

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        mymemory <- memory.limit();
        OutputDataSet <- as.data.frame(mymemory);'
    , @input_data_1 = N' ;'
WITH RESULT SETS (([Col1] int not null));
```

Viele Benutzer in der zeitlichen Steuerung Systemfunktionen in R, z. B. wie `system.time` und `proc.time`, zum Erfassen der Zeit, die von R-Prozessen verwendet wird und Leistungsprobleme analysieren.

Ein Beispiel finden Sie im Tutorial [Erstellen von Datenfunktionen](../tutorials/walkthrough-create-data-features.md). In dieser exemplarischen Vorgehensweise werden R-Funktionen zur zeitlichen Steuerung in die Lösung eingebettet, um die Leistung von zwei Methoden zum Erstellen von Funktionen aus Daten zu vergleichen: R-Funktionen und T-SQL-Funktionen.

## <a name="next-lesson"></a>Nächste Lektion

Als Nächstes erstellen Sie mithilfe von R in SQL Server ein Vorhersagemodell.

[Erstellen eines Vorhersagemodells](../tutorials/rtsql-create-a-predictive-model-r.md)
