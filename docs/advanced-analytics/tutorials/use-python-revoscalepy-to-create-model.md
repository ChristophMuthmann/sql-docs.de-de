---
title: Verwenden von Python mit Revoscalepy zum Erstellen eines Modells | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d886466d7bf4f0c86c1cd9505480a3fadb6e66ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>Verwenden von Python mit Revoscalepy zum Erstellen eines Modells
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In dieser Lektion erfahren Sie, wie zum Ausführen von Python-Code von einem Remotecomputer aus zum Entwickeln-Client, um ein lineares Regressionsmodell in SQL Server zu erstellen. 

## <a name="prerequisites"></a>Erforderliche Komponenten

+ In dieser Lektion verwendet unterschiedliche Daten als die vorherigen Lektionen. Sie müssen nicht zuerst die vorherigen Lektionen abgeschlossen. Jedoch wenn Sie die vorherigen Lektionen abgeschlossen haben und einen Server zum Ausführen von Python bereits konfiguriert haben, verwenden Sie dieses Servers und der Datenbank als computekontext verwenden.
+ Zum Ausführen von Python-Code mithilfe von SQL Server als einem Computer erfordert-Kontext für SQLServer 2017 oder höher. Darüber hinaus müssen Sie explizit zu installieren und aktivieren Sie das Feature "" **Machine Learning Services**, die Python-Language-Option auswählen.

    Wenn Sie eine Vorabversion von SQL Server-2017 installiert haben, sollten Sie auf mindestens die RTM-Version aktualisieren. Höhere Dienstversionen wurde erweitern und die Python-Funktionalität. Einige Funktionen dieses Lernprogramm funktionieren möglicherweise nicht in frühen Versionen vor.

+ Dieses Beispiel verwendet eine vordefinierte Python-Umgebung, mit dem Namen `PYTEST_SQL_SERVER`. Die Umgebung konfiguriert wurde, dass enthalten **Revoscalepy** und anderen erforderlichen Bibliotheken. 

    Wenn Sie keine Umgebung zum Ausführen von Python konfiguriert haben, müssen Sie dies separat tun. Eine Erläuterung zum Erstellen oder Ändern von Python-Umgebungen liegt außerhalb des gültigen Bereichs für dieses Lernprogramm. Weitere Informationen zum Einrichten von eines Python-Clients, der die richtigen Bibliotheken enthält, finden Sie unter [installieren Sie Python-Client](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) und [Link Python-Tools](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools).

## <a name="remote-compute-contexts-and-revoscalepy"></a>Remote rechenkontexte und revoscalepy

In diesem Beispiel wird veranschaulicht, wie eine Python-Modell zu erstellen, in einem _computekontext_, und Sie können Sie von einem Client aus arbeiten, aber wählen Sie eine remote-Umgebung, z. B. SQL Server, Spark oder Machine Learning-Servers, auf dem die Vorgänge werden tatsächlich ausgeführt. Verwenden rechenkontexte erleichtert es einmal Schreiben von Code und eine beliebige unterstützte Umgebung bereitgestellt.

Zum Ausführen von Python-Code in SQL Server erfordert die **Revoscalepy** Paket. Dies ist eine spezielle Python-Paket bereitgestellt von Microsoft, ähnlich wie die **"revoscaler"** -Paket für die Sprache "R". Die **Revoscalepy** Paket unterstützt die Erstellung von rechenkontexte, und bietet die Infrastruktur für die Übergabe von Daten und Modellen zwischen einer lokalen Arbeitsstation und einem Remoteserver. Die **Revoscalepy** -Funktion, die Ausführung von Code in der Datenbank wird unterstützt [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

Sie verwenden in dieser Lektion Daten in SQL Server zum Trainieren eines linearen Modells, basierend auf [Rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), eine Funktion in **Revoscalepy** , Regression sehr großer Datasets unterstützt. 

In dieser Lektion wird auch die Grundlagen zum Einrichten und verwenden Sie dann eine **SQL Server-computekontext** in Python. Nähere Informationen dazu, wie rechenkontexte mit anderen Plattformen funktionieren, und welcher Kontexten compute unterstützt werden, finden Sie unter [computekontext für die Ausführung des Skripts in Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)

## <a name="prepare-the-database-and-sample-data"></a>Vorbereiten der Daten der Datenbank und Beispiel

1. In dieser Lektion wird die Datenbank verwendet `sqlpy`. Wenn Sie keine vorherigen Lektionen abgeschlossen haben, können Sie die Datenbank erstellen, durch Ausführen des folgenden Codes:

    ```sql
    CREATE DATABASE sqlpy;
    GO
    USE sqlpy;
    GO
    ```

    > [!IMPORTANT]
    > Wenn Sie eine andere Datenbank verwenden möchten, achten Sie darauf, dass Sie die Beispielcode bearbeiten und den Datenbanknamen in der Verbindungszeichenfolge ändern.

2. Dieses Beispiel verwendet das Dataset Airline-Aktivität, die in R und Python verfügbar ist. Nachdem Sie eine Datenbank für die Python-Beispiele erstellt haben, eine Tabelle mit den Daten füllen, wie hier beschrieben: [Beispieldaten im "revoscaler"](https://docs.microsoft.com/machine-learning-server/r/sample-built-in-data).

3. Ändern Sie den Namen dieser Umgebung auf dem Client mit einer Umgebung zur Verfügung.

## <a name="run-the-sample-code"></a>Führen Sie den Beispielcode

Nachdem Sie die Datenbank vorbereitet haben, und haben, die Daten für das Training, die in einer Tabelle gespeichert eine Python-Entwicklungsumgebung zu öffnen und Ausführen des Codebeispiels.

Der Code führt die folgenden Schritte aus:

1. Importiert die erforderlichen Bibliotheken und Funktionen.
2. Erstellt eine Verbindung mit SQL Server. Erstellt **Datenquelle** Objekte für die Arbeit mit den Daten.
3. Ändert die Daten mit **Transformationen** , damit sie von den logistic Regression-Algorithmus verwendet werden kann.
4. Aufrufe `rx_lin_mod` und definiert die Formel verwendet, um das Modell passt.
5. Generiert einen Satz von Vorhersagen auf Grundlage der ursprünglichen Daten.
6. Erstellt eine Zusammenfassung, die basierend auf den vorhergesagten Werten.

Alle Vorgänge sind mit einer Instanz von SQL Server als computekontext.

> [!NOTE]
> Eine Demonstration dieses Beispiels über die Befehlszeile ausgeführt wird, finden Sie in diesem Video: [SQL Server 2017 Advanced Analytics mit Python](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>Beispielcode

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

from pandas import Categorical
import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=sqlpy;Trusted_Connection=True;'
    print("connectionString={0!s}".format(sql_connection_string))

    data_source = RxSqlServerData(
        sql_query = "select top 10 * from airlinedemosmall",
        connection_string = sql_connection_string,

        column_info = {
            "ArrDelay" : { "type" : "integer" },
            "DayOfWeek" : {
                "type" : "factor",
                "levels" : [ "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" ]
            }
        })

    sql_compute_context = RxInSqlServer(
        connection_string = sql_connection_string,
        num_tasks = 4,
        auto_cleanup = False
        )

    #
    # Run linmod locally
    #
    linmod_local = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source)
    #
    # Run linmod remotely
    #
    linmod = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)

    # Predict results
    # 
    predict = rx_predict(linmod, data = rx_import(input_data = data_source))
    summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)
