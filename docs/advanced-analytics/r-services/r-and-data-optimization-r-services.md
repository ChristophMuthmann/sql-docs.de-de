---
title: "R und Datenoptimierung (R-Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# R und Datenoptimierung (R-Services)
Dieses Thema beschreibt die Methoden zum Aktualisieren Ihres R-Codes zum Verbessern der Leistung und bekannte Probleme zu vermeiden.

## Berechnen von Kontext

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] können Sie entweder die __lokale__ oder __SQL__ Kontext beim Durchführen der Analyse zu berechnen. Bei Verwendung der __lokalen__ Compute-Kontext, Analyse auf dem Clientcomputer ausgeführt wird und Daten abgerufen werden müssen, von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] über das Netzwerk. Die Leistungseinbußen entstanden sind, für die Größe der übertragenen Daten Geschwindigkeit des Netzwerks dieser netzwerkübertragung abhängig und anderen Netzwerk übertragen, die zur gleichen Zeit auftreten.

Wenn der Compute-Kontext ist __SQL Server__, und klicken Sie dann in die analytischen Funktionen ausgeführt werden [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Die Daten sind lokal auf den Analysis-Task keine Netzwerk-Overhead eingeführt wird. 

Bei der Arbeit mit großen Datenmengen sollten Sie immer den SQL Server-Kontext verwenden.

## Faktoren

Die R-Sprache konvertiert Zeichenfolgen aus Tabellen in Faktoren. Nutzen Sie viele Datenquellenobjekte `colInfo` als Parameter zu steuern, wie Spalten behandelt werden. Z. B. `c(“fruit” = c(type = “factor”, levels=as.character(c(1:3)), newLevels=c(“apple”, “orange”, “banana”)))` Nutzen von ganzen Zahlen 1, 2 und 3 aus einer Tabelle und behandeln Sie sie als Faktoren mit Ebenen wird `apple`, `orange`, und `banana`. 

Datenanalysten verwenden häufig faktorvariablen in die Formel. jedoch entstehen mithilfe von Faktoren, wenn die Datenquelle eine ganze Zahl ist Leistung beeinträchtigt, wie zur Laufzeit ganze Zahlen in Zeichenfolgen konvertiert werden. Wenn die Spalte Zeichenfolgen enthält, Sie können jedoch angeben die Ebenen im Voraus `colInfo`. In diesem Fall wäre die entsprechende Anweisung  `c(“fruit” = c(type = “factor”, levels= c(“apple”, “orange”, “banana”)))`, die die Zeichenfolgen als Faktoren behandelt, wie sie gelesen werden. 

Um zur Laufzeit Umwandlungen zu vermeiden, sollten Sie Sie Ebenen als ganze Zahlen in der Tabelle zu speichern, und nutzen diese wie im ersten Beispiel Formel beschrieben. Ist keine semantische Unterschiede Modell generieren, kann dieser Ansatz eine bessere Leistung führen.

## Datentransformation

Datenanalysten verwenden häufig Transformation-Funktionen, die als Teil der Analyse in R geschrieben. Die Funktionen der Transformation müssen auf jede Zeile aus der Tabelle abgerufen angewendet werden. In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], diese Transformation im Batch-Modus erfolgt, und umfasst die Kommunikation zwischen den R-Interpreter und das Modul. Zum Ausführen der Transformations verschiebt die Daten aus SQL, für das Modul, und klicken Sie dann an den Prozess der R-Interpreter und. Daher bei der mithilfe von Transformationen kann eine erhebliche negative Auswirkung auf die Leistung des Algorithmus, abhängig von die Menge der Daten.

Es ist effizienter, alle erforderliche Spalten in der Tabelle oder Sicht, die vor dem Durchführen der Analyse, wie diese Transformationen während der Berechnung vermeidet. Ist dies nicht möglich, vorhandene Tabellen zusätzliche Spalten hinzufügen, können Sie eine andere Tabelle oder Sicht mit den transformierten Spalten erstellen und verwenden Sie eine entsprechende Abfrage zum Abrufen der Daten.

## Batchverarbeitung

Die SQL-Datenquelle (`RxSqlServerData`) verfügt über eine Option an, dass die Batchgröße, die mit dem Parameter `rowsPerRead`. Dieser Parameter gibt die Anzahl der Zeilen, die gleichzeitig verarbeitet. Zur Laufzeit liest die Nummerierung der Zeilen in jedem Batch angegebenen Algorithmen. Standardmäßig ist der Wert dieses Parameters auf 50.000 festgelegt, um sicherzustellen, dass die Algorithmen auch auch auf Computern mit wenig Arbeitsspeicher ausführen können. Wenn der Computer über genügend Arbeitsspeicher verfügt, kann eine bessere Leistung, insbesondere bei großen Tabellen durch Erhöhen dieses Wertes 500.000 oder selbst eine Million erzielt werden. 

