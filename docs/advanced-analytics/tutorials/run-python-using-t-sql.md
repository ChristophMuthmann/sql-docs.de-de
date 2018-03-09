---
title: "Ausführen von Python mit T-SQL | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 5c6145d3af6918a5f3daa954aae5522ffffebb89
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="run-python-using-t-sql"></a>Ausführen von Python mit T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Lernprogramm wird erläutert, wie Sie in SQL Server-2017 Python-Code ausführen können. Es führt Sie durch den Prozess des Verschiebens von Daten zwischen SQL Server und Python und erläutert, wie wohlgeformte Python-Code in einer gespeicherten Prozedur umschließen [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) zum Erstellen, Trainieren und Verwenden von Machine Learning-Modellen in SQL Server.

## <a name="prerequisites"></a>Erforderliche Komponenten

Um dieses Lernprogramm abzuschließen, müssen Sie zunächst installieren Sie SQL Server-2017 und Machine Learning-Dienste auf der Serverinstanz zu aktivieren, wie in beschrieben [in diesem Artikel](../python/setup-python-machine-learning-services.md). 

Sie sollten auch installieren [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Alternativ können Sie ein anderes Tool der Datenbank Management oder Abfrage, solange er Herstellen einer mit einem Server und einer Datenbank Verbindung kann, und führen Sie eine T-SQL-Abfrage oder gespeicherte Prozedur.

Nachdem Sie das Setup abgeschlossen haben, geben Sie an diesem Lernprogramm erfahren, wie zum Ausführen von Python-Code im Kontext einer gespeicherten Prozedur zurück. 

## <a name="overview"></a>Übersicht

Dieses Lernprogramm umfasst vier Lektionen:

+ Die Grundlagen des Verschiebens von Daten zwischen SQL Server und Python: erfahren Sie, die grundlegenden Anforderungen, Datenstrukturen, Eingaben und Ausgaben.
+ Üben Sie mithilfe von gespeicherten Prozeduren für einfache Python-Aufgaben, wie das Laden von Beispieldaten.
+ Gespeicherte Prozeduren verwenden, um eine Python-Machine learning-Modell zu erstellen, und Generieren von Bewertungen aus dem Modell.
+ Eine optionale Lektion für Benutzer, die von einem Remoteclient, mithilfe von SQL Server als Python ausführen möchten die _computekontext_. Enthält Code zum Erstellen eines Modells. Allerdings erfordert, dass Sie bereits einigermaßen mit Python-Umgebungen und Python-Tools vertraut sind.

Zusätzliche Python-Beispiele, die spezifisch für SQL Server-2017 sind hier bereitgestellt: [Python für SQL Server-Lernprogramme](../tutorials/sql-server-python-tutorials.md)

## <a name="verify-that-python-is-enabled-and-the-launchpad-is-running"></a>Stellen Sie sicher, dass Python aktiviert ist und das Launchpad wird ausgeführt

1. Führen Sie diese Anweisung, um sicherzustellen, dass der Dienst aktiviert wurde, in Management Studio.

    ```sql
    sp_configure 'external scripts enabled'
    ```

    Wenn **Run_value** beträgt 1, die Machine Learning-Funktion installiert und betriebsbereit ist.

    Eine häufige Ursache von Fehlern ist, dass das Launchpad, die Kommunikation zwischen SQL Server und Python verwaltet, angehalten wurde. Sie können den Launchpad-Status anzeigen, indem Sie mithilfe der Windowsfunktion **Services** Bereich aus, oder öffnen Sie SQL Server-Konfigurations-Manager. Wenn der Dienst beendet wurde, starten Sie ihn aus.

2. Als Nächstes stellen Sie sicher, dass die Python-Laufzeit arbeitet und bei der Kommunikation mit SQL Server. Zu diesem Zweck öffnen Sie ein neues **Abfrage** Fenster in SQL Server Management Studio und verbinden Sie die Instanz, die dem Python installiert wurde.

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    Wenn alles funktioniert gut, sollte eine resultierende Meldung wie die folgende angezeigt werden.

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. Wenn Fehler auftreten, gibt es eine Vielzahl von Vorgängen, die Sie ausführen können, um sicherzustellen, dass der Server und Python kommunizieren können. 

    Sie müssen die Windows-Benutzergruppe hinzufügen `SQLRUserGroup` als Anmeldung auf der Instanz, um sicherzustellen, dass das Launchpad Kommunikation zwischen Python und SQL Server bereitstellen kann. (Dieselbe Gruppe für beide R verwendet wird und Python-code ausführen.) Weitere Informationen finden Sie unter [implizite Authentifizierung aktiviert](../r/add-sqlrusergroup-to-database.md).
    
    Darüber hinaus müssen Sie zum Aktivieren von Netzwerkprotokollen, die deaktiviert wurden, oder öffnen Sie die Firewall so, dass SQL Server mit externen Clients kommunizieren kann. Weitere Informationen finden Sie unter [Problembehandlung für das Setup](../common-issues-external-script-execution.md).

## <a name="basic-python-interaction"></a>Grundlegende Python-Aktivität

Es gibt zwei Möglichkeiten zum Ausführen von Python-Code in SQL Server:

+ Fügen Sie ein Python-Skript als Argument der gespeicherten Systemprozedur, **Sp_execute_external_script**
+ Von einem Remoteclient von Python Herstellen einer Verbindung mit SQL Server, und führen Sie Code mithilfe des SQL Servers als computekontext. Dies erfordert [Revoscalepy](../python/what-is-revoscalepy.md).

Das primäre Ziel dieses Lernprogramm ist um sicherzustellen, dass Sie Python in einer gespeicherten Prozedur verwenden können.

1. Führen Sie einige einfache Code aus, um festzustellen, wie Daten zwischen SQL Server und Python hin und her übergeben werden.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. Vorausgesetzt, dass alles ordnungsgemäß eingerichtet wurden, und Python und SQL Server sind miteinander kommunizieren, das richtige Ergebnis wird berechnet, und der Python `print` Funktion gibt das Ergebnis, das die **Nachrichten** Windows.

    **Ergebnisse**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    Beim Abrufen von **"stdout"** Nachrichten ist praktisch, wenn Ihr Code testen, häufiger müssen Sie die Ergebnisse im Tabellenformat zurückgegeben werden, damit Sie es in einer Anwendung verwenden oder in einer Tabelle zu schreiben. 

Beachten Sie jetzt diese Regeln:

+ Sämtliche Inhalte innerhalb der `@script` Argument muss ein gültiger Python-Code. 
+ Das Verfolgen des Codes muss alle Pythonic Regeln hinsichtlich Einzug, Variablennamen und So weiter. Wenn Sie eine Fehlermeldung erhalten, überprüfen Sie die Leerzeichen und die Groß-/Kleinschreibung.
+ Wenn Sie alle Bibliotheken verwenden, die nicht standardmäßig geladen werden, müssen Sie eine Import-Anweisung am Anfang des Skripts verwenden, um sie zu laden. 
+ Wenn die Bibliothek nicht bereits installiert ist, beenden, und installieren Sie die Python-Paket außerhalb von SQL Server, wie hier beschrieben: [Installieren neuer Python-Pakete unter SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben

Standardmäßig [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) akzeptiert ein einzelnes Eingabedataset, die Sie in der Regel in Form einer gültigen SQL-Abfrage zu liefern. Andere Arten von Eingaben, die als SQL-Variablen übergeben werden können: beispielsweise, Sie können übergeben ein trainiertes Modells als Variable mit einem Serialisierungsfunktion wie [Engpass](https://docs.python.org/3.0/library/pickle.html) oder [Rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) schreiben Sie das Modell einem binäres Format.

Die gespeicherte Prozedur gibt eine einzelnen Python [Pandas](http://pandas.pydata.org/pandas-docs/stable/index.html) Datenrahmen als Ausgabe. Sie können jedoch skalare und Modelle als Variablen ausgeben. Sie können z. B. Ausgabe einem trainierten Modell als binäre Variable und übergeben, die für eine T-SQL-INSERT-Anweisung, dieses Modell in einer Tabelle zu schreiben. Sie können auch die Darstellungen (im binären Format) oder skalare generieren (einzelne Werte, z. B. das Datum und die Uhrzeit, die verstrichene Zeit zum Trainieren des Modells usw.).

Jetzt sehen wir uns nur die Standardeinstellung Eingabe- und Variablen `InputDataSet` und `OutputDataSet`. 

1. Führen Sie den folgenden Code aus, um einige mathematische Aufgaben und die Ergebnisse ausgeben.

        ```sql
        execute sp_execute_external_script 
        @language = N'Python', 
        @script = N'
        a = 1
        b = 2
        c = a/b
        print(c)
        OutputDataSet = c
        '
        WITH RESULT SETS ((ResultValue float))
        ```

2. Fehler auftreten, sollten abgerufen werden, da die Python-Code einen Skalar ist, nicht in einem Datenrahmen generiert.

        **Results**

        ```text
        line 43, in transform
            raise TypeError('OutputDataSet should be of type pandas.DataFrame')
        ```

3. Jetzt sehen, was geschieht, wenn Sie ein tabellarisches Dataset an Python, übergeben die Standardvariable Eingabe mit `InputDataSet`. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    Die gespeicherte Prozedur liefert eine data.frame automatisch, ohne dass Sie zusätzliche in Ihrem Python-Code keine Wirkung.

    **Ergebnisse**

    | kein Spaltenname|
    |------|
    | 1|

    Der einzelne tabellarische Eingabedataset hat standardmäßig den Namen `InputDataSet`. Sie können diese Namen jedoch ändern, indem eine Zeile wie folgt: `@input_data_1_name = N'myResultName'`.

    Von Python verwendete Spaltennamen werden nie in der Ausgabe beibehalten. Obwohl die Eingabeabfrage der Spaltenname angegeben `Col1`, diesen Namen wird nicht zurückgegeben, und alle Spaltenüberschriften, die von Ihrem Python-Skript verwendet würde. Verwenden, um eine Spalte und den Datentyp anzugeben bei der Rückgabe der Daten mit SQL Server die T-SQL `WITH RESULT SETS` Klausel.

4. Dieses Beispiel enthält die neue Namen für die Eingabe- und Variablen.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    MyOutput = MyInput
    ',
    @input_data_1_name = N'MyInput',
    @input_data_1 = N'SELECT 1 as Col1',
    @output_data_1_name = N'MyOutput'
    WITH RESULT SETS ((ResultValue int))
    ```

    Die WITH RESULT SET-Klausel definiert das Schema für die Ausgabe, da Python-Spaltennamen nie mit dem data.frame zurückgegeben werden.

    **Ergebnisse**

    | ResultValue|
    |------|
    | 1|

5. Jetzt sehen wir uns einen typischen Python-Fehler. Ändern Sie die Zeile im vorherigen Beispiel von `@input_data_1_name = N'MyInput'` auf `@input_data_1_name = N'myinput'`.

    Python-Fehler sind durch den Satelliten-Dienst von SQL Server verwendeten als Nachrichten an Sie übergeben. Nachrichten können lang sein und SQL Server-Fehlern oder Launchpad-Fehler zusätzlich zu den Python-Fehler, daher werden Patienten in untersuchen, durch den Text. Die schlüsselmeldung ist in dieser Zeile:

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    Beachten Sie, dass Python, wie R, Groß-/Kleinschreibung beachtet wird. Wenn Sie eine beliebige Art von Fehler erhalten, werden Sie prüfen die Variablennamen, und suchen Sie nach Problemen mit Datentypen, Einzug und Abstand.

## <a name="python-data-structures"></a>Python-Datenstrukturen

SQL Server abhängig von der Python **Pandas** Paket, d. h. sich hervorragend für das Arbeiten mit tabellarischen Daten. Sie haben jedoch bereits gesehen, dass Sie einen Skalarwert aus Python mit SQL Server zu übergeben und erwarten, dass "funktioniert" können nicht. In diesem Abschnitt müssen wir überprüfen, einige grundlegende Datentypdefinitionen zur Vorbereitung weitere Probleme, die Sie beim Übergeben von Tabellendaten zwischen Python und SQL Server über ausführen können.

+ Ein Datenrahmen ist eine Tabelle mit _mehrere_ Spalten.
+ Eine einzelne Spalte mit einem Datenrahmen ist eine Liste-ähnliche-Objekt, das eine Reihe aufgerufen.
+ Ein einzelner Wert ist eine Zelle von einem Datenrahmen und nach Index aufgerufen werden muss.

Wie würden Sie das einzige Ergebnis einer Berechnung als Data Frame, verfügbar machen, wenn eine data.frame tabellarischer erforderlich ist? Eine Antwort wird auf den einzelnen skalaren Wert als eine Reihe darstellen, die in einem Datenrahmen problemlos konvertiert wird. 

1. In diesem Beispiel werden einige einfache mathematische und konvertiert einen Skalar in einer Reihe. Eine Reihe erfordert einen Index, die Sie zuweisen können, wie hier gezeigt manuell oder programmgesteuert.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    s = pandas.Series(c, index =["simple math example 1"])
    print(s)
    '
    ```

2. Da die Reihen in einem data.frame konvertiert wurde noch nicht, die Werte werden im Meldungsfenster zurückgegeben, aber sehen Sie, dass die Ergebnisse in einem Tabellenformat mehr sind.

    **Ergebnisse**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Um die Länge der Reihe zu erhöhen, können Sie neue Werte hinzufügen, verwenden eines Arrays. 

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    '
    ```

    Wenn Sie einen Index nicht angeben, wird ein Index generiert mit den Werten beginnend mit 0 und endend mit der Länge des Arrays.

    **Ergebnisse**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. Wenn Sie die Anzahl der erhöhen **Index** Werte, aber keine neue hinzufügen **Daten** Werte, die Datenwerte werden wiederholt, um die Reihen auszufüllen.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    '
    ```

    **Ergebnisse**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    simple math example 2    0.5
    dtype: float64
    ```

### <a name="convert-series-to-data-frame"></a>Konvertieren von Reihen in Datenrahmen

Müssen in unsere skalare mathematischen Ergebnisse tabellarischer konvertiert, müssen wir sie in einem Format zu konvertieren, die SQL Server verarbeiten kann. 

1. Um eine Reihe in einem data.frame zu konvertieren, rufen Sie die Pandas [Datenrahmen](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) Methode.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s)
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

2. Beachten Sie, dass die Indexwerte Ausgabe werden nicht, auch wenn Sie den Index verwenden, um bestimmte Werte aus den data.frame abzurufen.

    **Ergebnisse**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>Ausgabewerte in data.frame mithilfe eines Indexes

Sehen wir uns an, wie Konvertierung in einen data.frame mit unserem zwei Reihen mit den Ergebnissen der einfache mathematische Operationen funktioniert. Die erste besitzt einen Index sequenzielle Werte, die von Python generiert. Beim zweiten wird einen beliebigen Index von Zeichenfolgenwerten verwendet.

1. In diesem Beispiel ruft einen Wert ab, aus der Reihe, die einen Ganzzahlenindex verwendet.

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s, index=[1])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    Denken Sie daran, dass der automatisch generierten Index bei 0 beginnt. Versuchen Sie es mit einem Wert außerhalb des Gültigkeitsbereichs Index, und Sie, was passiert.

2. Jetzt erhalten wir einen einzelnen Wert aus der Datenrahmen, die über einen Zeichenfolgenindex verfügt. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    **Ergebnisse**

    |ResultValue|
    |------|
    |0.5|

    Wenn Sie versuchen, einen numerischen Index verwenden, um einen Wert aus dieser Serie abzurufen, erhalten Sie eine Fehlermeldung an.

In dieser Übung sollte Ihnen eine Vorstellung zum Arbeiten mit verschiedenen Python-Datenstrukturen und stellen Sie sicher, dass das richtige Ergebnis als Data Frame zu erhalten. Sie können diese Ausgabe eines einzelnen Werts entspricht ein Datenrahmen schwieriger als seine folglich abgeschlossen haben! Glücklicherweise können Sie problemlos alle Arten von Werten in und aus der gespeicherten Prozedur als Variablen übergeben. Die in der nächsten Lektion behandelt:

## <a name="tips"></a>Tipps

+ Zwischen Programmiersprachen Python ist eine der die flexibelste im Hinblick auf einfache Anführungszeichen und doppelte Anführungszeichen. Sie sind weitgehend austauschbar. 

    T-SQL verwendet jedoch einfache Anführungszeichen für die nur bestimmte Aspekte, und die `@script` Argument verwendet einfache Anführungszeichen zum Einschließen von Python-Code als Unicode-Zeichenfolge. Aus diesem Grund müssen Sie möglicherweise überprüfen den Python-Code, und ändern einige einfache Anführungszeichen in doppelte Anführungszeichen.

+ Die gespeicherte Prozedur wurde nicht gefunden `sp_execute_external_script`? Dies bedeutet, dass Sie wahrscheinlich noch nicht abgeschlossen Konfigurieren der Instanz zur Unterstützung von externen skriptausführung. Nach dem 2017 von SQL Server-Setup ausführen und Python als Machine learning Sprache auswählen, müssen Sie auch ausdrücklich aktivieren die Funktion mit `sp_configure`, und klicken Sie dann die Instanz neu gestartet. 

    Weitere Informationen finden Sie unter [Setup Machine Learning-Dienste mit Python](../python/setup-python-machine-learning-services.md).

## <a name="next-steps"></a>Nächste Schritte

[Umschließen von Python-Code in eine gespeicherte SQL-Prozedur](wrap-python-in-tsql-stored-procedure.md)