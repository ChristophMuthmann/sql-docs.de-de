---
title: Aktualisiert – Advanced Analytics für SQL Server-Dokumentation | Microsoft Docs
description: Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation für Advanced Analytics für Microsoft SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 058278df1ee54a6440f8225ea15f727857df76f2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Neue und kürzlich aktualisierte: Advanced Analytics für SQLServer
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **3.12.2017** &nbsp; bis &nbsp; **3.2.2018**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Advanced Analytics für SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Installieren neuer Python-Pakete unter SQL Server](python/install-additional-python-packages-on-sql-server.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Bekannte Probleme in Machine Learning-Diensten](#TitleNum_1)
2. [Konvertieren von R-Code für die Ausführung in Datenbank](#TitleNum_2)
3. [Bestimmen Sie, welche R-Pakete auf SQL Server installiert sind](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1. &nbsp; [Bekannte Probleme in Machine Learning-Diensten](known-issues-for-sql-server-machine-learning-services.md)

*Aktualisiert: 2018-02-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 163.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c6f46adcf795c43f818120b88407a3a89304cb27 c781562605f5cd77f6c43bfe5e89810cb72ceae0  (PR=4789  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=386bfb688843bac7fa4d83dc1cfef94dd19db110) -->



Weitere bekannte Probleme, die R-Lösungen beeinträchtigen können, finden Sie unter der [Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) Standort.

**"Zugriff verweigert" Warnung bei der Ausführung von R-Skripts an SQL Server auf einem Nichtstandard-Speicherort**


Wenn z. B. SQL Server-Instanz an einen nicht standardmäßigen Speicherort installiert wurde außerhalb der `Program Files` Ordner, der die Warnung ACCESS_DENIED ausgelöst wird, wenn Sie versuchen, Skripts auszuführen, die ein Paket zu installieren. Beispiel:

> *In normalizePath(path.expand(path), Winslash, MustWork): der Pfad [2] = "~ExternalLibraries/R/8/1": Zugriff wurde verweigert*

Der Grund hierfür ist, dass eine R-Funktion versucht, den Pfad zu lesen, und schlägt fehl, wenn die integrierte Benutzergruppe **SQLRUserGroup**, hat keinen Lesezugriff. Die Warnung, die ausgelöst wird, blockiert die Ausführung des aktuellen R-Skripts nicht, aber die Warnung möglicherweise mehrmals wiederholt werden, wenn der Benutzer alle R-Skript ausführt.

Wenn Sie SQL Server am Standardspeicherort installiert haben, dieser Fehler tritt nicht auf, da alle Windows-Benutzer auf über Leseberechtigungen verfügen die `Program Files` Ordner.

Dieses Problem wird in einer bevorstehenden Dienstversion behandelt werden. Dieses Problem zu umgehen, geben Sie der Gruppe "" **SQLRUserGroup**, mit Lesezugriff für alle übergeordneten Ordner der `ExternalLibraries`.

**Serialisierungsfehler zwischen den alten und neuen Versionen von "revoscaler"**


Wenn Sie ein Modell mit einem serialisierten Format mit einer Remoteinstanz von SQL Server übergeben, wird möglicherweise die Fehlermeldung angezeigt:

> *Fehler in MemDecompress (Daten, Typ = Dekomprimieren) interner Fehler-3 in memDecompress(2).*

Dieser Fehler wird ausgelöst, wenn Sie das Modell über eine aktuelle Version von die Serialisierungsfunktion gespeichert [RxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), aber SQL Server-Instanz, in dem Sie das Modell deserialisieren, hat eine ältere Version der APIs "revoscaler" von SQL Server 2017 CU2 oder früher.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-converting-r-code-for-execution-in-databaserconverting-r-code-for-use-in-sql-servermd"></a>2. &nbsp; [Konvertieren von R-Code für die Ausführung in Datenbank](r/converting-r-code-for-use-in-sql-server.md)

*Aktualisiert: 2018-01-08* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 136.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a1d156fac1af5813ef75965071686b177e2aede7 fc8beff0aa0d7ea298e493b90984875e81e9143e  (PR=4493  ,  Filename=converting-r-code-for-use-in-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f486d12078a45c87b0fcf52270b904ca7b0c7fc8) -->



**Verpacken von R-Code in einer gespeicherten Prozedur**

+ Wenn Ihr Code relativ einfach ist, können Sie es in einer T-SQL eine benutzerdefinierte Funktion ohne Änderung einbetten, wie in diesen Beispielen beschrieben:

    + [Erstellen Sie eine R-Funktion, die im RxExec ausgeführt wird](r/../tutorials/deepdive-create-a-simple-simulation.md)
    + [Feature Engineering mit T-SQL und R](r/../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Wenn der Code komplexer ist, verwenden Sie das R-Paket **Sqlrutils** Code zu konvertieren. Dieses Paket soll erfahrene Benutzer von R gute gespeicherte Prozedurcode schreiben zu helfen.

    Der erste Schritt ist die R-Code umschreiben müssen, als einzelne Funktion mit klar definierten Eingaben und Ausgaben.

    Verwenden Sie dann die **Sqlrutils** Paket im richtigen Format der Eingaben und Ausgaben zu generieren. Die **Sqlrutils** Paket der vollständigen gespeicherte Prozedur-Code für Sie generiert, und können auch die gespeicherte Prozedur in der Datenbank registrieren.

    Weitere Informationen und Beispiele finden Sie unter [SqlRUtils](r/../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md).

**Integration mit anderen workflows**

+ T-SQL-Tools und ETL-Prozessen genutzt werden. Führen Sie namens Feature Engineering merkmalsextraktion und DatenBereinigung als Teil des Datenworkflows im voraus.

    Bei der Arbeit in einer dedizierten R-Entwicklungsumgebung wie z. B. R-Tools für Visual Studio oder RStudio Sie möglicherweise Abrufen von Daten auf Ihrem Computer, die Daten analysieren, iterativ, und klicken Sie dann auszuschreiben oder zeigen die Ergebnisse.

    Jedoch wenn eigenständigen R-Code zu SQL Server migriert wird, kann Großteil dieser Prozess werden vereinfacht oder automatisiert an andere SQL Server-Tools zu delegieren.

+ Verwenden Sie sichere, asynchrone Visualisierung Strategien.

    Häufig Benutzer von SQL Server können nicht auf Dateien auf dem Server zugreifen, und in der Regel führen Sie R-Grafikgerät SQL Clienttools nicht unterstützt. Wenn Sie grafische Darstellungen oder andere Grafik als Teil der Lösung generieren, sollten Sie die Darstellungen als binäre Daten exportieren und in einer Tabelle speichern, oder schreiben.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3. &nbsp; [Bestimmen Sie, welche R-Pakete auf SQL Server installiert sind](r/determine-which-packages-are-installed-on-sql-server.md)

*Aktualisiert: 2018-01-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_2))

<!-- Source markdown line 78.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9a065066398843a4bed318fa46d4982d712915a9 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f  (PR=4715  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=9e6a029456f4a8daddb396bc45d7874a43a47b45) -->




**Speicherort der Bibliothek und Version abrufen**


Im folgenden Beispiel wird der Speicherort von "revoscaler" im lokalen rechenkontext und die Paketversion.

```
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

**Bestimmen der Bibliothek, die von SQL Server verwendeten Pfad**


Wenn Sie Machine learning-Komponenten mithilfe von Bindung aktualisiert haben, kann der Pfad zum R-Bibliothek ändern. In diesem Fall möglicherweise vorherigen Verknüpfungen zu R-Tools mit eine frühere Version verweisen. Der Pfad und der Paket-Version von SQL Server verwendet, können Sie sicherstellen, dass einen Befehl wie folgt ausführen:

```
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**Ergebnisse**

```
STDOUT message(s) from external script:
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```







## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die *über* neue oder kürzlich aktualisierte Artikel verfügen


- [Neu und aktualisiert (1+3):&nbsp;Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Analytics Platform System für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zur **Datenbank-Engine für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu und aktualisiert (12+1): Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu und aktualisiert (6+2):&nbsp;Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu und aktualisiert (15+0): Dokumente zu **PowerShell für SQL**](../powershell/new-updated-powershell.md)
- [Neu und aktualisiert (2+9):&nbsp;Dokumente zu **relationalen Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu und aktualisiert (1+0):&nbsp;Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zu **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Neu und aktualisiert (1+2):&nbsp;Dokumente zu **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Neu und aktualisiert (0+2):&nbsp;Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Themenbereiche, die *nicht* über neue oder kürzlich aktualisierte Artikel verfügen


- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [Neue und aktualisierte (0 + 0): **ActiveX Data Objects (ADO) für SQL** Docs](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [Neue und aktualisierte (0 + 0): **Data Quality Services für SQL** Docs](../data-quality-services/new-updated-data-quality-services.md)
- [Neue und aktualisierte (0 + 0): **Data Mining Extensions (DMX) für SQL** Docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [Neue und aktualisierte (0 + 0): **MDX (Multidimensional Expressions) für SQL** Docs](../mdx/new-updated-mdx.md)
- [Neue und aktualisierte (0 + 0): **ODBC (Open Database Connectivity) für SQL** Docs](../odbc/new-updated-odbc.md)
- [Neue und aktualisierte (0 + 0): **Samples for SQL** Docs](../samples/new-updated-samples.md)
- [Neue und aktualisierte (0 + 0): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [Neue und aktualisierte (0 + 0): **XQuery für SQL** Docs](../xquery/new-updated-xquery.md)