Diesen Wert erhöhen, erzeugen möglicherweise nicht immer bessere Ergebnisse und erfordern ein experimentieren, um den optimalen Wert zu ermitteln. Werden die Vorteile dieser sich auf einem großen Dataset mit mehreren Prozessen (`numTasks` festlegen auf einen Wert größer als `1`).

## Parallelverarbeitung

Zur Verbesserung der Leistung der ausgeführten Rx Analysefunktionen in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] basiert auf parallele Verarbeitung mithilfe der verfügbaren Kerne auf dem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer. Es gibt zwei Möglichkeiten zum Erreichen der Parallelisierung mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]:

* Bei Verwendung der `sp_execute_external_script` gespeicherte Prozedur ein R-Skript ausführen der `@parallel` Parameter `1`. Dies ist nützlich für R-Skripts, die nicht RevoScaleR verwenden möchten, der in der Regel mit "Rx" vorangestellt werden. Wenn das Skript RevoScaleR Funktionen verwendet, paralleler Verarbeitung automatisch erfolgt und sollte nicht festgelegt `@parallel` auf `1`.

    Wenn R-Skript parallelisiert werden kann und die [!INCLUDE[tsql_md](../../includes/tsql-md.md)] Abfrage parallelisiert werden, dann [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] erstellt mehrere parallele Prozesse (bis zu der __Max. Grad an Parallelität MAXDOP__ für [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)],), und führen Sie das gleiche Skript für alle Prozesse. Jeder Prozess erhält nur einen Teil der Daten, damit dies nicht mit Skripts nützlich ist, die alle Daten, wie z. B. finden Sie unter muss beim Trainieren eines Modells. Es ist jedoch nützlich, wenn Tasks wie das Batch-Vorhersage parallel ausführen. Weitere Informationen zur Verwendung von Parallelität mit [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), finden Sie unter der __Tipps für Fortgeschrittene: parallele Verarbeitung__ Abschnitt [mithilfe von R-Code in Transact-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md).

* Legen Sie bei Verwendung von Rx-Funktionen mit einem SQL Server-Compute-Kontext `numTasks` auf die Anzahl der Prozesse, die Sie erstellen möchten. Die tatsächliche Anzahl der erstellten Prozesse richtet sich nach [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], und ist möglicherweise kleiner als angefordert. Die Anzahl der Prozesse erstellt kann nie mehr als __MAXDOP__.

    Wenn das R-Skript parallelisiert werden kann und die [!INCLUDE[tsql_md](../../includes/tsql-md.md)] Abfrage parallelisiert werden, dann [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] erstellt mehrere parallele Prozesse aus, wenn die Rx-Funktionen ausgeführt.

Die Anzahl der Prozesse, die erstellt werden, hängt davon ab, eine Vielzahl von Faktoren wie z. B. die Ressourcenkontrolle, aktuelle Verwendung von Ressourcen, die anderen Sitzungen und der Abfrageausführungsplan für die Abfrage, die mit R-Skript verwendet. 

### Parallelisierung der Abfragen

Um sicherzustellen, dass die Daten parallel analysiert werden können, sollte die Abfrage zum Abrufen der Daten so eingeschlossen werden, um sich selbst für die parallele Ausführung zu rendern. 

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ermöglicht die Arbeit mit SQL-Datenquellen mithilfe von `RxSqlServerData` können Sie die Datenquelle angeben. Die Quelle kann es sich um eine Tabelle oder eine Abfrage sein. In den folgenden Beispielen wird z. B. ein R-Datenquellenobjekt basierend auf einer SQL-Abfrage definieren:
~~~~
RxSqlServerData(table=”airline”, connectionString = sqlConnString)
~~~~

~~~~
RxSqlServerData(sqlquery=”select [ArrDelay],[CRSDepTime],[DayOfWeek] from airlineWithIndex where rowNum <= 100000”, connectionString = sqlConnString)
~~~~ 

Wie die Algorithmen für die Analyse große Datenmengen aus den Tabellen ziehen, ist es wichtig, um sicherzustellen, dass die Abfrage erhalten `RxSqlServerData` für die parallele Ausführung optimiert ist. Eine Abfrage, die nicht in einem parallelen Ausführungsplan führen kann dazu führen, dass ein einzelner Prozess für die Berechnung.

[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] kann verwendet werden, um den Ausführungsplan zu analysieren und verbessern die Leistung der Abfrage. Ein fehlender Index für eine Tabelle kann z. B. die Zeit zum Ausführen einer Abfrage beeinträchtigen. Finden Sie unter [Überwachen und Optimieren der Leistung](../../relational-databases/performance/monitor-and-tune-for-performance.md) Weitere Informationen.