```

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>Definieren einer Datenquelle im Vergleich zu definieren einen computekontext.

Eine Datenquelle unterscheidet sich von einen computekontext. Die _Datenquelle_ definiert die Daten in Ihrem Code verwendet. Die _computekontext_ definiert, in dem der Code ausgeführt wird. Allerdings verwenden einige der Informationen:

+ Python-Variablen, wie z. B. `sql_query` und `sql_connection_string`, die Quelle der Daten zu definieren. 

    Diese Variablen zum Übergeben der [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) Konstruktor zum Implementieren der **Datenquellenobjekt** mit dem Namen `data_source`.

+ Sie erstellen eine **compute Context-Objekt** mithilfe der [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata) Konstruktor. Das resultierende **compute Context-Objekt** lautet `sql_cc`.

    Dieses Beispiel verwendet die gleiche Verbindungszeichenfolge, mit denen Sie erneut in der Datenquelle, auf der Annahme, die die Daten in der gleichen SQL Server-Instanz ist, die Sie als computekontext verwenden möchten. 
    
    Allerdings können die Datenquelle und des computekontexts auf verschiedenen Servern sein.
 
### <a name="changing-compute-contexts"></a>Ändern rechenkontexte

Nachdem Sie einen computekontext definiert haben, müssen Sie festlegen der **active computekontext**. 

Wird standardmäßig die meisten Vorgänge werden lokal ausgeführt wird, d. h., wenn Sie einen anderen computekontext nicht angeben, werden die Daten aus der Datenquelle abgerufen werden und der Code in der aktuellen Python-Umgebung ausgeführt wird.

Es gibt zwei Möglichkeiten zum Festlegen des aktiven computekontexts:
+ Als Argument einer Methode oder Funktion
+ Durch Aufrufen `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Legen Sie als Argument einer Methode oder Funktion-computekontext.

In diesem Beispiel Festlegen des computekontexts mit dem Argument der einzelnen **Rx** Funktion.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Diese computekontext wird im Aufruf wiederverwendet [Rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Legen Sie einen computekontext explizit mit rx_set_compute_context

Die Funktion [Rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) können Sie zwischen wechseln von remotecomputekontexten, die bereits definiert wurden.

Nachdem Sie festgelegt haben der aktiven computekontext, bleibt aktiv, bis Sie ihn ändern.

### <a name="using-parallel-processing-and-streaming"></a>Verwenden parallele Verarbeitung und streaming

Beim Festlegen des computekontexts können Sie auch Parameter, die steuern festlegen wie die Daten von der computekontext behandelt werden. Diese Parameter variieren je nach Typ der Datenquelle.

Sie können für SQL Server-rechenkontexte legen Sie die Batchgröße oder Bereitstellen von Hinweisen zur den Grad der Parallelität in ausgeführten Aufgaben verwenden.

+ Das Beispiel auf einem Computer mit vier Prozessoren ausgeführt wurde daher das `num_tasks` Parameter auf 4 festgelegt ist, um maximale Nutzung von Ressourcen zu ermöglichen. 
+ Wenn Sie diesen Wert auf 0 festlegen, verwendet SQL Server die Standardeinstellung, die so viele Aufgaben gleichzeitig wie möglich, unter dem aktuellen MAXDOP-Einstellungen für den Server ausgeführt wird. Allerdings hängt die genaue Anzahl der Aufgaben, die möglicherweise viele andere Faktoren, z. B. Server-Einstellungen und andere Aufträge, die ausgeführt werden.

## <a name="related-samples"></a>Beispiele

Diese zusätzliche Python-Beispiele und Lernprogramme veranschaulichen End-to-End-Szenarien, die mit komplexen Datenquellen als auch die Verwendung von remote rechenkontexte.

+ [In der Datenbank Python für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md)
+ [Erstellen eines Vorhersagemodells über Python- und SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [Erstellen eines Vorhersagemodells über Python- und SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
