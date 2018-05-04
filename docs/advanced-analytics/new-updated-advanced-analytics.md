---
title: Aktualisiert – Advanced Analytics für SQL Server-Dokumentation | Microsoft Docs
description: Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation für Advanced Analytics für Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: advanced-analytics
ms.date: 04/28/2018
ms.openlocfilehash: bbce32579b54647e167c25d2708a80027ae0e678
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Neue und kürzlich aktualisierte: Advanced Analytics für SQLServer



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2018-02-03** &nbsp; - zu - &nbsp; **2018-04-28**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Advanced Analytics für SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Installieren von SQL Server 2017 Machine Learning-Services (Datenbankintern) unter Windows](install/sql-machine-learning-services-windows-install.md)
2. [Installieren von SQL Server 2017 Machine Learning-Server (eigenständig) unter Windows](install/sql-machine-learning-standalone-windows-install.md)
3. [Installieren von SQL Server-Machine Learning-Komponenten über die Befehlszeile](install/sql-ml-component-commandline-install.md)
4. [Installieren von SQL Server-Machine learning-Komponenten ohne Internetzugang](install/sql-ml-component-install-without-internet-access.md)
5. [Installieren von SQL Server 2016 R Services (Datenbankintern)](install/sql-r-services-windows-install.md)
6. [Installieren von SQL Server 2016 R Server (eigenständig)](install/sql-r-standalone-windows-install.md)
7. [Einrichten von Python-Clienttools für die Verwendung mit SQL Server-Machine Learning](python/setup-python-client-tools-sql.md)
8. [Verwenden Sie Python-Modell in SQL zum Trainieren und bewerten](tutorials/train-score-using-python-in-tsql.md)
9. [Python-Code in einer gespeicherten Prozedur umschließen](tutorials/wrap-python-in-tsql-stored-procedure.md)
10. [Was sind SQL Server-Machine Learning Services?](what-is-sql-server-machine-learning.md)
11. [Erweiterte Ereignisse für die Überwachung von PREDICT-Anweisungen](xe-event-predict-tsql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Anzeigen von R oder Python-Pakete, die auf SQL Server installiert](#TitleNum_1)
2. [Installieren Sie Pre-tained Machine learning-Modelle mit SQL Server](#TitleNum_2)
3. [Einrichten eines Data Science-Clients für die Entwicklung von R in SQL Server](#TitleNum_3)
4. [SQLServer Machine Learning und R Services (Datenbankintern)](#TitleNum_4)
5. [Ausführen von Python mit T-SQL](#TitleNum_5)
6. [Verwenden von Python mit Revoscalepy zum Erstellen eines Modells](#TitleNum_6)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-viewing-r-or-python-packages-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>1. &nbsp; [Anzeigen von R oder Python-Pakete, die auf SQL Server installiert](r/determine-which-packages-are-installed-on-sql-server.md)

*Aktualisiert: 2018-04-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 208.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f ec6859ac91b27539dc36f21aec82c99937c0187a  (PR=5610  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f1f96a990644c0d6cfa5a1d88ccee959cab6c2b2) -->



**Python**


In diesem Beispiel gibt die Liste der Ordner für die Python `sys.path` Variable. Die Liste enthält das aktuelle Verzeichnis und den Pfad der Standardbibliothek.

```
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**Ergebnisse**

```
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

Weitere Informationen zu den Variablen `sys.path` und wie sie zum Festlegen der Interpreter Suchpfad für Module verwendet wird, finden Sie unter der [Python-Dokumentation](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-install-pre-trained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>2. &nbsp; [Installieren Sie Pre-tained Machine learning-Modelle mit SQL Server](r/install-pretrained-models-sql-server.md)

*Aktualisiert: 2018-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 140.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 aa03623d819750d4919feb7910b07ec1875bb509 7382228fa68b04b500a5fde73c29995e12aa20ac  (PR=5504  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



1. Starten Sie den separaten Windows-basierten Installer entweder [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) oder [Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Wählen Sie die Sprachen, die Sie verwenden möchten, aktualisieren, und wählen Sie die **Pre-trained Modelle** Option.

    > [!TIP]
    > Wenn Sie zuvor ausgeführt, haben die Installer zum Aktualisieren von R Server (eigenständig), und nur die Pre-tained Modelle hinzufügen möchten, lassen Sie alle vorherigen Auswahl **als**, und wählen Sie nur am vorkonfigurierten **-Modelle trainiert** Option . **Nicht** deaktivieren Sie alle zuvor ausgewählten Optionen; in diesem Fall wird das Installationsprogramm Komponenten entfernt.

    Es wird empfohlen, dass Sie die Standardeinstellungen für die Modell-Speicherorte akzeptieren.

3. Klicken Sie auf **Weiter**.

4. Akzeptieren Sie alle anderen aufforderungen, einschließlich der Lizenzverträge.

Nachdem die Installation abgeschlossen ist, müssen Sie einige zusätzliche Schritte zum Registrieren der vorab trainierten Modelle ausführen.

1. Öffnen Sie Windows-Eingabeaufforderung **als Administrator**.

2. Navigieren Sie zu dem Ordner "Setup bootstrap", für R Server (eigenständig), die auch vom Microsoft-R-Installationsprogramm enthält.

3. Führen Sie `RSetup.exe` und geben Sie an die Komponente zu installieren, die Version und den Ordner, der der Quelldateien für das Modell mithilfe dieser Syntax enthält:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    Die folgenden Werte sind für den "Version"-Parameter unterstützt:



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-set-up-a-data-science-client-for-r-development-on-sql-serverrset-up-a-data-science-clientmd"></a>3. &nbsp; [Einrichten eines Data Science-Clients für die Entwicklung von R in SQL Server](r/set-up-a-data-science-client.md)

*Aktualisiert: 2018-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_2) | [Weiter](#TitleNum_4))

<!-- Source markdown line 39.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0583f8febcedc5dc2e14ca1a8073ca204ca37987 3d50ad8f35f2985944741a9b2211a461df2c13e4  (PR=5504  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



**R-tools**


Bei der Installation von R mit SQL Server erhalten Sie dieselben R-Tools, die mit allen installiert sind **Basis** Installation von R, wie z. B. Rterm, "rgui.exe" und So weiter. Technisch gesehen, müssen Sie daher alle Tools, die Sie zum Entwickeln und Testen von R-Code erforderlich.

Die folgenden standard-R-Tools sind in enthalten eine *basieren Installation* von R, und daher standardmäßig installiert sind.

+ **RTerm**: eine Befehlszeilen Terminaldienste zum Ausführen von R-Skripts

+ **RGui.exe**: einen einfachen interaktiven Editor für R. Die Befehlszeilenargumente sind identisch für RGui.exe und RTerm.

+ **RScript**: ein Befehlszeilentool zum Ausführen von R-Skripts im Batchmodus.

Um diese Tools zu suchen, ermitteln Sie die R-Bibliothek, die beim Einrichten von SQL Server oder das eigenständige-Machine learning-Funktion installiert wurde. Z. B. in einer Standardinstallation der R-Tools in diesen Ordnern befinden sich:

+ SQL Server 2016-R-Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server eigenständige: `~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 2017 Machine Learning-Dienste: `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ Machine Learning-Server (eigenständig): `~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

Wenn Sie Hilfe bei der R-Tools benötigen, öffnen Sie einfach **"rgui.exe"**, klicken Sie auf **Hilfe**, und wählen Sie eine der Optionen

**Microsoft R Client**


Microsoft R-Client ist kostenlos, das Ihnen den Zugriff auf die "revoscaler"-Pakete für die Verwendung der Entwicklung bietet. Indem Sie R-Client installieren, können Sie R-Lösungen erstellen, die in allen unterstützten rechenkontexte, einschließlich SQL Server in der Datenbank Analytics und verteilte R Datenverarbeitung auf Hadoop, Spark oder Linux verwenden Machine Learning-Server ausgeführt werden können.

Wenn Sie eine andere R-Entwicklungsumgebung bereits installiert haben wie RStudio, achten Sie neu konfigurieren, die Umgebung, verwenden Sie die Bibliotheken und ausführbaren Dateien von Microsoft R-Client bereitgestellt wird. Indem Sie auf diese Weise, sodass Sie alle Funktionen von der "revoscaler"-Paket verwenden können, obwohl die Leistung beschränkt sind.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-sql-server-machine-learning-and-r-services-in-databasersql-server-r-servicesmd"></a>4. &nbsp; [SQLServer Machine Learning und R Services (Datenbankintern)](r/sql-server-r-services.md)

*Aktualisiert: 2018-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_3) | [Weiter](#TitleNum_5))

<!-- Source markdown line 83.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b1a95a7f6d391a518762eb271e8ea7e0d684d403 7fbfabf62917e03e2bcb99d297e1c9d0f0604440  (PR=5504  ,  Filename=sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



Wählen Sie die beste Sprache für den Task aus. R ist am besten für statistische Berechnungen, die schwierig zu implementieren, verwenden SQL sind. Für setbasierte Vorgänge für Daten, nutzen die Leistungsfähigkeit des *{eingeschlossene-Inhalt-sinkt-Here}* um optimale Leistung zu erzielen. Verwenden Sie das in-Memory-Datenbankmodul für sehr schnelle Berechnungen über Spalten.

**Schritt 4: Optimieren Sie Ihre Lösung**


Wenn das Modell für die Skalierung auf Enterprise-Daten ist, funktioniert der Data Scientist oft mit dem Datenbankadministrator oder der SQL-Entwickler Prozesse wie z. B. zu optimieren:

+ Featureentwicklung
+ Als "Erfassung" Daten und die Datentransformation
+ Bewertung

Bisher mussten Datenanalysten verwenden R Probleme mit der Leistung und Skalierung, insbesondere wenn Sie große Datasets verwendet. Das liegt daran Implementierung des allgemeinen Laufzeitmoduls nur einen einzelnen Thread und nur die Datasets, die in den verfügbaren Arbeitsspeicher auf dem lokalen Computer entsprechen aufnehmen kann. Integration mit SQl Server-Machine Learning-Services stellt mehrere Funktionen für eine bessere Leistung, mehr Daten bereit:

+ **"Revoscaler"**: Diese R-Paket enthält die Implementierung einiger der beliebtesten R-Funktionen neu gestaltet, um die Parallelität und Skalierung bereitzustellen. Das Paket enthält auch Funktionen, die Leistung und Skalierung weiter steigern, indem Sie Berechnungen zum Übertragen der *{eingeschlossene-Inhalt-sinkt-Here}* Computer, die in der Regel wesentlich mehr Arbeitsspeicher und rechenleistung verfügt.

+ **Revoscalepy**. Diese Python-Clientbibliothek in SQL Server 2017 implementiert die am häufigsten verwendeten Funktionen im "revoscaler", z. B. remote rechenkontexte, und viele Algorithmen, die unterstützt verteilte Verarbeitung.

**Ressourcen**

+ [Leistung Fallstudie]
+ [R und Datenoptimierung]

**Schritt 5: Bereitstellen und nutzen**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-run-python-using-t-sqltutorialsrun-python-using-t-sqlmd"></a>5. &nbsp; [Ausführen von Python mit T-SQL](tutorials/run-python-using-t-sql.md)

*Aktualisiert: 2018-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_4) | [Weiter](#TitleNum_6))

<!-- Source markdown line 306.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bde8c6476df259d225847c08224cefd02f3529d5 cad56997abe7928b588ac4a0302384c5edc1ede5  (PR=5497  ,  Filename=run-python-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



2. Beachten Sie, dass die Indexwerte Ausgabe werden nicht, auch wenn Sie den Index verwenden, um bestimmte Werte aus den data.frame abzurufen.

    **Ergebnisse**

    |ResultValue|
    |------|
    |0.5|
    |2|

**Ausgabewerte in data.frame mithilfe eines Indexes**


Sehen wir uns an, wie Konvertierung in einen data.frame mit unserem zwei Reihen mit den Ergebnissen der einfache mathematische Operationen funktioniert. Die erste besitzt einen Index sequenzielle Werte, die von Python generiert. Beim zweiten wird einen beliebigen Index von Zeichenfolgenwerten verwendet.

1. In diesem Beispiel ruft einen Wert ab, aus der Reihe, die einen Ganzzahlenindex verwendet.

```
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

```
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



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>6. &nbsp; [Verwenden von Python mit Revoscalepy zum Erstellen eines Modells](tutorials/use-python-revoscalepy-to-create-model.md)

*Aktualisiert: 2018-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_5))

<!-- Source markdown line 22.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5b642b391ca571412c30c8470875d3d4d3c57246 bd83387eb8a1076a1396bbd48dca12872843aa2f  (PR=5497  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



Wenn Sie eine Vorabversion von SQL Server-2017 installiert haben, sollten Sie auf mindestens die RTM-Version aktualisieren. Höhere Dienstversionen wurde erweitern und die Python-Funktionalität. Einige Funktionen dieses Lernprogramm funktionieren möglicherweise nicht in frühen Versionen vor.

+ Dieses Beispiel verwendet eine vordefinierte Python-Umgebung, mit dem Namen `PYTEST_SQL_SERVER`. Die Umgebung konfiguriert wurde, dass enthalten **Revoscalepy** und anderen erforderlichen Bibliotheken.

    Wenn Sie keine Umgebung zum Ausführen von Python konfiguriert haben, müssen Sie dies separat tun. Eine Erläuterung zum Erstellen oder Ändern von Python-Umgebungen liegt außerhalb des gültigen Bereichs für dieses Lernprogramm. Weitere Informationen zum Einrichten von eines Python-Clients, der die richtigen Bibliotheken enthält, finden Sie unter [installieren Sie Python-Client](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) und [Link Python-Tools](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools).

**Remote rechenkontexte und revoscalepy**


In diesem Beispiel wird veranschaulicht, wie eine Python-Modell zu erstellen, in einem _computekontext_, und Sie können Sie von einem Client aus arbeiten, aber wählen Sie eine remote-Umgebung, z. B. SQL Server, Spark oder Machine Learning-Servers, auf dem die Vorgänge werden tatsächlich ausgeführt. Verwenden rechenkontexte erleichtert es einmal Schreiben von Code und eine beliebige unterstützte Umgebung bereitgestellt.

Zum Ausführen von Python-Code in SQL Server erfordert die **Revoscalepy** Paket. Dies ist eine spezielle Python-Paket bereitgestellt von Microsoft, ähnlich wie die **"revoscaler"** -Paket für die Sprache "R". Die **Revoscalepy** Paket unterstützt die Erstellung von rechenkontexte, und bietet die Infrastruktur für die Übergabe von Daten und Modellen zwischen einer lokalen Arbeitsstation und einem Remoteserver. Die **Revoscalepy** -Funktion, die Ausführung von Code in der Datenbank wird unterstützt [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).







## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die *über* neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (11 + 6): &nbsp; &nbsp; **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (18 + 0): &nbsp; &nbsp; **Analysis Services für SQL** Docs](../analysis-services/new-updated-analysis-services.md)
- [Neue und aktualisierte (218 + 14): **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (14 + 0): &nbsp; &nbsp; **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (3 + 2): &nbsp; &nbsp; **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (3 + 3): &nbsp; &nbsp; **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (7 + 10): &nbsp; &nbsp; **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (0 + 2): &nbsp; &nbsp; **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (1 + 3): &nbsp; &nbsp; **SQL Operations Studio** Docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neue und aktualisierte (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (0 + 2): &nbsp; &nbsp; **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)
- [Neue und aktualisierte (1 + 1): &nbsp; &nbsp; **-Tools für SQL** Docs](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Themenbereiche, die *nicht* über neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (0 + 0): **Analyseplattformsystem für SQL** Docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neue und aktualisierte (0 + 0): **Data Quality Services für SQL** Docs](../data-quality-services/new-updated-data-quality-services.md)
- [Neue und aktualisierte (0 + 0): **Data Mining Extensions (DMX) für SQL** Docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [Neue und aktualisierte (0 + 0): **MDX (Multidimensional Expressions) für SQL** Docs](../mdx/new-updated-mdx.md)
- [Neue und aktualisierte (0 + 0): **ODBC (Open Database Connectivity) für SQL** Docs](../odbc/new-updated-odbc.md)
- [Neue und aktualisierte (0 + 0): **PowerShell für SQL** Docs](../powershell/new-updated-powershell.md)
- [Neue und aktualisierte (0 + 0): **Samples for SQL** Docs](../samples/new-updated-samples.md)
- [Neue und aktualisierte (0 + 0): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neue und aktualisierte (0 + 0): **XQuery für SQL** Docs](../xquery/new-updated-xquery.md)

