---
title: "Konvertieren von R-Code f&#252;r die Verwendung in R-Dienste | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Konvertieren von R-Code f&#252;r die Verwendung in R-Dienste
Wenn Sie R-Code von R Studio oder einer anderen Umgebung mit SQL Server verschieben, häufig funktioniert der Code ohne weitere Änderung hinzugefügt der *@script* Parameter der [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Dies ist vor allem, wenn Sie Ihre Lösung mit den Funktionen ScaleR entwickelt haben, das relativ einfache Ausführungskontexte ändern.    
    
Allerdings in der Regel wird den R-Code in beide nutzen, die eine engere Integration mit SQL Server ausgeführt ändern möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und teure Übertragung von Daten zu vermeiden.   
   
   
## Ressourcen  
  
Beispiele wie R-Code in SQL Server ausgeführt werden kann, finden Sie in diesen exemplarischen Vorgehensweisen:   
+ [In der Datenbank-Analysen für den SQL-Entwickler](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)    
  Veranschaulicht, wie den R-Code modularer durch Einbinden in gespeicherten Prozeduren  
+ [End-to-End-Data-Science-Lösung](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)    
  Enthält einen Vergleich zwischen Featureentwicklung in R und T-SQL

## Änderungen an den Data Science Process in SQLServer  
  
Bei Verwendung [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)], RStudio, oder anderen Umgebung Workflow normalerweise zum Abrufen von Daten auf Ihrem Computer, die Daten analysieren, iterativ, schreiben und zeigen die Ergebnisse. Allerdings eigenständige R-Code zum SQL Server migriert wird, kann Großteil dieses Prozesses vereinfacht oder delegiert, um andere SQL Server-Tools:

| Externer code | R in SQLServer |
|-------|-------|
| Erfassen von Daten| Definieren von Eingabedaten als SQL-Abfrage in der Datenbank | 
| Zusammenfassen und Visualisieren von Daten| Keine Änderung; Plots können als Bilder exportiert oder einer remote-Arbeitsstation gesendet werden|
|Verarbeiten von Funktionen| Können Sie in der Datenbank R, aber es kann effizienter sein, T-SQL-Funktionen oder benutzerdefinierten UDFs aufrufen|
|Daten, die Teil der Analyseprozess-Bereinigung| DatenBereinigung kann an ETL-Prozesse delegiert und im Voraus ausgeführt werden|
|Vorhersagen der Ausgabe in eine Datei| Vorhersagen, Tabelle oder einbinden ausgeben `predict` in gespeicherten Prozeduren für den direkten Zugriff von Clientanwendungen|
  

  
## Bewährte Methoden  
  
