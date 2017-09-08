---
title: Verwenden von Python mit Revoscalepy zum Erstellen eines Modells | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6b7e166971ff74add56bce628838c82a9a6c1128
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>Verwenden von Python mit Revoscalepy zum Erstellen eines Modells

In diesem Beispiel wird veranschaulicht, wie ein Logistisches Regressionsmodell in SQL Server mithilfe eines Algorithmus aus können die **Revoscalepy** Paket.

Die **Revoscalepy** -Paket für Python-Objekte, Transformationen enthält und Algorithmen, die ähnliche aus Gründen der **"revoscaler"** -Paket für die Sprache "R". Mit dieser Bibliothek können Sie einen computekontext erstellen, Verschieben von Daten zwischen remotecomputekontexten, Transformieren von Daten und Vorhersagemodellen mit gängigen Algorithmen wie z. B. logistische und lineare Regression und Entscheidungsstrukturen zu trainieren.

Weitere Informationen finden Sie unter [was Revoscalepy ist?](../python/what-is-revoscalepy.md)

## <a name="prerequisites"></a>Erforderliche Komponenten

> [!IMPORTANT]
> Zum Ausführen von Python-Code in SQL Server muss installiert sein CTP für SQL Server 2017 2.0 oder höher, und müssen Sie installieren und aktivieren Sie das Feature "" **Machine Learning Services** mit Python. Integration von Python unterstützt andere Versionen von SQL Server nicht.

## <a name="run-the-sample-code"></a>Führen Sie den Beispielcode

Dieser Code führt die folgenden Schritte aus:

1. Importiert die erforderlichen Bibliotheken und Funktionen
2. Erstellt eine Verbindung mit SQL Server und Datenquellenobjekte zum Arbeiten mit den Daten erstellt
3. Ändert die Daten, sodass es von den logistic Regression-Algorithmus verwendet werden kann
4. Aufrufe `rx_lin_mod` und definiert die Formel verwendet, um das Modell passt.
5. Generiert eine Reihe von Vorhersagen auf Grundlage des ursprünglichen Datasets
6. Erstellt eine Zusammenfassung, die basierend auf den vorhergesagten Werten

Alle Vorgänge sind mit einer Instanz von SQL Server als computekontext.

Im Allgemeinen ist der Prozess der aufrufenden Python in einen remote-computekontext ähnlich wie bei der Verwendung von R in einen remote-computekontext. Führen Sie das Beispiel als ein Python-Skript über die Befehlszeile oder mithilfe einer Python-Entwicklungsumgebung, die die bereitgestellten Python-Integrationskomponenten in dieser Version enthält. In Ihrem Code erstellen und verwenden eine Compute Context-Objekt, um anzugeben, wo bestimmte Berechnungen ausgeführt werden soll.

> [!NOTE]
> Achten Sie darauf, dass die Datenbank und die Umgebung Namen nach Bedarf ändern.
> 
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
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=PyTestDb;Trusted_Connection=True;'
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

## <a name="discussion"></a>Erläuterung

Nehmen wir den Code überprüfen, und markieren Sie einige wichtige Schritte.

### <a name="defining-a-data-source-and-compute-context"></a>Definieren eine Datenquelle aus, und computekontext

Eine Datenquelle unterscheidet sich von einen computekontext. Die _Datenquelle_ definiert die Daten in Ihrem Code verwendet. Die _computekontext_ definiert, in dem der Code ausgeführt wird.

1. Erstellen Sie die Python-Variablen, z. B. `sql_query` und `sql_connection_string`, die definiert, die Quelle und die Daten, die Sie verwenden möchten. Diese Variablen dann an den Konstruktor RxSqlServerData implementieren übergeben der **Datenquellenobjekt** mit dem Namen `data_source`.
2. Erstellen Sie eine Compute Context-Objekt mithilfe der **RxInSqlServer** Konstruktor. In diesem Beispiel übergeben Sie dieselbe Verbindungszeichenfolge, die Sie zuvor auf der Annahme definiert, die die Daten in der gleichen SQL Server-Instanz ist, die Sie als computekontext verwenden möchten. Allerdings können die Datenquelle und des computekontexts auf verschiedenen Servern sein. Das resultierende **compute Context-Objekt** lautet `sql_cc`.
3. Wählen Sie den aktiven computekontext. Standardmäßig Vorgänge werden lokal ausgeführt wird, d. h., wenn Sie einen anderen computekontext nicht angeben, werden die Daten aus der Datenquelle abgerufen werden und das Modell Anpassung wird in der aktuellen Python-Umgebung ausgeführt.

### <a name="changing-compute-contexts"></a>Ändern rechenkontexte

In diesem Beispiel Festlegen des computekontexts mit dem Argument der einzelnen **Rx** Funktion.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Das gleiche gilt, in dem Aufruf von **Rxsummary**, wobei computekontext wiederverwendet wird.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

Sie können auch mithilfe der Funktion **Rxsetcomputecontext** zwischen rechenkontexte zu wechseln, die bereits definiert wurden. 

### <a name="setting-the-degree-of-parallelism"></a>Den Grad an Parallelität festlegen

Beim Festlegen des computekontexts können Sie auch Parameter, die steuern festlegen wie die Daten von der computekontext behandelt werden. Diese Parameter variieren je nach Typ der Datenquelle. 

Sie können für SQL Server-rechenkontexte legen Sie die Batchgröße oder Bereitstellen von Hinweisen zur den Grad der Parallelität in ausgeführten Aufgaben verwenden.

Das Beispiel auf einem Computer mit vier Prozessoren ausgeführt wurde, damit wir setzen die *Num_tasks* Parameter 4. Wenn Sie diesen Wert auf 0 festlegen, verwendet SQL Server die Standardeinstellung, die so viele Aufgaben gleichzeitig wie möglich, unter dem aktuellen MAXDOP-Einstellungen für den Server ausgeführt wird. Hängt jedoch auch auf Servern mit vielen Prozessoren, die genaue Anzahl der Aufgaben, die möglicherweise viele andere Faktoren, z. B. Server-Einstellungen und andere Aufträge, die ausgeführt werden. 

Weitere Informationen finden Sie unter [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver).

## <a name="related-samples"></a>Beispiele

Diese Python-Beispiele und Lernprogramme für erweiterte Tipps und End-to-End-Demos angezeigt.

+ [In der Datenbank Python für SQL-Entwickler](sqldev-in-database-python-for-sql-developers.md)
+ [Erstellen eines Vorhersagemodells über Python- und SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [Bereitstellen und Nutzen von Python-Modelle](../python/publish-consume-python-code.md)

