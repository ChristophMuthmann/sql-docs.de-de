---
title: "Neue Komponenten in SQLServer zur Unterst&#252;tzung von R-Dienste | Microsoft Docs"
ms.custom: ""
ms.date: "06/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# Neue Komponenten in SQLServer zur Unterst&#252;tzung von R-Dienste

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] enthält die neue Komponenten, die aus der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Datenbank-Engine, die Erweiterbarkeit für die Sprache R zu unterstützen. Sicherheit für diese Komponenten verwaltet [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und wird später im Detail besprochen werden.

## Neue SQL Server-Komponenten und Anbietern

Zusätzlich zu der Shell, die lädt R und R-Code wie beschrieben in der Übersicht über die Architektur [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] dieser zusätzlichen Komponenten enthält.

### **Launchpad** 
  Die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] ist ein neuer Dienst, der von bereitgestellten [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] für die Ausführung des externen Skripts, ähnlich wie das, dass der Volltextsuchdienst Indizierung und Abfrage einen separaten Host startet, für die Verarbeitung von Volltextabfragen unterstützen. 
  
  Der Launchpad-Dienst startet nur vertrauenswürdigen Startprogramme, die von Microsoft veröffentlicht werden, oder, die von Microsoft als Meeting-Anforderungen für Leistung und Ressourcenmanagement zertifiziert. In [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)], R ist derzeit die einzige externe von unterstützte Sprache der [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)].
  
  Der [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] -Dienst unter seinem eigenen Benutzerkonto ausgeführt wird. Jeder Satelliten-Prozess für eine bestimmte Sprache-Laufzeit wird das Benutzerkonto des LaunchPads erben. Weitere Informationen zur Konfiguration und der Sicherheitskontext des LaunchPads finden Sie unter [Übersicht über die Sicherheit](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md).

