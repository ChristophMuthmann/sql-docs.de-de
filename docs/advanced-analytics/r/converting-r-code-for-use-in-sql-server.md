---
title: Konvertieren von R-Code für die Verwendung in R Services| Microsoft-Dokumentation
ms.date: 12/20/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 669f52d499b9479e23266af91c04e6bc084bb8ea
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="converting-r-code-for-execution-in-database"></a>Konvertieren von R-Code für die Ausführung in Datenbank
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel bietet Anleitung auf hoher Ebene zum Ändern von R-Code in SQL Server funktionieren. 

Wenn Sie R-Code von R Studio oder eine andere Umgebung mit SQL Server verschieben, meistens der Code funktioniert ohne weitere Änderung: z. B. wenn der Code einfacher ist, z. B. eine Funktion, die einige akzeptiert Eingaben und gibt einen Wert zurück. Es ist auch einfacher, Port-Lösungen, in denen die **"revoscaler"** oder **MicrosoftML** Pakete, mit denen Ausführung in verschiedenen Ausführungskontexte mit minimalen Änderungen zu unterstützen.

Erfordert jedoch möglicherweise der Code erhebliche Änderungen Wenn eine der folgenden Bedingungen zutrifft:

+ Sie verwenden die R-Bibliotheken, die auf das Netzwerk zugreifen, oder, die nicht auf SQL Server installiert sein.
+ Der Code führt separate Aufrufe auf Datenquellen außerhalb von SQL Server, wie z. B. Excel-Arbeitsblättern, Dateien auf Freigaben und andere Datenbanken. 
+ Den Code in ausgeführt werden soll die *@script* Parameter [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) und die gespeicherte Prozedur auch parametrisieren.
+ Die ursprüngliche Lösung umfasst mehrere Schritte, die eine effizientere in einer produktiven Umgebung unabhängig, z. B. datenvorbereitung oder Feature Engineering im Vergleich zu Modell trainieren oder bewerten reporting ausgeführt werden können.
+ Sie verbessern möchten Optimieren der Leistung von Bibliotheken ändern, verwenden parallele Ausführung oder einige Verarbeitung mit SQL Server-Abladung. 

## <a name="step-1-plan-requirements-and-resources"></a>Schritt 1: Anforderungen des Plans und Ressourcen

**Pakete**

+ Bestimmen, welche Pakete erforderlich sind, und stellen Sie sicher, dass sie auf SQL Server funktionieren.
 
+ Installieren Sie Pakete im voraus, in der Paket-Standardbibliothek, die von Machine Learning-Dienste verwendet. Benutzerbibliotheken werden nicht unterstützt.

**Datenquellen** 

