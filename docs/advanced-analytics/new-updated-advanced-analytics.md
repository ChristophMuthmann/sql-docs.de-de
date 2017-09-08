---
title: "Aktualisiert – Advanced Analytics für SQL Server-Dokumentation | Microsoft Docs"
description: "Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation für Advanced Analytics für Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/17/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79f979ecda1ff0851978d19ef28fa3cf909f9a43
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Neue und kürzlich aktualisierte: Advanced Analytics für SQLServer



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates*: &nbsp; **23.5.2017** &nbsp; -bis- &nbsp; **17.7.2017**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Advanced Analytics für SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Häufige Probleme mit der externen Skriptausführung](common-issues-external-script-execution.md)
2. [Die Datensammlung für die Problembehandlung von Machine Learning](data-collection-ml-troubleshooting-process.md)
3. [Lernprogramme für SQL Server-Python](tutorials/sql-server-python-tutorials.md)
4. [Lernprogramme für SQL Server R](tutorials/sql-server-r-tutorials.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>1. &nbsp;[Revoscalepy Einführung](python/what-is-revoscalepy.md)

*Aktualisiert: 23.6.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 112.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cab7330ac9944508aaa360e00cbc2e866455776d 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a  (PR=2171  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**Verwenden von Revoscalepy mit MicrosoftML**


Die Python-Funktionen für MicrosoftML integriert die rechenkontexte und Datenquellen, die in Revoscalepy bereitgestellt werden. Sie könnten daher verwenden einen Algorithmus MicrosoftML definieren und Trainieren Sie ein Modell in Python und verwenden Sie die Revoscalepy Funktionen zum Ausführen von Python-Code entweder lokal oder in einer SQl Server-computekontext.

Importieren Sie die Module in Ihrem Python-Code, und verweisen Sie auf den einzelnen Funktionen, die Sie benötigen.

```
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**Anforderungen**


Zum Ausführen von Python-Code in SQL Server muss installiert sein 2017 von SQL Server zusammen mit der Funktion **Machine Learning Services**, und die Sprache Python aktiviert. Python-Integration wird von frühere Versionen von SQL Server nicht unterstützt.

> [!NOTE]
> Python-Open Source-Distributionen unterstützt rechenkontexte für SQL Server nicht. Wenn Sie zum Veröffentlichen und Nutzen von Python-Anwendungen in Windows müssen, können Sie Microsoft Machine Learning-Server installieren, ohne Installation von SQL Server. Weitere Informationen finden Sie unter [Erstellen einer eigenständigen R Server--... /r/Create-a-Standalone-r-Server.MD)

**Weitere Hilfe**





&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-step-5-train-and-save-a-model-using-t-sqltutorialssqldev-py5-train-and-save-a-model-using-t-sqlmd"></a>2. &nbsp;[Schritt 5: Schulen und speichern Sie ein Modell mithilfe des T-SQL](tutorials/sqldev-py5-train-and-save-a-model-using-t-sql.md)

*Aktualisiert: 2017-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 121.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c1cbe92282b96105ffdb69efa803f58dc0ac7e2 e4077a2154a90de468c435efa5b2225125d5b0e7  (PR=1904  ,  Filename=sqldev-py5-train-and-save-a-model-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



1. In [! INCLUDE [SsManStudio--... /.. /Includes/ssmanstudio-MD.MD)], öffnen Sie ein neues Abfragefenster, und führen Sie die folgende Anweisung zum Erstellen der gespeicherten Prozedur _TrainTipPredictionModelRxPy_.  Dieses Modell wird auf die Trainingsdaten basieren, die Sie soeben vorbereitet. Da die gespeicherte Prozedur, die bereits eine Definition der Eingabedaten enthält, müssen Sie eine Eingabeabfrage bereitstellen.

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    ```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-step-6-operationalize-the-modeltutorialssqldev-py6-operationalize-the-modelmd"></a>3. &nbsp;[Schritt 6: das Modell Operationalisieren](tutorials/sqldev-py6-operationalize-the-model.md)

*Aktualisiert: 2017-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_2) | [Weiter](#TitleNum_4))

<!-- Source markdown line 236.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1eb50ac902d4e80bafb1dd7fdf8f607dcdf0d33f 57d5abdc6119db1ecd81587d625054a5bbfb5fc8  (PR=1904  ,  Filename=sqldev-py6-operationalize-the-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



Hier ist die Definition der gespeicherten Prozedur, der ausführt, Bewertung mithilfe der **Revoscalepy** Modell.

```
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures-- 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
```




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>4. &nbsp;[Verwenden von Python mit Revoscalepy zum Erstellen eines Modells](tutorials/use-python-revoscalepy-to-create-model.md)

*Aktualisiert: 2017-06-21* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_3))

<!-- Source markdown line 119.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0886939f86fe12d7ff7b339689a02c7fc75e0786 23dd469349a05d535063aab3c14aec152ed2cd7b  (PR=2141  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=76839e39427e24688609353b8708d59fee772d28) -->



**Überprüfen Sie den code**


Nehmen wir den Code überprüfen, und markieren Sie einige wichtige Schritte.

**Definieren eine Datenquelle aus, und computekontext**


Dies ist ein wichtiger Teil der Verwendung von **Revoscalepy** und seine zugehörigen R-Paket **"revoscaler"**. Eine Datenquelle unterscheidet sich von einen computekontext. Die _Datenquelle_ definiert die Daten in Ihrem Code verwendet. Die _computekontext_ definiert, in dem der Code ausgeführt wird.

> [!NOTE]
> Unterstützung für einige Datenquellentypen unterstützt in "revoscaler" kann in der Vorabversion beschränkt sein. Weitere Informationen zu Funktionen, die in der neuesten Version enthalten finden Sie unter [was Revoscalepy--ist... /Python/What-is-revoscalepy.MD).

Die gesamte zum Erstellen und verwenden eine Datenquelle verarbeitet und compute-Kontext wie folgt lautet:

1. Erstellen Sie die Python-Variablen, z. B. _SqlQuery_ und _"ConnectionString"_, die definiert, die Quelle und die Daten, die Sie verwenden möchten. Diese Variablen zum Übergeben der **RxSqlServerData** Konstruktor zum Implementieren der **Datenquellenobjekt** mit dem Namen _DataSource_.
2. Erstellen Sie eine Compute Context-Objekt mithilfe der **RxInSqlServer** Konstruktor. In diesem Beispiel übergeben Sie dieselbe Verbindungszeichenfolge, die Sie zuvor auf der Annahme definiert, die die Daten in der gleichen SQL Server-Instanz ist, die Sie als computekontext verwenden möchten. Allerdings können die Datenquelle und des computekontexts auf verschiedenen Servern sein. Das resultierende **compute Context-Objekt** lautet _ComputeContext_.
3. Wählen Sie den aktiven computekontext. Standardmäßig Vorgänge werden lokal ausgeführt wird, d. h., wenn Sie einen anderen computekontext nicht angeben, werden die Daten aus der Datenquelle abgerufen werden und das Modell Anpassung wird in der aktuellen Python-Umgebung ausgeführt.

    Im "revoscaler", können Sie auch mithilfe der Funktion `rxSetComputeContext` zwischen rechenkontexte zu wechseln. Die Funktion ist noch nicht implementiert in der Preview-Version von **Revoscalepy**, aber Sie können die computekontext angeben, als Argument an **Rx_lin_mod_ex**.





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>Ähnliche Artikel

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen, innerhalb des gleichen GitHub-Repository: [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [New + Updated (4+4): **Advanced Analytics for SQL** docs (Neu + Aktualisiert (4+4): Dokumentation zu Erweiterten Analytics für SQL)](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (2+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (2+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (1+2): **Connect to SQL** docs (Neu + Aktualisiert (1+2): Dokumentation zur Herstellung einer Verbindung mit SQL)](../connect/new-updated-connect.md)
- [New + Updated (6+0): **Database Engine for SQL** docs (Neu + Aktualisiert (6+0): Dokumentation zum Datenbankmodul für SQL)](../database-engine/new-updated-database-engine.md)
- [New + Updated (13+2): **Linux for SQL** docs (Neu + Aktualisiert (13+2): Dokumentation zu Linux für SQL)](../linux/new-updated-linux.md)
- [New + Updated (1+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (1+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (1+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (1+0): Dokumentation zur Open Database Connectivity für SQL)](../odbc/new-updated-odbc.md)
- [New + Updated (8+4): **Relational Databases for SQL** docs (Neu + Aktualisiert (8+4): Dokumentation zu relationalen Datenbanken für SQL)](../relational-databases/new-updated-relational-databases.md)
- [New + Updated (2+2): **Microsoft SQL Server** docs (Neu + Aktualisiert (2+2): Dokumentation zu Microsoft SQL Server)](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+1): **SQL Server Management Studio (SSMS)** docs (Neu + Aktualisiert (0+1): Dokumentation zu SQL Server Management Studio (SSMS))](../ssms/new-updated-ssms.md)
- [New + Updated (1+0): **Transact-SQL** docs (Neu + Aktualisiert (1+0): Dokumentation zu Transact-SQL)](../t-sql/new-updated-t-sql.md)
- [New + Updated (1+0): **Tools for SQL** docs (Neu + Aktualisiert (1+0): Dokumentation zu Tools für SQL)](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Integration Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu SSIS für SQL)](../integration-services/new-updated-integration-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Reporting Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Reporting Services für SQL)](../reporting-services/new-updated-reporting-services.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+0): Dokumentation zu SQL Server Data Tools (SSDT))](../ssdt/new-updated-ssdt.md)
- [New + Updated (0+0): **SQL Server Migration Assistant (SSMA)** docs (Neu + Aktualisiert (0+0): SQL Server Migration Assistant-Dokumente (SSMA))](../ssma/new-updated-ssma.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


&nbsp;