Eine andere Aufsicht, die die Leistung beeinträchtigen können ist beim Abrufen der Abfrage mehr Spalten als erforderlich sind. Z. B. wenn eine Formel auf nur 3 Spalten basiert und die Tabelle Spalten 30 enthält, verwenden Sie keine Abfrage wie z. B. `select *` oder eines, das mehr Spalten als erforderlich markiert.

> [!NOTE]
> Wenn eine Tabelle in der Datenquelle nicht mit einer Abfrage angegeben wird [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] intern bestimmt die benötigten Spalten aus der Tabelle abrufen, ist jedoch dieser Ansatz genügt nicht parallele Ausführung.

## Algorithmusparameter

Viele Rx Training Algorithmen unterstützt Parameter, um zu steuern, wie das Modell trainieren generiert wird. Während die Genauigkeit und Richtigkeit des Modells wichtig ist, kann die Leistung des Algorithmus gleichermaßen wichtig sein. Sie können Parametersthe Modellparameter Schulung zum Beschleunigen der Berechnung ändern, und in vielen Fällen Sie möglicherweise die Leistung zu verbessern, ohne das Reduzieren der Genauigkeit und Richtigkeit. 

Z. B. `rxDTree` unterstützt die `maxDepth` -Parameter, der die maximale Strukturtiefe steuert. Als `maxDepth` wird erhöht, Leistung kann beeinträchtigt werden, daher es wichtig ist, um die Vorteile der Erhöhen der Tiefe im Vergleich zu Auswirkungen auf die Leistung zu analysieren. 

Einer der Parameter, die mit `rxLinMod` und `rxLogit` ist die `cube` Argument. Dieses Argument kann verwendet werden, wenn der erste abhängige Variable der Formel Faktor ist. Wenn `cube` Wert `TRUE`, erfolgt die Regression mithilfe einer partitionierte Inverse, kann es schneller und verwenden weniger Speicher als standard Regression Berechnung. Wenn die Formel eine große Anzahl von Variablen verfügt, kann die Leistungssteigerung erheblich sein.

Die [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) Benutzerhandbuch hat einige nützliche Informationen für steuern das Modell bei verschiedenen Algorithmen passen. Z. B. mit `rxDTree` können Sie steuern, die Balance zwischen Zeitgründen Komplexität und Prediction durch Anpassen der Parameter wie z. B. `maxNumBins`, `maxDepth`, `maxComplete`, und `maxSurrogate`. Das Erhöhen der Tiefe auf 10 oder 15 kann die Berechnung sehr teuer machen.

Weitere Informationen zum Optimieren der Leistung für `rxDForest` und `rxDTree`, finden Sie unter [Leistung Optimierungsoptionen für RxDForest/RxDTree](https://support.microsoft.com/kb/3104235).

## Modell und Vorhersage

Nachdem das Training abgeschlossen ist und das beste Modell ausgewählt, es wird empfohlen, damit diese leicht verfügbar für Vorhersagen sind das Modell in der Datenbank gespeichert. Für Onlinetransaktionen-Verarbeitung, die Vorhersage erfordert, ist es sehr effizient, laden das vorberechnete Modell aus der Datenbank für die Vorhersage. Die Beispielskripts verwenden Sie diesen Ansatz zum Serialisieren und speichern Sie das Modell in einer Datenbanktabelle. Für die Vorhersage ist das Modell aus der Datenbank deserialisiert.

Einige Modelle, die von Algorithmen, wie z. B. lm oder Glm können sehr groß sein, insbesondere, wenn auf einem großen Dataset verwendet. Größe gelten für die Einschränkungen die Daten, die in gespeichert werden können [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Sie sollten das Modell bereinigen, vor der Speicherung in der Datenbank.

> [!NOTE] Wenn schnell Vorhersage mit einer gespeicherten Modell und integrieren die Analyse in einer Anwendung ein wichtiges Szenario handelt, empfehlen wir __DeployR__. Es kann verwendet werden, auf einfache Weise R Analytics in Web, Desktop, Mobile und Dashboard-Anwendung einbinden. Insbesondere ist es hervorragend für das Speichern eines Modells und die Durchführung der einzeiligen Vorhersage mit dem gespeicherten Modell. Weitere Informationen finden Sie unter [zu DeployR](https://msdn.microsoft.com/microsoft-r/rserver/deployr-about).

## Siehe auch
[Ressourcenkontrolle](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
[der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)

[EXTERNE RESSOURCEN-POOL ERSTELLEN](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server-R Services Performance Tuning Guide](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [SQL Server-Konfiguration für R-Dienste](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [Fallstudie zur Leistung](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 