### **BxlServer und SQL Satellitenassemblys**
  BxlServer ist eine ausführbare Datei, die von Microsoft, die Kommunikation zwischen verwaltet bereitgestellten [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und der R-Laufzeit, und auch implementiert ScaleR-Funktionen. Erstellt die Windows-Auftragsobjekte werden verwendet, um sichere Arbeitsordner Vorschriften für jeden Auftrag R, R Sitzungen enthalten SQL Satelliten verwendet, um die Datenübertragung zwischen R zu verwalten und [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  

  BxlServer ist eine Ergänzung zu, die mit R [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Unterstützung der Integration von R mit SQL Server. BXL steht für binäre Exchange Language und bezieht sich auf das Datenformat verwendet, um effizient Verschieben von Daten zwischen SQL Server und externe Prozesse wie R. 

 Die Satelliten-SQL ist eine neue Erweiterbarkeits-API in SQL Server 2016, die vom Datenbankmodul zur Unterstützung von externem Code oder externe Laufzeiten, die mit C oder C++ implementiert bereitgestellt wird. R ist derzeit die einzige unterstützte Runtime. BxlServer verwendet SQL Satellitenassembly für die Kommunikation mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
 
  Der SQL-Satelliten verwendet eine benutzerdefinierte Datenformat, das optimiert ist, für schnelle zwischen Datenübertragung [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und externen Skriptsprachen. Er führt Typumwandlungen und definiert die Schemas Eingabe- und Datasets, die während der Kommunikation zwischen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und R.

  BxlServer verwendet SQL Satelliten für diese Aufgaben: 
  - Lesen von Eingabedaten
  - Schreiben von Ausgabedaten
  - Eingabeargumente abrufen
  - Ausgabeargumente schreiben
  - Fehlerbehandlung
  - STDOUT und STDERR zurück auf den Client geschrieben

  Der SQL-Satelliten kann mithilfe von erweiterte Ereignisse überwacht werden. Weitere Informationen finden Sie unter [Extended Events für SQL Server-R-Services](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md).


## Der Kommunikationskanäle zwischen Komponenten

+ **TCP/IP** standardmäßig die interne Kommunikation zwischen den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und die SQL-Satelliten TCP/IP verwenden.

+ **Named Pipes**

  Interne Datenübertragung zwischen der BxlServer und [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] über Satelliten SQL verwendet Sie ein proprietäres, komprimierten Format zur Verbesserung der Leistung. Daten aus dem Speicher R BxlServer über named Pipes im Format BXL ausgetauscht. 
  
+ **ODBC** Kommunikation zwischen externen Data Science-Clients und die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanz ODBC verwenden. Das Konto, das die R sendet Aufträge auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] müssen beide Berechtigungen, mit der Instanz herstellen und externe Skripts auszuführen. Darüber hinaus muss das Konto über die Berechtigung zum Zugriff auf alle Daten, die vom Auftrag verwendet wird, zum Schreiben von Daten (z. B. Speichern von Ergebnissen in einer Tabelle) oder zum Erstellen von Datenbankobjekten (z. B., wenn der R-Funktionen als Teil einer neuen gespeicherten Prozedur zu speichern) haben.

  Wenn [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ist verwendet der Compute-Kontext für einen R-Auftrag gesendet wird, von einem Remoteclient aus, und der R-Befehl muss Daten aus einer externen Quelle abrufen, für das Rückschreiben ODBC verwendet wird. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] wird die Identität des Benutzers, den remoten-R-Befehl ausgibt, die Identität des Benutzers in der aktuellen Instanz zugeordnet, und führen Sie den ODBC-Befehl mit den Anmeldeinformationen des Benutzers. Die Verbindungszeichenfolge, die zum Durchführen dieser ODBC-Aufruf erforderlich sind, wird vom Clientcode abgerufen.
  
  Zusätzliche ODBC-Aufrufe erfolgen in das Skript mithilfe von **RODBC**. RODBC ist eine beliebte R-Paket, das Zugriff auf Daten in relationalen Datenbanken verwendet. die Leistung ist jedoch im Allgemeinen langsamer als vergleichbare Datenanbietern durch [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Viele R-Skripts verwenden eingebettete Aufrufe RODBC als eine Möglichkeit zum Abrufen von "sekundären" Datasets zur Verwendung in Analysen. Beispielsweise kann die gespeicherte Prozedur, die ein Modell trainiert definieren eine SQL-Abfrage zum Abrufen der Daten zum Trainieren eines Modells, aber verwenden Sie einen eingebetteten RODBC-Aufruf zum Abrufen zusätzlicher Faktoren beeinflusst werden, um Suchvorgänge auszuführen, oder zum Abrufen neuer Daten aus externen Quellen wie Textdateien oder Excel.

  Der folgende Code zeigt einen RODBC-Aufruf in einem R-Skript eingebettet:
   ~~~~
  library(RODBC);
  connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
  dbhandle <- odbcDriverConnect(connStr)
  OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
  ~~~~

+ **Andere Protokolle** Prozesse, die möglicherweise in "Blöcken" arbeiten oder Übertragen von Daten an einem remote-Client können Sie auch die. Von Microsoft r tatsächliche Datenübertragung unterstützten XDF-Format erfolgt über codierte Blobs.

## Interaktion von Komponenten

Die soeben beschriebene Architektur um zu garantieren, dass die open-Source-R-Code arbeiten kann, "wie besehen" bereitgestellt wurde, während die Bereitstellung erheblich erhöht Leistung für Code, der ausgeführt wird, auf einem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer. Der Mechanismus für die Interaktion der Komponenten mit der R-Laufzeit und die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Datenbankmodul unterscheidet sich geringfügig, je nachdem, wie der R-Code aufgerufen wird. In diesem Abschnitt werden die wichtigsten Szenarien zusammengefasst. 
 
### R-Skripts, die Ausführung von SQL Server (in der Datenbank)

R-Code, der von "Inside" ausgeführt wird, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] durch Aufrufen einer gespeicherten Prozedur ausgeführt wird. Daher kann jede Anwendung, die eine gespeicherte Prozedur aufrufen können R-Code Ausführung zu starten.  Danach [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] verwaltet die Ausführung von R-Code, wie in der folgenden Abbildung zusammengefasst.

![rsql_indb780-01](../../advanced-analytics/r-services/media/rsql-indb780-01.png)

1. Eine Anforderung für die Laufzeit R angegeben, durch den Parameter _@language 'R' =_ an die gespeicherte Prozedur übergeben [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] sendet diese Anforderung an den Launchpad-Dienst.
2. Der Launchpad-Dienst startet der entsprechenden Startprogramm; In diesem Fall RLauncher.
3. RLauncher startet den externen Prozess von R.
4. BxlServer-Koordinaten mit der R-Laufzeit zum Verwalten der Austausch von Daten mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und Speicherung von Ergebnissen arbeiten.
5. Über den gesamten, SQL verwaltet die Kommunikation über verwandte Aufgaben und Prozesse mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
6. BxlServer verwendet SQL Satelliten Status kommunizieren und zu Ergebnissen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Ruft die Ergebnisse ab und schließt Aufgaben und Prozesse. 


### R-Skripts, die von einem Remoteclient ausgeführt

Wenn von einem remote Data Science-Client eine Verbindung herstellen, die Microsoft R unterstützt, können Sie R-Funktionen ausführen, im Kontext des [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mithilfe der ScaleR-Funktionen. Dies ist von einem anderen Workflow aus dem vorherigen Beispiel und ist in der folgenden Abbildung zusammengefasst.


![rsql_fromR2db-01](../../advanced-analytics/r-services/media/rsql-fromr2db-01.png)

1. Für ScaleR-Funktion ruft die R-Laufzeit eine Verbindungsfunktion die BxlServer wiederum aufruft. 
2. BxlServer ist in Microsoft R und in einem separaten Prozess ausgeführt wird, aus der R-Laufzeit.
3. BxlServer bestimmt das Verbindungsziel und initiiert eine Verbindung mithilfe von ODBC, Anmeldeinformationen, die als Teil der Verbindungszeichenfolge in das R-Objekt übergeben.
4. BxlServer öffnet eine Verbindung mit der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanz.
5. Ein R-Aufruf, der LaunchPad-Dienst aufgerufen wird, startet also Turn der entsprechenden Startprogramm RLauncher. Anschließend ist die Verarbeitung von R-Code ähnelt dem Prozess zum Ausführen von R-Code von T-SQL.
6. RLauncher Ruft die Instanz des R-Laufzeit, der auf den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer. 
7. Ergebnisse werden an BxlServer zurückgegeben.
8. SQL-Satelliten verwaltet die Kommunikation mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und der entsprechenden Auftragsobjekte bereinigt.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Ergebnisse werden zurück an den Client weitergegeben.

## Siehe auch
[Übersicht über die Architektur](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)