+ Wenn Sie beabsichtigen, Ihre R-Code im einbetten [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identifizieren Sie die primären und sekundären Datenquellen. 

    + **Primäre** -Datenquellen können Sie große Datasets, z. B. modelltrainingsdaten oder Eingabedaten für Vorhersagen. Der Eingabeparameter der größten Dataset zuordnen möchten [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + **Sekundäre** Datenquellen sind in der Regel kleiner Datasets, beispielsweise Listen von Faktoren oder zusätzliche Gruppierungs--Variablen. 
    
    Sp_execute_external_script unterstützt derzeit nur ein einzelnes Dataset als Eingabe für die gespeicherte Prozedur. Allerdings können Sie mehrere skalare oder binäre Eingaben hinzufügen.

    Vor dem Ausführen der Aufrufe von gespeicherten Prozeduren können nicht verwendet werden, als Eingabe für [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Sie können Abfragen, Sichten oder eine andere gültige SELECT-Anweisung verwenden.

+ Bestimmen Sie die Ausgaben, die Sie benötigen. Wenn das Ausführen von R-Code mithilfe von Sp_execute_external_script kann die gespeicherte Prozedur daher nur einen Datenrahmen ausgegeben. Allerdings können Sie auch mehrere Ausgaben auf skalare, einschließlich Darstellungen ausgegeben und Modelle im Binärformat als auch andere Skalare Werte von R-Code oder SQL Parameter.

**Datentypen**

+ Stellen Sie eine Prüfliste der möglichen Probleme bei Datentypen zusammen.

    Alle R-Datentypen werden von SQL Server-Machine Learning-Dienste unterstützt. Allerdings [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt eine größere Vielfalt Datentypen als R. Aus diesem Grund werden einige implizite datentypkonvertierungen ausgeführt, beim Senden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten in R und umgekehrt. Sie müssen explizit umgewandelt oder einige Daten zu konvertieren. 

    NULL-Werte werden unterstützt. R allerdings verwendet die `na` Data-Konstrukts einen fehlenden Wert darstellen, also ein NULL-Wert ähnelt.

+ Entfernen Sie Abhängigkeit von Daten, die vom R: z. B. Rowid verwendet werden können und GUID-Datentypen von SQL Server nicht genutzt werden, indem Sie R und erzeugen Fehler.

    Weitere Informationen finden Sie unter [R-Bibliotheken und Datentypen](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Schritt 2: Konvertieren oder Verpacken von code

Wie viel Code ändern, hängt davon ab, ob Sie möchten, senden Sie die R-Code von einem Remoteclient aus, um in der SQL Server-computekontext auszuführen, oder den Code als Teil einer gespeicherten Prozedur und eine bessere Leistung und datensicherheit zu gewinnen, bereitstellen möchten. Umschließen den Code in einer gespeicherten Prozedur stellt einige zusätzlichen Anforderungen. 

+ Definieren Sie Ihre primären Eingabedaten als eine SQL-Abfrage an, nach Möglichkeit zum Verschieben von Daten zu vermeiden.

+ Bei der Ausführung von R in einer gespeicherten Prozedur können Sie über mehrere übergeben **skalare** Eingaben. Für alle Parameter, die Sie in der Ausgabe verwenden möchten, fügen die **Ausgabe** Schlüsselwort. 

    Z. B. die folgenden skalaren Eingabe `@model_name` enthält den Modellnamen auch in einer eigenen Spalte in den Ergebnissen ausgegeben wird:

    ```SQL
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Alle Variablen, die Sie als Parameter der gespeicherten Prozedur übergeben [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) Variablen in der R-Code zugeordnet werden muss. Standardmäßig werden die Variablen nach Namen zugeordnet.

    Alle Spalten im Eingabedataset müssen auch Variablen in der R-Skript zugeordnet werden.  Nehmen wir beispielsweise an, dass Ihre R-Skript enthält eine Formel wie diese:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Ein Fehler wird ausgelöst, wenn die Eingabedatasets keine Spalten mit den entsprechenden Namen ArrDelay, CRSDepTime DayOfWeek, CRSDepHour und DayOfWeek enthält.

+ In einigen Fällen muss der Ausgabeschema für die Ergebnisse im Voraus definiert werden.

    Angenommen, um die Daten in eine Tabelle einzufügen, müssen Sie verwenden die **mit RESULTSET** -Klausel, um das Schema angeben.

    Ausgabeschema ist auch erforderlich, wenn das R-Skript, das Argument verwendet `@parallel=1`. Grund hierfür ist, dass mehrere Prozesse von SQL Server zum Ausführen der Abfrage möglicherweise parallel erstellt und die Ergebnisse am Ende gesammelten werden. Aus diesem Grund muss Ausgabeschema vorbereitet werden, bevor die parallele Prozesse erstellt werden können.
    
    In anderen Fällen können Sie das ergebnisschema weglassen, mithilfe der Option **mit RESULT SETS UNDEFINED**. Diese Anweisung gibt das Dataset aus dem R-Skript zurück, ohne benennen die Spalten oder die SQL-Datentypen angeben.

+ Erwägen Sie die Generierung der zeitlichen Steuerung oder änderungsnachverfolgung Daten, die mithilfe von T-SQL anstelle von r

    Übergeben Sie z. B. die Systemzeit oder andere Informationen, die zur Überwachung und Speicher verwendet wird, durch Hinzufügen eines T-SQL-Aufrufs, der über die Ergebnisse übergeben wird, anstatt die ähnliche Daten in der R-Skript generieren. 

**Verbessern der Leistung und Sicherheit**

+ Vermeiden Sie vorhersagen oder Zwischenergebnisse in eine Datei schreiben. Schreiben Sie vorhersagen stattdessen in eine Tabelle, um die datenverschiebung zu vermeiden.

+ Führen Sie alle Abfragen im voraus, und überprüfen Sie die SQL Server-Abfragepläne Aufgaben zu identifizieren, die parallel ausgeführt werden können.

    Wenn die Eingabeabfrage parallelisiert werden kann, legen Sie `@parallel=1` als Teil Ihrer Argumente [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    Eine Parallelverarbeitung mit diesem Flag ist in der Regel jedes Mal möglich, wenn SQL Server mit partitionierten Tabellen arbeiten oder eine Abfrage zwischen mehreren Prozessen verteilen kann und die Ergebnisse am Ende aggregiert. Eine Parallelverarbeitung mit diesem Flag ist nicht möglich, wenn Sie Modelle mithilfe von Algorithmen trainieren, die ein Lesen aller Daten voraussetzen, oder wenn Sie Aggregate erstellen müssen.

+ Überprüfen Sie Ihren R-Code, um Schritte zu identifizieren, die unabhängig oder effizienter ausgeführt werden können, und verwenden Sie dazu einen separat gespeicherten Prozeduraufruf. Beispielsweise erhalten Sie möglicherweise eine bessere Leistung, indem Sie auf diese Weise namens Feature Engineering oder Funktion extrahiert, und die Werte in einer Tabelle speichern.

+ Suchen Sie nach Möglichkeiten zum T-SQL und R-Code für satzbasierte Berechnungen verwenden.

    Beispielsweise diese R-Lösung zeigt, wie eine benutzerdefinierte T-SQL-Funktionen und R kann führen dieselbe Funktion engineering: [Data Science-End-to-End-Exemplarische Vorgehensweise](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Wenn möglich, ersetzen Sie herkömmliche R-Funktionen mit **ScaleR** Funktionen, die verteilte Ausführung zu unterstützen. Weitere Informationen finden Sie unter [Vergleich der Base R und R-Funktionen für Skalierung](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Wenden Sie sich an ein Datenbankentwickler, um zu bestimmen, Möglichkeiten zum Verbessern der Leistung mithilfe von SQL Server-Funktionen wie z. B. [Speicheroptimierte Tabellen](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables), oder wenn Sie Enterprise Edition verfügen [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    Weitere Informationen finden Sie unter [SQL Server-Optimierung Tipps und Tricks für Analytics Services](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>Schritt 3: Für die Bereitstellung vorbereiten

+ Benachrichtigen Sie den Administrator, damit Pakete installiert und im Voraus getestet werden, bevor Sie Ihren Code bereitstellen. 

    In einer Entwicklungsumgebung ist es möglicherweise angemessen, Pakete als Teil des Codes zu installieren, aber dies ist kein empfehlenswertes Verfahren in einer produktionsumgebung. 

    Benutzerbibliotheken werden nicht unterstützt, unabhängig davon, ob Sie eine gespeicherte Prozedur oder Ausführen von R-Code in der SQL Server-computekontext.

**Verpacken von R-Code in einer gespeicherten Prozedur**

+ Wenn Ihr Code relativ einfach ist, können Sie es in einer T-SQL eine benutzerdefinierte Funktion ohne Änderung einbetten, wie in diesen Beispielen beschrieben:

    + [Erstellen Sie eine R-Funktion, die im RxExec ausgeführt wird](..\tutorials\deepdive-create-a-simple-simulation.md)
    + [Feature Engineering mit T-SQL und R](..\tutorials\sqldev-create-data-features-using-t-sql.md)

+ Wenn der Code komplexer ist, verwenden Sie das R-Paket **Sqlrutils** Code zu konvertieren. Dieses Paket soll erfahrene Benutzer von R gute gespeicherte Prozedurcode schreiben zu helfen. 

    Der erste Schritt ist die R-Code umschreiben müssen, als einzelne Funktion mit klar definierten Eingaben und Ausgaben.

    Verwenden Sie dann die **Sqlrutils** Paket im richtigen Format der Eingaben und Ausgaben zu generieren. Die **Sqlrutils** Paket der vollständigen gespeicherte Prozedur-Code für Sie generiert, und können auch die gespeicherte Prozedur in der Datenbank registrieren. 

    Weitere Informationen und Beispiele finden Sie unter [SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md).

**Integration mit anderen workflows**

+ T-SQL-Tools und ETL-Prozessen genutzt werden. Führen Sie namens Feature Engineering merkmalsextraktion und DatenBereinigung als Teil des Datenworkflows im voraus.

    Wenn Sie arbeiten in einer dedizierten R-Entwicklungsumgebung wie z. B. [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] oder RStudio, Sie möglicherweise Abrufen von Daten auf Ihrem Computer, die Daten analysieren, iterativ, und klicken Sie dann auszuschreiben oder zeigen die Ergebnisse. 
    
    Jedoch wenn eigenständigen R-Code zu SQL Server migriert wird, kann Großteil dieser Prozess werden vereinfacht oder automatisiert an andere SQL Server-Tools zu delegieren. 

+ Verwenden Sie sichere, asynchrone Visualisierung Strategien.

    Häufig Benutzer von SQL Server können nicht auf Dateien auf dem Server zugreifen, und in der Regel führen Sie R-Grafikgerät SQL Clienttools nicht unterstützt. Wenn Sie grafische Darstellungen oder andere Grafik als Teil der Lösung generieren, sollten Sie die Darstellungen als binäre Daten exportieren und in einer Tabelle speichern, oder schreiben.

+ Umschließen Sie vorhersagen und Funktionen zur entfernungsbewertung in gespeicherten Prozeduren für den direkten Zugriff von Anwendungen.

### <a name="other-resources"></a>Weitere Ressourcen

Zum Anzeigen von Beispielen für wie R-Lösungen in SQL Server bereitgestellt werden kann, finden Sie in diesen Beispielen aus:

+ [Erstellen eines Vorhersagemodells für Ski Vermietung Business mittels R und SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [In der Datenbank Analytics für den SQL-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md) veranschaulicht, wie Sie R-Code modularer können durch Einbinden in gespeicherten Prozeduren

+ [End-to-End Data Science-Lösung](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) enthält einen Vergleich der namens Feature Engineering in R und T-SQL
