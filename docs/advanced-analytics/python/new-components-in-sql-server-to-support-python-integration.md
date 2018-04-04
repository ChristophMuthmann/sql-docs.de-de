---
title: Komponenten für die Python-Integration in SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/03/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: a35b592ef3d6d89bb3014962b9fca80816240315
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="components-in-sql-server-to-support-python-integration"></a>Komponenten in SQL Server zur Unterstützung der Python-integration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Ab SQL Server 2017 unterstützt Machine Learning Services Python als externe Sprache, die von T-SQL ausgeführt werden kann, oder Remote mithilfe von SQL Server als computekontext ausgeführt.

Dieses Thema beschreibt die Komponenten in SQL Server-2017, die Erweiterungen im Allgemeinen unterstützen und die Sprache Python speziell an.

## <a name="sql-server-components-and-providers"></a>SQL Server-Komponenten und Anbietern

So konfigurieren Sie SQL Server-2017 zum Ausführen von Python-Skripts ermöglichen die ist ein mehrstufiger Prozess aus.

1. Installieren Sie die Erweiterbarkeitsfunktion.
2. Aktivieren Sie die externen Skript Ausführung-Funktion.
3. Starten Sie den Datenbank-Engine-Dienst neu.

Remoteausführung von Skripts zu unterstützen, können zusätzliche Schritte erforderlich sein.

Weitere Informationen finden Sie unter [installieren Sie SQL Server 2017 Machine Learning Services (Datenbankintern)](../install/sql-machine-learning-services-windows-install.md).

### <a name="launchpad"></a>Launchpad

SQL Server vertrauenswürdige Launchpad handelt es sich um einen Dienst, eingeführt in SQL Server 2016, die verwaltet und externer Skripts, ähnlich wie bei, dass der Volltextsuchdienst indizierungs- und Abfragefunktionen einen separaten Host wird gestartet, für die Verarbeitung von Volltextabfragen ausführt.

Der Launchpad-Dienst starten, die von Microsoft veröffentlicht werden, oder, die von Microsoft als Besprechung Anforderungen für Leistung und Ressourcenmanagement zertifiziert, nur vertrauenswürdigen Startprogramme.

+ SQL Server-2017 unterstützt R und Python 3.5
+ SQL Server 2016 unterstützt R

Der [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]-Dienst wird unter dem eigenen Benutzerkonto ausgeführt.

> [!TIP]
> Wenn Sie das Konto, das Launchpad ausgeführt wird ändern, achten Sie darauf, dass Sie in diesem Fall verwandten Dateien mithilfe von SQL Server-Konfigurations-Manager, um sicherzustellen, dass Änderungen in geschrieben werden.

Zum Ausführen von Aufgaben in einer bestimmten unterstützten Sprache, dem Launchpad Ruft eine gesicherte workerkonto aus dem Pool ab und startet einen satellitenprozess zum Verwalten von externen Runtime:

+ Datei "rlauncher.dll" für die Sprache "R"
+ PythonLauncher.dll für Python 3.5

Jeder satellitenprozess erbt das Benutzerkonto des Launchpad und verwendet das workerkonto dieses für die Dauer der Ausführung des Skripts. Wenn die Python-Skript parallele Prozessen verwendet wird, werden sie unter dem workerkonto dieselbe, einzelne erstellt.

Weitere Informationen zu den Sicherheitskontext des LaunchPads, finden Sie unter [Sicherheit](security-overview-sql-server-python-services.md).

### <a name="bxlserver-and-sql-satellite"></a>BxlServer und SQL-Satelliten

Wenn das Ausführen [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) während ein Python-Auftrag ausgeführt wird, wird möglicherweise eine oder mehrere Instanzen von BxlServer.

