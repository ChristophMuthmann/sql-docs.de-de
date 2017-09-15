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
ms.date: 09/11/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: fb6185aae04a1fb53a4db03cbab267e3f52dc779
ms.contentlocale: de-de
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Neue und kürzlich aktualisierte: Advanced Analytics für SQLServer



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-07-18** &nbsp; - zu - &nbsp; **2017-09-11**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Advanced Analytics für SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links führen zu neue Artikel, die vor kurzem hinzugefügt wurden.


1. [Zum Bewerten von Realtime oder systemeigenen bewerten in SQL Server ausführen](r/how-to-do-realtime-scoring.md)
2. [Installieren Sie vortrainierte Machine learning-Modelle mit SQL Server](r/install-pretrained-models-sql-server.md)
3. [Native Bewertung](sql-native-scoring.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

Dieser Abschnitt zeigt die Auszüge von Updates, die vom Artikel, die vor kurzem eine große Aktualisierung aufgetreten sind.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese compact Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Einrichten von Python Machine Learning-Services (Datenbankintern)](#TitleNum_1)
2. [Einführung in revoscalepy](#TitleNum_2)
3. [Unterschiede in Machine Learning-Features zwischen SQL Server-Editionen](#TitleNum_3)
4. [Operationalisieren von R-Code (Machine Learning-Services)](#TitleNum_4)
5. [Leistung für R Services: Ergebnisse und Ressourcen](#TitleNum_5)
6. [Leistung für R Services – Data-Optimierung](#TitleNum_6)
7. [R-paketverwaltung für SQL Server](#TitleNum_7)
8. [Einrichten von SQL Server Machine Learning Services (datenbankintern)](#TitleNum_8)
9. [SQL Server-Konfiguration für die Verwendung mit R](#TitleNum_9)
10. [Optimieren der Leistung für R in SQL Server](#TitleNum_10)
11. [Szenarien für Data Science und Lösungsvorlagen](#TitleNum_11)
12. [Was ist neu in Machine Learning Services in SQL Server](#TitleNum_12)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-set-up-python-machine-learning-services-in-databasepythonsetup-python-machine-learning-servicesmd"></a>1. &nbsp;[Python Machine Learning-Dienste (In-Database) einrichten](python/setup-python-machine-learning-services.md)

*Aktualisiert: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 263.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 fbe2ef55a5caecd64bb21ce854617a10b2d65567 8cd65baf77f27db00a0a4f07f3129a4231edb48b  (PR=3084  ,  Filename=setup-python-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=05976158e43d7dfafaf02289462d1537f5beeb36) -->



     [Modify the user account pool for SQL Server R Services--../r/modify-the-user-account-pool-for-sql-server-r-services.md)

Wenn Sie SQL Server Standard Edition verwenden, verfügen nicht über die Ressourcenkontrolle können Sie dynamische Verwaltungssichten und erweiterte Ereignisse verwenden, helfen Ihnen beim Verwalten von Serverressourcen. Sie können auch Windows-ereignisüberwachung für diesen Zweck. Weitere Informationen finden Sie unter [überwachen und Verwalten von R Services –... /r/Managing-and-Monitoring-r-Solutions.MD).

**Aktualisieren Sie den Computer mit dem Erlernen von Komponenten**


Wenn Sie Machine Learning Services mithilfe von SQL Server-2017 installieren, erhalten Sie die Version der Komponenten, zum Zeitpunkt der Veröffentlichung veröffentlicht wurde. Jedes Mal gepatcht oder aktualisieren Sie die SQL Server-Instanz werden die Machine Learning-Komponenten ebenfalls aktualisiert.

Upgrade Machine learning-Komponenten auf einen schnelleren Zeitplan als unterstützt, wird von SQL Server-Versionen von Microsoft Machine Learning-Server installieren. Wenn Sie dies tun, erhalten Sie auch keine neuen Features, die in der neuesten Version von Machine Learning-Server, z. B. unterstützt:

+ Updates für Python-Pakete für [Revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) und [Microsoftml für Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).
+ [Modelle pretrained](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) für bildanalysen Klassifizierung und Text.

Informationen zum Aktualisieren einer Instanz finden Sie unter [Upgrade R-Komponenten über Bindung--... \r\use-sqlbindr-exe-to-Upgrade-an-instance-of-SQL-Server.MD).

> [!NOTE]
>
> Die aktuelle Releaseversion enthält die neueste Version aller Machine Learning-Komponenten. Obwohl Upgrades über Microsoft Machine Learning-Server für SQL Server-2017 unterstützt werden, gilt die Aktualisierung, die derzeit verfügbar ist daher nur für SQL Server 2016-Instanzen.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>2. &nbsp;[Revoscalepy Einführung](python/what-is-revoscalepy.md)

*Aktualisiert: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 79.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a d2eac3313a74bc5d5afd754fc357b3693e6801e1  (PR=2939  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



| (column_1) | (Spalte_2) | (column_3) |
| :-- | :-- | :-- |
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



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-differences-in-machine-learning-features-between-editions-of-sql-serverrdifferences-in-r-features-between-editions-of-sql-servermd"></a>3. &nbsp;[Unterschiede in Machine Learning-Funktionen zwischen SQL Server-Editionen](r/differences-in-r-features-between-editions-of-sql-server.md)

*Aktualisiert: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_2) | [Weiter](#TitleNum_4))

<!-- Source markdown line 47.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5890e212063f3ef228e69afe54e226320d2467f 4e0357701d960c0b8dbda1ac8d56a82f3335c77f  (PR=2964  ,  Filename=differences-in-r-features-between-editions-of-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



     Only Express Edition with Advanced Services includes the machine learning features. The performance limitations are similar to Standard Edition. Web edition is not intended for tasks such as creating machine learning models; however, you can use the PREDICT function to perform scoring using models trained elsewhere.

-   **Azure SQL-Datenbank**

     Machine Learning-Funktionen wie R und Python-Skripts werden in Azure SQL-Datenbank derzeit nicht unterstützt.

     Weitere Informationen und Hinweise zu, wenn diese Funktion zur Verfügung stehen, werden die SQL Server-Blog finden Sie unter: [Python in SQL Server-2017: Erweiterte in Datenbank-Machine Learning](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


**In allen Editionen unterstützten Sprachen**


Für alle Editionen werden die folgenden Machine Learning-Sprachen unterstützt:

+ SQLServer 2017: R und Python
+ SQLServer 2016: Nur R

Microsoft R Open ist in allen Editionen enthalten.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-operationalize-r-code-machine-learning-servicesroperationalizing-your-r-codemd"></a>4. &nbsp;[Operationalisieren von R-Code (Machine Learning-Services)](r/operationalizing-your-r-code.md)

*Aktualisiert: 2017-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_3) | [Weiter](#TitleNum_5))

<!-- Source markdown line 56.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e11d9a5db93932ec89ca96b5337aa4ea03c1d13 0779f06444b5b73ae2dff8bc190d0e388b4ae8e7  (PR=2660  ,  Filename=operationalizing-your-r-code.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



+ [Echtzeit--... / real-time-scoring.md) bewerten, optimiert für kleine Batches
+ Einzeiliges Bewertung, für das Aufrufen von einer Anwendung
+ [Systemeigene bewerteten--... / Sql-systemeigenen-scoring.md), für die schnelle Batch Vorhersage von SQL Server ohne Aufruf von R

Diese exemplarische Vorgehensweise enthält Beispiele für bewerteten mithilfe einer gespeicherten Prozedur in Batches und einzeiliges Modi:

+ [End-to-end Data sience-Vorgehensweise für R in SQL Server--... / tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Finden Sie unter dieser Projektmappenvorlagen für Beispiele zur Bewertung in einer Anwendung zu integrieren:

+ [Retail forecasting](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Unterbindung](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [Kunden, die clustering](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

**Hoher Leistung und Skalierung**


Obwohl die open Source-R-Sprache Einschränkungen aufweist bekanntermaßen, die "revoscaler"-Paket APIs können großen Datasets ausgeführt werden und davon profitieren mit mehreren Threads, Kernen und Prozessen datenbankinternen Berechnungen.

Wenn Ihre R-Lösung komplexe Aggregationen verwendet oder große Datasets, können Sie SQL-Server möglichst effizient in-Memory Aggregationen und columnstore-Indizes nutzen und lassen Sie die R-Code behandeln die statistischen Berechnungen und Bewertungen.

Weitere Informationen zum Verbessern der Leistung in SQL Server-Machine Learning finden Sie unter:

+ [Leistungsoptimierung für SQL Server R Services –... /.. / advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Tipps zur Optimierung der Leistung und tricks](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**R-Code für andere Plattformen anpassen oder remotecomputekontexten**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-performance-for-r-services-results-and-resourcesrperformance-case-study-r-servicesmd"></a>5. &nbsp;[Leistung für R Services: Ergebnisse und Ressourcen](r/performance-case-study-r-services.md)

*Aktualisiert: 2017-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_4) | [Weiter](#TitleNum_6))

<!-- Source markdown line 282.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 40c8cd255ead88edc60531d45dd0377ecbaf7c9b eeca5eed96e2223508910b246dbff18173eecea3  (PR=2565  ,  Filename=performance-case-study-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



Die "revoscaler" und die MicrosoftML Pakete wurden zum Trainieren eines Vorhersagemodells in einer komplexen R-Lösung, die im Zusammenhang mit großen Datasets verwendet. SQL-Abfragen und R-Code wurden identisch. Alle Tests wurden auf einer einzelnen Azure-VM mit SQL Server-Installation ausgeführt. Der Autor verglichen dann bewerteten Zeiten mit und ohne diese Optimierungen, die von SQL Server bereitgestellt wird:

- In-Memory-Tabellen
- Soft-NUMA
- Resource Governor

Um die Auswirkung von Soft-NUMA auf R-skriptausführung zu bewerten, getestet, die Data Science-Team die Lösung auf virtuellen Azure-Computer mit 20 physischen Kernen. Auf diese physische Kerne wurden vier Soft-NUMA-Knoten automatisch erstellt, dass jeder Knoten fünf Kerne enthalten sind.

CPU-Affinitization wurde im Szenario fortsetzen übereinstimmende zum Bewerten der Auswirkungen auf R-Aufträge erzwungen. Vier **SQL Ressourcenpools** und vier **externen Ressourcenpools** erstellt wurden, und die CPU-Affinität wurde angegeben, um sicherzustellen, dass dieselbe Gruppe von CPUs in den einzelnen Knoten verwendet werden würde.

Jede der Ressourcenpools wurde zur Optimierung der Auslastung der Hardware eine andere Arbeitsauslastungsgruppe zugewiesen. Der Grund hierfür ist, Soft-NUMA und CPU-Affinität physischen Speicher in der physischen NUMA-Knoten kann nicht geteilt werden. aus diesem Grund müssen alle soft NUMA-Knoten, die auf dem gleichen physischen NUMA-Knoten basieren definitionsgemäß Arbeitsspeicher in demselben Betriebssystem-Speicherblock verwenden. Das heißt, ist es keine Speicher-Prozessor-Affinität.

Der folgende Prozess wurde verwendet, um diese Konfiguration zu erstellen:

1. Reduzieren Sie die Arbeitsspeichermenge, die mit SQL Server standardmäßig zugewiesen.

2. Erstellen Sie die vier neuen Pools für die R-Aufträge parallel ausgeführt wird.

3. Erstellen Sie vier Arbeitsauslastungsgruppen, sodass jede Arbeitsauslastungsgruppe einen Ressourcenpool zugeordnet ist.

4. Starten der Ressourcenkontrolle mit dem neuen Arbeitsauslastungsgruppen und Zuweisungen.

5. Erstellen Sie eine benutzerdefinierte Klassifizierungsfunktion-Funktion (UDF) verschiedene Aufgaben auf anderen Arbeitsauslastungsgruppen zuweisen.

6. Aktualisieren Sie die Konfiguration der Ressourcenkontrolle, um die Funktion für die entsprechenden Arbeitsauslastungsgruppen zu verwenden.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-performance-for-r-services---data-optimizationrr-and-data-optimization-r-servicesmd"></a>6. &nbsp;[Leistung für R Services – Data-Optimierung](r/r-and-data-optimization-r-services.md)

*Aktualisiert: 2017-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_5) | [Weiter](#TitleNum_7))

<!-- Source markdown line 107.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2ae2e54e8c5c8a3ec92fd2017088dd6ee879a9a1 9cb06bdce4ad6dfa2e9dc19da49103a6cd9817b3  (PR=2565  ,  Filename=r-and-data-optimization-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



> Wenn eine Tabelle in der Datenquelle nicht mit einer Abfrage angegeben ist, verwendet R Services interner Heuristik, um bestimmt die benötigten Spalten aus der Tabelle abgerufen; Dieser Ansatz ist jedoch genügt nicht parallelen Ausführung.

Um sicherzustellen, dass die Daten parallel analysiert werden können, sollten so zum Abrufen der Daten verwendete Abfrage eingeschlossen werden, dass das Datenbankmodul auf einen parallelen Abfrageplan erstellen kann. Wenn der Code oder der Algorithmus große Mengen an Daten verwendet wird, stellen sicher, dass die Abfrage übergeben, um `RxSqlServerData` ist optimiert für die parallele Ausführung. Eine Abfrage, die nicht zu einem parallelen Ausführungsplan führt, kann zu einem einzelnen Prozess für die Berechnung führen.

Wenn Sie mit großen Datasets arbeiten möchten, verwenden Sie Management Studio oder in einer anderen SQL Query Analyzer vor dem Ausführen von R-Code, um den Ausführungsplan zu analysieren. Klicken Sie dann, nehmen Sie alle empfohlenen Schritte zum Verbessern der Leistung der Abfrage. Ein fehlender Index für eine Tabelle kann z.B. die Zeit zum Ausführen einer Abfrage beeinträchtigen. Weitere Informationen finden Sie unter [überwachen und Optimieren der Leistung –... /.. / relational-databases/performance/monitor-and-tune-for-performance.md).

Eine andere häufiger Fehler, der die Leistung beeinträchtigt ist, dass eine Abfrage, mehr Spalten abruft als erforderlich sind. Z. B. wenn eine Formel darauf, dass nur drei Spalten basiert, aber die Quelltabelle über 30 Spalten verfügt, verschieben Sie Daten unnötigerweise.

 + Vermeiden Sie die Verwendung `SELECT *`!
 + Nehmen Sie überprüfen die Spalten im Dataset, und identifizieren Sie nur die für die Analyse benötigt einige Zeit in Anspruch
 + Entfernen Sie aus Ihrer Abfragen keine Spalten mit Datentypen, die mit R-Code, z. B. GUIDS und ROWGUID nicht kompatibel sind
 + Kontrollkästchen für nicht unterstützte Datums- und Zeitformate
 + Anstelle eine Tabelle zu laden, erstellen Sie eine Sicht, die bestimmte Werte aktiviert bzw. deaktiviert das wandelt Spalten, um Fehler bei der Konvertierung zu vermeiden.

**Optimieren der Machine Learning-Algorithmus**


Dieser Abschnitt enthält verschiedene Tipps und Ressourcen, die für "revoscaler" und anderen Optionen im Microsoft R. spezifisch sind



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-r-package-management-for-sql-serverrr-package-management-for-sql-server-r-servicesmd"></a>7. &nbsp;[R-paketverwaltung für SQL Server](r/r-package-management-for-sql-server-r-services.md)

*Aktualisiert: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_6) | [Weiter](#TitleNum_8))

<!-- Source markdown line 22.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2add5a7e1aef02487ac875e353c51161658050a4 5da92dd8b5402266a837172bda9aaabed3162ce8  (PR=2939  ,  Filename=r-package-management-for-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



Dieses Thema beschreibt die Paket-Verwaltungsfunktionen, die Sie verwenden können, um R-Pakete verwalten, die auf einer Instanz von SQL Server ausgeführt werden.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

**Verwalten von Paketen mithilfe des T-SQL**


Sie können R-Pakete als Administrator auf dem Computer zu installieren, wenn Sie diese Berechtigungen verfügen, und wenn Sie die einzige Person, die mithilfe des Servers für Machine Learning-Aufträge werden weiterhin.

Allerdings ist, wenn Sie Pakete für andere Benutzer freigeben möchten, oder wenn mehrere Personen Machine Learning-Aufträge auf dem Server ausführen müssen, es effizienter, eine Bibliothek des Pakets für shared einrichten. SQL Server unterstützt über die Datenbankrollen.

Der Datenbankadministrator ist verantwortlich für das Einrichten Rollen und Hinzufügen von Benutzern zu Rollen. Über Rollen kann der Datenbankadministrator steuern, wer über die Berechtigung zum Hinzufügen oder Entfernen von R-Pakete aus der SQL Server-Umgebung verfügt, und Paketinstallation überwachen können.

**Datenbankrollen für paketverwaltung**


Die folgenden neuen Datenbankrollen Unterstützung sicheren Installation und Verwaltung der R-Paket in SQL Server:

- `rpkgs-users`: Ermöglicht es Benutzern, die alle freigegebenen Pakete verwenden, die von Mitgliedern der installiert wurden die `rpkgs-shared` Rolle.

- `rpkgs-private`: Bietet Zugriff auf freigegebene Pakete mit den gleichen Berechtigungen wie die `rpkgs-users` Rolle. Mitglieder dieser Rolle können darüber hinaus Pakete mit privatem Geltungsbereich installieren, entfernen und verwenden.

-  `rpkgs-shared`: Bietet die gleichen Berechtigungen wie die `rpkgs-private` Rolle. Benutzer, die Mitglied dieser Rolle sind, können ebenfalls freigegebene Pakete installieren oder entfernen.

- `db_owner`: Hat die gleichen Berechtigungen wie die `rpkgs-shared` Rolle. Kann darüber hinaus Benutzern das Recht zum Installieren oder Entfernen von freigegebenen und/oder privaten Paketen erteilen.

**Erstellen einer Bibliothek für externe Paket mithilfe des T-SQL**


Darüber hinaus unterstützt SQL Server 2017 die T-SQL-Anweisung **externe Bibliothek erstellen**, um die Verwaltung von Datenbankadministrator von externen Bibliotheken unterstützen. Derzeit können Sie diese Anweisung verwenden, Windows-basierten Bibliotheken für zusätzliche r zu erstellen, die Unterstützung in Zukunft für Python-Pakete und für Pakete, die für die Ausführung auf anderen Plattformen wie Linux geschrieben geplant ist.



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>8. &nbsp;[Einrichten von SQL Server Machine Learning-Services (Datenbankintern)](r/set-up-sql-server-r-services-in-database.md)

*Aktualisiert: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_7) | [Weiter](#TitleNum_9))

<!-- Source markdown line 240.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 452dc36b4d0097f9562642238ba49eea0373d25b 4d355f6494b417dd90dce3943e7176eaece7336e  (PR=3070  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



Wenn Sie R-Lösungen auf einer Data Science-Clientcomputer erstellen und Code mithilfe von SQL Server-Computers als computekontext ausführen müssen, können Sie eine SQL-Anmeldung oder die integrierte Windows-Authentifizierung verwenden.

* Wenn Sie eine SQL-Anmeldung verwenden, müssen Sie sicherstellen, dass sie über die erforderlichen Berechtigungen für die Datenbank verfügt, in der Sie Daten lesen werden. Können Sie dies tun, indem hinzufügen *Herstellen einer Verbindung mit* und *wählen* Berechtigungen, oder indem Sie den Anmeldenamen für die *"db_datareader"* Rolle. Bei Anmeldungen, die zum Erstellen von Objekten müssen hinzufügen *DDL_admin* Rechte. Für Anmeldungen, die Daten speichern müssen, um Tabellen, fügen Sie den Anmeldenamen für die *Db_datawriter* Rolle.

* Für Windows-Authentifizierung: müssen Sie möglicherweise eine ODBC-Datenquelle auf dem Data Science-Client zu konfigurieren, der den Namen der Instanz und andere Verbindungsinformationen angibt. Weitere Informationen finden Sie unter [ODBC-Datenquellenadministrator](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

**Nächste Schritte**


Nachdem Sie sichergestellt haben, dass das Feature für die Ausführung von Skripts in SQL Server funktioniert, können Sie R und Python-Befehle ausführen, von SQL Server Management Studio, Visual Studio-Code oder einem anderen Client, der T-SQL-Anweisungen an den Server gesendet werden kann.

Sie möchten jedoch nehmen einige Änderungen an der Systemkonfiguration, zur Unterstützung einer starke Nutzung von Machine Learning, oder fügen neue R-Pakete.

Dieser Abschnitt enthält einige allgemeine Änderungen, die Sie vornehmen können, um Machine Learning unterstützt.

**Weitere Konten hinzufügen**


Wenn Sie glauben, dass R intensivsten verwendet werden kann oder wenn Sie davon ausgehen, dass viele Benutzer gleichzeitig ausgeführte Skripts werden, können Sie die Anzahl der Worker Konten erhöhen, die mit dem Launchpad-Dienst zugewiesen sind. Weitere Informationen finden Sie unter [Ändern des benutzerkontenpools für SQL Server R Services--modify-the-user-account-pool-for-sql-server-r-services.md).

**<a name="bkmk_optimize"></a>Optimieren des Servers für den externen skriptausführung**




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-sql-server-configuration-for-use-with-rrsql-server-configuration-r-servicesmd"></a>9. &nbsp;[SQL Server-Konfiguration für die Verwendung mit R](r/sql-server-configuration-r-services.md)

*Aktualisiert: 2017-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_8) | [Weiter](#TitleNum_10))

<!-- Source markdown line 149.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3f57bae70e3c118c1e2bcd57017322940bae83f8 f296242d470db47077cba4215ef420bd0c60bf33  (PR=2660  ,  Filename=sql-server-configuration-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



Wenn die Abfrage einen einzigen Speicherknoten (Knoten 0) zurückgibt, Sie verfügen nicht über die NUMA-Hardware oder die Hardware ist als interleaved (nicht-NUMA) konfiguriert. SQL Server ignoriert auch Hardware-NUMA bei der es maximal vier CPUs oder mindestens einen Knoten nur eine CPU aufweist.

Wenn Ihr Computer verfügt über mehrere Prozessoren, aber keinen Hardware-NUMA, können Sie auch [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) auf CPUs in kleinere Gruppen unterteilen.  Die Soft-NUMA-Funktion ist in SQL Server 2016 und SQL Server-2017 automatisch aktiviert, beim Starten des SQL Server-Diensts.

Wenn Soft-NUMA aktiviert ist, werden die Knoten für Sie automatisch von SQL Server verwaltet; um bestimmte arbeitsauslastungen zu optimieren, Sie können jedoch deaktivieren _weicher Affinität_ und CPU-Affinität für die soft-NUMA-Knoten manuell konfigurieren. Dies können Sie bieten mehr Kontrolle über die arbeitsauslastungen zugewiesen sind, auf die Knoten beschränkt, insbesondere, wenn Sie eine Edition von SQL Server verwenden, die Unterstützung der Ressourcenkontrolle. Durch Angabe der CPU-Affinität und zum Ausrichten von Ressourcenpools für Gruppen von CPUs, können Sie die Wartezeit reduzieren und stellen Sie sicher, dass verwandte Prozesse im selben NUMA-Knoten ausgeführt werden.

Das generelle Verfahren zum Konfigurieren von Soft-NUMA und CPU-Affinität für die Unterstützung von R-Arbeitslasten ist wie folgt aus:

1. Aktivieren von Soft-NUMA, falls verfügbar
2. Prozessor-Affinität definieren
3. Erstellen von Ressourcenpools für externe Prozesse, die mit [Resource Governor--... /r/Resource-Governance-for-r-Services.MD)
4. Weisen Sie die [Arbeitsauslastungsgruppen..-- /.. / relational-databases/resource-governor/resource-governor-workload-group.md) an bestimmten affinitätsgruppen

Details, einschließlich Beispielcode finden Sie in diesem Lernprogramm: [SQL Optimierung Tipps und Tricks (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Weitere Ressourcen:**



&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-performance-tuning-for-r-in-sql-serverrsql-server-r-services-performance-tuningmd"></a>10. &nbsp;[Leistungsoptimierung für R in SQL Server](r/sql-server-r-services-performance-tuning.md)

*Aktualisiert: 2017-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_9) | [Weiter](#TitleNum_11))

<!-- Source markdown line 76.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9c30753efdec81e499d5654b5b7a07f0cfe5b003 136a9f483bc8c9e1f69cf9d340d1472c21a52ec4  (PR=2565  ,  Filename=sql-server-r-services-performance-tuning.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



- Konfigurieren Sie die SQL Server-Instanz Saldo Modul Datenbankvorgänge und R oder Python-skriptausführung mit passender. Dazu gehören das Ändern von SQL Server-Standardwerte für den Arbeitsspeicher und CPU-Nutzung, NUMA und prozessoraffinitätsoptionen und Erstellung von Ressourcengruppen.

- Optimieren Sie die Server-Computers für die effiziente Verwendung externer Skripts unterstützen. Dazu kann gehören, erhöhen die Anzahl der Konten, die zum Ausführen des externen Skripts, Aktivierung der paketverwaltung, und Zuweisen von Benutzern zu zugehörigen Sicherheitsrollen.

- Anwenden von Optimierungen, die bestimmte auf Speicherung und Übertragung in SQL Server, einschließlich der Indizierung und Statistiken Strategien, Abfrageentwurf und abfrageoptimierung und des Entwurfs von Tabellen, die für Machine Learning verwendet werden. Sie möglicherweise auch analysieren, Datenquellen und Daten transportieren von Methoden, oder ändern Sie die ETL-Prozesse für die merkmalsextraktion zu optimieren.

- Optimieren der Analysemodell Ineffizienz zu vermeiden. Der Bereich der Optimierungen, die möglich sind richten sich nach der Komplexität von R-Code-Pakete und die Daten, die Sie verwenden. Wichtige Aufgaben umfassen teure Datentransformationen eliminieren oder Auslagern der Daten zur Vorbereitung oder Feature engineering Aufgaben von R oder Python ETL-Prozesse oder SQL. Sie können auch Umgestalten von Skripts, beseitigen Inline-Paket installiert, unterteilen Sie R-Code in separate Verfahren für das Training, Bewertung und Auswertung verwendet, oder vereinfachen Code effizienter als eine gespeicherte Prozedur funktioniert.

**Artikel in dieser Serie**


+ [Leistungsoptimierung für R in SQL Server - Hardware –... \r\sql-Server-Configuration-r-Services.MD)

    Bietet einen Leitfaden zum Konfigurieren der Hardware,..! --SsNoVersion_md--NSCHLIEßEN-NotShown... \..\includes\ssnoversion-md.md)] auf, und klicken Sie zum Konfigurieren von SQL Server-Instanz, um externe Skripts besser zu unterstützen installiert ist. Dies ist besonders nützlich für **Datenbankadministratoren**.

+ [Leistungsoptimierung für R in SQL Server - Code und die Optimierung--... \r\r-and-Data-Optimization-r-Services.MD)



&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-data-science-scenarios-and-solution-templatestutorialsdata-science-scenarios-and-solution-templatesmd"></a>11. &nbsp;[Data Science-Szenarien und -Projektmappenvorlagen](tutorials/data-science-scenarios-and-solution-templates.md)

*Aktualisiert: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_10) | [Weiter](#TitleNum_12))

<!-- Source markdown line 45.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 22c621731015f2192cb0b8d61b22062a4be50e70 6cf9e3f0a3803ed2bce9c4ffadfd7314f15f6b51  (PR=2964  ,  Filename=data-science-scenarios-and-solution-templates.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



[Vorhersagen, wie und wann Leads kontaktieren](https://microsoft.github.io/r-server-campaign-optimization/)

**Was:** diese Lösung verwendet Versicherungsbranche Daten basierend auf demografischen Daten, die Verlaufsdaten Antwortdaten und produktspezifische Details Leads vorherzusagen.  Empfehlungen werden auch generiert, um anzugeben, die beste Kanal und Zeit für Ansatz Benutzer zum Kaufverhalten beeinflussen.

**Vorgehensweise:** die Projektmappe erstellt, und mehrere Modelle verglichen. Die Lösung zeigt auch automatisierte Datenintegration und die Vorbereitung der Daten mithilfe von gespeicherten Prozeduren. Parallele Beispiele werden für SQL Server in-Datenbank, in Azure HDInsight Spark bereitgestellt.

**Gesundheitswesen: Dauer der Krankenhaus Vorhersagen**


[Dauer der Krankenhäusern Vorhersagen](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**Was:** genau Vorhersagen, welche Patienten langfristigen Krankenhausaufenthalt möglicherweise ist ein wichtiger Teil von Sorgfalt und Planung. Administratoren müssen in der Lage, um zu bestimmen, welche Funktionen mehr Ressourcen benötigen, und Betreuer sicherstellen möchten, dass diese den Bedürfnissen von Patienten können.

**Vorgehensweise:** dieser Lösung verwendet die Data Science Virtual Machine und eine Instanz von SQL Server mit Machine Learning aktiviert. Darüber hinaus eine Reihe von Power BI-Berichten, die Sie für die Interaktion mit einem bereitgestellten Modell verwenden können.

**Änderungsumfang von Kunden**


[Kunden Änderungsumfang Vorhersage Vorlage (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**Was:** analysieren und Vorhersagen von Kunden codeänderung ist wichtig, in allen Branchen, bei der Verlust von Kunden an die Konkurrenz verwaltet und verhindert werden muss: Bankgeschäfte, Telekommunikation und Einzelhandel, um nur einige zu nennen. Das Ziel der Abwanderungsanalyse ist es, zu identifizieren, welche Kunden möglicherweise abwandern und anschließend angemessene Maßnahmen einzuleiten, um diese Kunden zu behalten und weiterhin Geschäfte mit ihnen zu machen.



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-whats-new-in-machine-learning-services-in-sql-serverwhat-s-new-in-sql-server-machine-learning-servicesmd"></a>12. &nbsp;[Neuigkeiten in Machine Learning Services in SQL Server](what-s-new-in-sql-server-machine-learning-services.md)

*Aktualisiert: 2017-08-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_11))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 025e68a93895a3788a63847cd91bff068775acf3 6dc0be2920c670235038a126d135e08d6f16ec3a  (PR=2712  ,  Filename=what-s-new-in-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=ea75391663eb4d509c10fb785fcf321558ff0b6e) -->



> Machine Learning-Dienste, einschließlich der Verwendung von R oder Python, werden derzeit nicht unterstützt, wenn SQL Server unter Linux oder in Azure SQL-Datenbank ausgeführt. Suchen Sie nach Änderungen in einer späteren Version.
>
> Allerdings wird native Bewertung mithilfe der PREDICT-Funktion derzeit in der Linux-Edition unterstützt.

**Python-Integration in der Datenbank**


Sie können Python in gespeicherten Prozeduren ausführen oder Python Remote mithilfe von SQL Server-Computers als computekontext auszuführen. Diese Integration eröffnet neue Möglichkeiten für die großen Community von Python Entwicklern und Data Scientists ausnutzen der Leistungsfähigkeit von SQL Server und Innovationen von Microsoft untersuchen, wie z. B. **Revoscalepy** und **Microsoftml**.

SQL Server-Entwickler können Sie zugreifen, die eine umfangreiche Python-Bibliotheken in open-Source-Ökosystem, einschließlich gängigen Frameworks wie Scikit-Tensorflow, Caffe und Theano/Keras finden.

Aber Python in der Datenbank für den Machine learning wird nicht ausgeführt. Es gibt unzählige andere Anwendungen für die Integration von Python mit SQL "oder" nutzt die Vorteile von den jeweiligen Sprachen aus, um intelligentere, leistungsstarke Lösungen zu übermitteln.

+ **revoscalepy**

    Diese Version enthält die endgültige Version von **Revoscalepy**, die streaming-Algorithmen in "revoscaler" Pythonic äquivalente skalierbar, ausgeben. Sie können die Python-Modelle für linear und logistische Regressionen, Entscheidungsstrukturen, verstärkten Bäumen und zufällige Gesamtstrukturen, alle parallelisiert und kann in remote rechenkontexte ausgeführt erstellen.

    Weitere Informationen finden Sie unter [What's Revoscalepy--Python/Was-ist-revoscalepy.md).

+ Remote rechenkontexte für Python

    Diese Version unterstützt die Verwendung von mehreren Datenquellen und remote rechenkontexte. Der datenanalyst oder Entwickler kann Python-Code auf einem remote-SQL-Server zum Durchsuchen von Daten oder Modelle erstellen, ohne Verschieben von Daten ausführen. Verwendung von remote rechenkontexte erfordert **Revoscalepy**.







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Dieser Abschnitt enthält sehr ähnlich Artikel für die zuletzt aktualisierten Artikel in anderen Bereichen in unserer öffentlichen Repositorys für "github.com" Betreff: [MicrosoftDocs/Sql-Docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neue und aktualisierte (3 + 12): **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (5 + 0): **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (5 + 1): **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (19 + 82): **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (1 + 8): **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (12 + 1): **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (0 + 1): **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (7 + 1): **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (1 + 1): **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (0 + 2): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neue und aktualisierte (1 + 4): **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (4 + 1): **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)
- [Neue und aktualisierte (0 + 1): **-Tools für SQL** Docs](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [Neue und aktualisierte (0 + 0): **Analysis Services für SQL** Docs](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [Neue und aktualisierte (0 + 0): **Master Data Services (MDS) für SQL** Docs](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)