+ Notieren Sie Sie Abhängigkeiten, wie z. B. die erforderlichen Pakete im voraus. In einer Entwicklungs- und testumgebung ist es möglicherweise zum Installieren der Pakete als Teil des Codes in Ordnung, aber dies ist kein empfehlenswertes Verfahren in einer produktiven Umgebung. Benachrichtigen Sie den Administrator, damit Pakete installiert und im Voraus über das Bereitstellen von Code getestet werden können.  
+ Stellen Sie eine Prüfliste der möglichen Probleme geben. Dokumentieren Sie die Schemas der Ergebnisse in jedem Abschnitt des Codes erwartet.  
+ Primäre Datenquellen wie z. B. modelltrainingsdaten oder Eingabedaten für Vorhersagen im Vergleich zu sekundären Quellen wie z. B. Faktoren, die weitere Gruppierung Variablen usw. zu identifizieren. Der Eingabeparameter der größte Dataset zuordnen [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
+ Ändern Sie die Eingabedaten-Anweisungen direkt in der Datenbank arbeiten. Sondern Verschieben von Daten in einer lokalen CSV-Datei oder durch ODBC-Aufrufe wiederholt, erhalten Sie eine bessere Leistung mit SQL-Abfragen oder Sichten, die direkt gegen die Datenbank ausgeführt werden können Verschieben von Daten zu vermeiden.  
+ Mit SQL Server Abfragepläne, um Aufgaben zu identifizieren, die parallel ausgeführt werden können. Wenn die Eingabeabfrage parallelisiert werden kann, legen Sie `@parallel=1` als Teil Ihrer Argumente für Sp_execute_external_script. Parallele Verarbeitung mit diesem Flag kann in der Regel jedes Mal, dass SQL Server können mit partitionierten Tabellen arbeiten oder eine Abfrage von mehreren Prozessen zu verteilen und die Ergebnisse am Ende aggregiert. 
   Parallele Verarbeitung dieses Flag ist in der Regel nicht möglich, wenn Sie sind Schulungen-Modellen mit Algorithmen, die alle Daten gelesen werden müssen oder Aggregate erstellt werden müssen. 
+ Ersetzen Sie nach Möglichkeit konventionelle R-Funktionen mit **ScaleR** Funktionen, die verteilte Ausführung unterstützen. Weitere Informationen finden Sie unter [Vergleichsfunktionen in R skalieren und CRAN R](Summary%20of%20rx%20Functions.md).
+ Überprüfen Sie Ihre R-Code um festzustellen, ob es Schritte, die unabhängig ausgeführt oder effizienter gibt, mithilfe eines Aufrufs separate gespeicherte Prozedur ausgeführt werden können. Sie könnten z. B. Feature Engineering oder Feature Extraction separat ausführen und die Werte in eine neue Spalte hinzufügen. Verwenden Sie die T-SQL anstelle von R-Code für satzbasierte Berechnungen. Ein Beispiel für eine R-Lösung, die Leistung von UDFs und R für Aufgaben Funktion vergleicht, finden Sie in diesem Lernprogramm: [Data Science-End-to-End-Exemplarische Vorgehensweise](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md).  
  
    
## Einschränkungen    
 Beachten Sie die folgenden Einschränkungen bei der Konvertierung von R-Code:    
   
**Datentypen**    
-   Alle Arten von R werden unterstützt. Allerdings [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt eine größere Vielfalt von Datentypen als R, übernimmt, sodass einige implizite datentypkonvertierungen ausgeführt werden, beim Senden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Daten, r und umgekehrt. Explizit umgewandelt oder konvertieren eventuell Daten auch.    
    
- NULL-Werte werden unterstützt. R verwendet die `na` Daten erstellen Sie zum Darstellen von fehlenden Werten Null vergleichbar ist.    
    
- Weitere Informationen finden Sie unter [Arbeiten mit Datentypen R](../../advanced-analytics/r-services/working-with-r-data-types.md).    
 
 **Eingaben und Ausgaben**   
+ Sie können nur eine Eingabe-Dataset als Teil der Parameter der gespeicherten Prozedur definieren. Diese Eingabe Abfrage für die gespeicherte Prozedur kann eine beliebige gültige einzelne SELECT-Anweisung sein. Es wird empfohlen, diese Eingabe für das größte Dataset zu verwenden, und kleinere Datasets abrufen nach Bedarf durch Aufrufe RODBC. 

+ Die gespeicherte Prozedur ruft EXECUTE vorangestellt, die als Eingabe für Sp_execute_external_script verwendet werden können.    
    
+ Variablen im R-Skript müssen alle Spalten im Eingabedataset zugeordnet werden. Variablen werden automatisch nach Namen zugeordnet. Angenommen Sie, Ihre R-Skript enthält eine Formel wie diese:    
    
    ```    
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek    
    ```    
    
     Ein Fehler wird ausgelöst werden, wenn das Eingabe-Dataset enthält keine Spalten mit den entsprechenden Namen, ArrDelay, ID, DayOfWeek, CRSDepHour und DayOfWeek.    

+ Sie können auch mehrere skalare Parametern als Eingabe bereitstellen. Allerdings alle Variablen, die Sie als Parameter der gespeicherten Prozedur übergeben [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) müssen Variablen im R-Code zugeordnet werden. Standardmäßig werden die Variablen nach Namen zugeordnet.
+ Um skalare Variablen in der Ausgabe des R-Code einzuschließen, fügen Sie einfach die **Ausgabe** -Schlüsselwort, wenn Sie die Variable definieren.             
+ In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], Ihren R-Code ist nur ein einzelnes Dataset als data.frame Objekt ausgeben. Sie können jedoch auch ausgegeben Skalar ausgibt, einschließlich der Elemente im Binärformat und Modelle im Varbinary-Format.    
    
+ Sie können in der Regel das Dataset, das R-Skript zurückgegeben wird, ohne Namen von Ausgabespalten, geben Sie mithilfe der Option mit RESULT SETS UNDEFINED ausgeben. Allerdings müssen alle Variablen im R-Skript, das Sie ausgeben möchten SQL Output-Parametern zugeordnet werden.
    
+ Wenn Ihre R-Skript das-Argument verwendet `@parallel=1`, müssen Sie das Ausgabeschema definieren. Der Grund ist, dass mehrere Prozesse von SQL Server zum Ausführen der Abfrage parallel mit den Ergebnissen, die am Ende gesammelten erstellt werden können. Daher muss das Ausgabe-Schema definiert werden, bevor die parallele Prozesse erstellt werden können.

 **Abhängigkeiten**
 + Vermeiden Sie die Installation von Paketen aus R-Code. SQL Server sollte im Voraus Pakete installiert werden.  
  
  
  