**BxlServer** ist eine ausführbare Datei, die von Microsoft, die Kommunikation zwischen verwaltet bereitgestellten [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und Python (oder R). Erstellt die Windows-Auftrag-Objekte, die werden verwendet, um externen Skript Sitzungen Vorschriften sichere Arbeitsordner für jeden Auftrag externes Skript enthalten, und verwendet SQL-Satelliten zum Verwalten der Datenübertragung zwischen der externen Runtime und [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

BxlServer ist eine Ergänzung zur Python, die mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Daten zu übertragen und Aufgaben verwalten. BXL steht für binäre Exchange-Sprache und bezieht sich auf das Datenformat verwendet, um Daten effizient zwischen SQL Server und externen Prozessen zu verschieben. BxlServer ist auch ein wichtiger Teil der Microsoft-R-Client und Microsoft R Server.

**SQL-Satelliten** ist ein Erweiterbarkeits-API, in das Datenbankmodul, beginnend mit SQL Server 2016, die von externem Code unterstützt enthalten oder externen Laufzeiten, die mit C oder C++ implementiert.

BxlServer verwendet den SQL-Satelliten für die folgenden Aufgaben:.

+ Lesen von Eingabedaten
+ Schreiben von Ausgabedaten
+ Abrufen von Eingabeargumenten
+ Schreiben von Ausgabeargumenten
+ Fehlerbehandlung
+ STDOUT und STDERR zurück auf den Client schreiben

SQL-Satelliten verwendet eine benutzerdefinierte Datenformat, der optimiert ist, für schnelle zwischen Datenübertragung [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und externen Skriptsprachen. Er führt Konvertierungen und definiert die Schemas Eingabe- und Datasets, die während der Kommunikation zwischen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und die externe Skriptlaufzeit.

Die SQL-Satelliten kann mithilfe von Windows, die erweiterte Ereignisse (xEvents) überwacht werden. Weitere Informationen finden Sie unter [Extended Events for R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md).

## <a name="communication-channels-between-components"></a>Kommunikationskanäle zwischen Komponenten

+ **TCP/IP**

  Standardmäßig sind interne Kommunikation zwischen den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und den SQL-Satelliten TCP/IP verwenden.

+ **Named Pipes**

  Der interne Datentransport zwischen BxlServer und [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] über den SQL-Satelliten verwendet ein proprietäres, komprimiertes Datenformat, um die Leistung zu steigern. Daten werden im BXL-Format mithilfe von Named Pipes zwischen Python und BxlServer ausgetauscht.

+ **ODBC**

  Kommunikation zwischen externen Data Science-Clients und die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanz verwenden von ODBC. Das Konto, das das Skript wird gesendet, um Aufträge [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] müssen beide Berechtigungen für die Verbindung mit der Instanz sowie zum Ausführen externer Skripts.

  Darüber hinaus kann das Konto abhängig von der Aufgabe diese Berechtigungen erforderlich:

  + Lesen von Daten, die vom Auftrag verwendete
  + Daten in Tabellen geschrieben werden: z. B. beim Speichern der Ergebnisse an eine Tabelle
  + Erstellen von Datenbankobjekten: z. B., wenn externes Skript als Teil einer neuen gespeicherten Prozedur zu speichern.

  Wenn [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] wird als computekontext für Python-Skript ausgeführt wird, von einem Remoteclient aus, und die ausführbare Datei aus Python muss Daten aus einer externen Quelle abrufen verwendet, für das Rückschreiben ODBC verwendet wird. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Ordnet die Identität des Benutzers remote Befehl ausgeben, um die Identität des Benutzers auf die aktuelle Instanz und den ODBC-Befehl mit den Anmeldeinformationen des Benutzers ausgeführt. Die Verbindungszeichenfolge, die zum Durchführen dieses ODBC-Aufruf erforderlich ist, wird vom Clientcode abgerufen.

## <a name="interaction-of-components"></a>Interaktion von Komponenten

Die folgenden Diagramme stellen die Interaktion von SQL Server-Komponenten mit der Python-Laufzeit in jedes der unterstützten Szenarien: Ausführen von Skripts in der Datenbank und remote von einem Python-Terminal, verwenden einen SQL Server-computekontext ausgeführt.

### <a name="python-scripts-executed-in-database"></a>Python-Skripts ausgeführt, in der Datenbank

Beim Ausführen von Python "interne" [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], müssen Sie die Python-Skript in einer speziellen gespeicherten Prozedur kapseln [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Nachdem das Skript in der gespeicherten Prozedur eingebettet wurde, kann jede Anwendung, die eine gespeicherte Prozedur aufrufen können Ausführung der Python-Code starten.  Danach [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] codeausführung verwaltet, wie in der folgenden Abbildung zusammengefasst.

![Skript in Db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Eine Anforderung für die Python-Laufzeit wird angegeben, durch den Parameter `@language='Python'` an die gespeicherte Prozedur übergeben. SQL Server sendet diese Anforderung an den Launchpad-Dienst.
2. Der Launchpad-Dienst gestartet wird, das entsprechende Startprogramm; In diesem Fall PythonLauncher.
3. PythonLauncher startet den externen Prozess von Python35.
4. BxlServer die Koordination mit der Python-Laufzeit-Datenaustausch und Speicherung von arbeiten Ergebnisse zu verwalten.
5. SQL-Satelliten verwaltet die Kommunikation über verwandte Aufgaben und Prozesse mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
6. BxlServer verwendet SQL-Satelliten, um den Status und die Ergebnisse mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zu kommunizieren.
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ruft die Ergebnisse ab und schließt verwandte Aufgaben und Prozesse.

### <a name="python-scripts-executed-from-a-remote-client"></a>Python-Skripts, die von einem Remoteclient ausgeführt

Sie können Ausführen von Python-Skripts von einem Remotecomputer, z. B. einen Laptop, und bitten, dass im Kontext der SQl Server-Computer ausgeführt werden, wenn diese Bedingungen erfüllt sind:

+ Die Skripts entwerfen entsprechend
+ Der Remotecomputer wurde die Erweiterbarkeit Bibliotheken installiert, die von Machine Learning-Diensten verwendet werden. Die [Revoscalepy](what-is-revoscalepy.md) Paket ist erforderlich, um remote rechenkontexte verwenden.

Das folgende Diagramm fasst den gesamten Workflow an, wenn Skripts von einem Remotecomputer gesendet werden.

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. Für Funktionen, die unterstützt werden **Revoscalepy**, die Python-Laufzeit ruft eine verknüpfungsframework-Funktion, die ihrerseits BxlServer.
2. BxlServer ist im Lieferumfang von Machine Learning-Services (Datenbankintern) und in einem separaten Prozess ausgeführt wird, aus der Python-Laufzeit.
3. BxlServer bestimmt das Verbindungsziel und initiiert eine Verbindung mithilfe von ODBC, Anmeldeinformationen, die als Teil der Verbindungszeichenfolge in der Python-Skript übergeben.
4. BxlServer öffnet eine Verbindung mit der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz.
5. Wenn eine externe Skriptlaufzeit aufgerufen wird, wird der Launchpad-Dienst aufgerufen wird, dem beginnt wiederum des entsprechenden Startprogramms: in diesem Fall PythonLauncher.dll. Danach wird der Verarbeitung von Python-Code in einem Workflow ähnelt der behandelt, wenn von einer gespeicherten Prozedur in T-SQL-Python-Code aufgerufen wird.
6. PythonLauncher führt einen Aufruf an die Instanz von der Python, die auf installiert ist die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer.
7. Ergebnisse werden an BxlServer zurückgegeben.
8. Der SQL-Satellit verwaltet die Kommunikation mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und der Bereinigung verwandter Auftragsobjekte.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] gibt die Ergebnisse dem Client zurück.

## <a name="next-steps"></a>Nächste Schritte

[Übersicht über die Architektur für Python in SQL Server](architecture-overview-sql-server-python.md)
