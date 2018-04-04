---
title: Zur Unterstützung von R-Komponenten in SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: cc9f600d6bfce5d522abb8452800c35f41069b92
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="components-in-sql-server-to-support-r"></a>Zur Unterstützung von R-Komponenten in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In SQL Server 2016 und 2017 enthält das Datenbankmodul optionale Komponenten, die Erweiterbarkeit für externe Skriptsprachen, einschließlich R und Python zu unterstützen. Unterstützung für die Sprache "R" wurde in SQL Server 2016 hinzugefügt; Unterstützung für Python in SQL Server 2017 Machine Learning Services hinzugefügt wurde.

Dieses Thema beschreibt die neuen Komponenten, die speziell für die Sprache "R" arbeiten. Eine Erläuterung der Funktionsweise dieser Komponenten mit open Source-R, finden Sie unter [R-Interoperabilität](r-interoperability-in-sql-server.md)

## <a name="components-and-providers"></a>Komponenten und Anbietern

Zusätzlich zur Shell, die R lädt und R-Code so wie in der Übersicht über die Architektur ausführt, enthält [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] diese zusätzlichen Komponenten.

### <a name="launchpad"></a>Launchpad 

Die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] ist ein Dienst gebotenen [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] für die Unterstützung der Ausführung externer Skripts, ähnlich wie bei, dass der Volltextsuchdienst indizierungs- und Abfragefunktionen einen separaten Host wird gestartet, für die Verarbeitung von Volltextabfragen.

Der Launchpad-Dienst startet nur vertrauenswürdige Startprogramme, die von Microsoft veröffentlicht wurden oder die durch Microsoft zertifiziert wurden, da sie die Anforderungen für Leistung und Ressourcenverwaltung erfüllen. Die Benennung für das die sprachspezifische Startprogramme ist einfach:

  + R - Datei "rlauncher.dll"
  + Python - PythonLauncher.dll

Der [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]-Dienst wird unter dem eigenen Benutzerkonto ausgeführt. Jeder Satellitenprozess für eine bestimmte Sprachlaufzeit erbt das Benutzerkonto des Launchpads. Weitere Informationen zur Konfiguration und der Sicherheitskontext des Launchpad finden Sie unter [Sicherheitsübersicht](../../advanced-analytics/r/security-overview-sql-server-r.md).

### <a name="bxlserver-and-sql-satellite"></a>BxlServer und SQL-Satelliten

BxlServer ist eine ausführbare Datei, die von Microsoft, die Kommunikation zwischen verwaltet bereitgestellten [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und den R-Laufzeit, und auch implementiert RevoScaleR-Funktionen. Sie erstellt die Windows-Auftragsobjekte, die R-Sitzungen enthalten, sichere Arbeitsordner für jeden R-Auftrag bereitstellen und den SQL-Satellit zum Verwalten von Datenübertragungen zwischen R und [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] verwenden.

Daher ist BxlServer ein Begleiter für R, der mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] arbeitet, um die Integration von R mit SQL Server zu unterstützen. BXL steht für binäre Exchange-Sprache und bezieht sich auf das Datenformat verwendet, um Daten effizient zwischen SQL Server und externen Prozessen verschieben, z. B. r BxlServer.dll bei der Installation von Microsoft R-Client oder Microsoft R Server ebenfalls installiert ist.

Der SQL-Satellit ist eine neue Erweiterbarkeits-API in SQL Server 2016, die durch das Datenbankmodul bereitgestellt wurde, um externen Code oder externe Laufzeiten, die mithilfe von C oder C++ implementiert wurden, zu unterstützen. BxlServer verwendet den SQL-Satelliten für die Kommunikation mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Der SQL-Satellit verwendet ein benutzerdefiniertes Datenformat, der für die schnelle Datenübertragung zwischen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und externen Skriptsprachen optimiert wird. Er führt Typumwandlungen durch und definiert die Schemas der Eingabe- und Ausgabedatasets während der Kommunikation zwischen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und R.

BxlServer verwendet den SQL-Satelliten für die folgenden Aufgaben:.

  + Lesen von Eingabedaten
  + Schreiben von Ausgabedaten
  + Abrufen von Eingabeargumenten
  + Schreiben von Ausgabeargumenten
  + Fehlerbehandlung
  + Die Standardausgabe geschrieben und Fehler an den Client zurück

Der SQL-Satellit kann mithilfe von erweiterten Ereignissen überwacht werden. Weitere Informationen finden Sie unter [Erweiterte Ereignisse bei SQL Server R Services](extended-events-for-sql-server-r-services.md).

## <a name="communication-channels-between-components"></a>Kommunikationskanäle zwischen Komponenten

+ **TCP/IP**

    Standardmäßig sind interne Kommunikation zwischen den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und den SQL-Satelliten TCP/IP verwenden.

+ **Named Pipes**

    Interne die Datenübertragung zwischen der BxlServer und [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] über SQL-Satelliten wird im Format proprietären, komprimierte Daten zur Verbesserung der Leistung. Daten aus dem R-Speicher werden über Named Pipes im BXL-Format mit BxlServer ausgetauscht.

+ **ODBC**

    Kommunikation zwischen externen Data Science-Clients und die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanz verwenden von ODBC. Das Konto, das R-Aufträge an [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] übermittelt, muss über beide Berechtigungen verfügen, um eine Verbindung mit der Instanz herzustellen, um externe Skripts auszuführen. Darüber hinaus muss das Konto über Berechtigungen zum Zugriff auf Daten verfügen, die vom Auftrag verwendet werden, um Daten zu schreiben (z.B. wenn Sie Ergebnisse in einer Tabelle speichern) oder um Datenbankobjekte zu erstellen (als wenn Sie z.B. R-Funktionen als Teil einer neuen gespeicherten Prozedur speichern).

    Wenn [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] als Computekontext für einen R-Auftrag verwendet wird, der von einem Remotclient gesendet wird, und der R-Befehl Daten aus einer externen Quelle abrufen muss, wird ODBC für den Rückschreibevorgang verwendet. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ordnet die Identität des Benutzers zu, der den remoten R-Befehl an die Identität des Benutzers auf der aktuellen Instanz ausgibt, und führt den ODBC-Befehl mithilfe der Anmeldeinformationen dieses Benutzers aus. Die Verbindungszeichenfolge, die zum Durchführen dieses ODBC-Aufruf erforderlich ist, wird vom Clientcode abgerufen.

    Zusätzliche ODBC-Aufrufe können innerhalb des Skripts mithilfe von **RODBC** erfolgen. RODBC ist eine beliebte R-Paket, das für den Zugriff auf Daten in relationalen Datenbanken verwendet wird. Die Leistung ist jedoch im Allgemeinen langsamer als die von vergleichbaren Anbietern, die von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] verwendet werden. Viele R-Skripts verwenden eingebettete Aufrufe auf RODBC als eine Möglichkeit, „sekundäre“ Datasets für den Gebrauch in Analysen abzurufen. Beispielsweise kann die gespeicherte Prozedur, die ein Modell trainiert, möglicherweise eine SQL-Abfrage definieren, um die Daten für das Trainieren eines Modells abzurufen, aber einen eingebetteten RODBC-Aufruf zum Abrufen zusätzlicher Faktoren verwenden, um Lookups auszuführen oder um neue Daten aus externen Quellen zu erhalten, z.B. Textdateien oder Excel.

    Der folgende Code zeigt einen RODBC-Aufruf, der in einem R-Skript eingebettet ist:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Andere Protokolle**

    Prozesse, die möglicherweise funktionieren in "datenrationen", oder übertragen Sie die Daten wieder mit einem Remoteclient können auch die. XDF-Format unterstützt, die von Microsoft r tatsächliche Datenübertragung erfolgt über codierte Blobs.

## <a name="interaction-of-components"></a>Interaktion von Komponenten

Die soeben beschriebene Komponentenarchitektur wurde bereitgestellt, um zu garantieren, dass Open-Source-R-Code „unverändert“ ausgeführt werden kann, wobei erheblich gesteigerte Leistung für Code, der auf einem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Computer ausgeführt wird, bereitgestellt wird. Der Mechanismus, wie Komponenten mit der R-Laufzeit und dem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Datenbankmodul interagieren, kann je nachdem wie der R-Code gestartet wird, leicht variieren. In diesem Abschnitt werden die wichtigsten Szenarios zusammengefasst.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>R-Skripts, die von SQL Server in-Database ausgeführt

R-Code, der „innerhalb“ von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ausgeführt wird, wird durch Aufruf einer gespeicherten Prozedur ausgeführt. Daher kann jede Anwendung, die eine gespeicherte Prozedur aufrufen kann, die Ausführung von R-Code initiieren.  Anschließend verwaltet [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] die Ausführung von R-Code, wie im folgenden Diagramm dargestellt wird.

![rsql_indb780-01](media/script_in-db-r.png)

1. Eine Anforderung für die R-Laufzeit wird vom Parameter _@language='R'_ indiziert, der an die gespeicherte Prozedur [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) übergeben wird. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] sendet diese Anforderung an den Launchpad-Dienst.
2. Der Launchpad-Dienst startet das entsprechende Startprogramm; In diesem Fall „RLauncher“.
3. RLauncher startet den externen Prozess von R.
4. BxlServer koordiniert mit der R-Laufzeit, um die Austauschvorgänge von Daten mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und der Speicherung von Arbeitsergebnissen zu verwalten.
5. SQL-Satelliten verwaltet die Kommunikation über verwandte Aufgaben und Prozesse mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
6. BxlServer verwendet SQL-Satelliten, um den Status und die Ergebnisse mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] zu kommunizieren.
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ruft die Ergebnisse ab und schließt verwandte Aufgaben und Prozesse.

### <a name="r-scripts-executed-from-a-remote-client"></a>Von einem Remoteclient ausgeführte R-Skripts

Wenn von einem remote Data Science-Client eine Verbindung herstellen, die von Microsoft R unterstützt, können Sie R-Funktionen ausführen, im Kontext der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mithilfe der RevoScaleR-Funktionen. Dieser Workflow unterscheidet sich vom vorherigen und wird im folgenden Diagramm zusammengefasst.

![rsql_fromR2db-01](media/remote-sqlcc-from-r2.png)

1. Die R-Laufzeit ruft eine verknüpfende Funktion, die ihrerseits BxlServer RevoScaleR-Funktionen.
2. BxlServer wird in Microsoft R und in einem separaten Prozess von der R-Laufzeit bereitgestellt.
3. BxlServer bestimmt das Verbindungsziel und initiiert eine Verbindung mithilfe von ODBC, wobei Anmeldeinformationen, die als Teil der Verbindungszeichenfolge im R-Datenquellenprojekt bereitgestellt werden, übergeben werden.
4. BxlServer öffnet eine Verbindung mit der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz.
5. Die ist gestartet für einen R-Aufruf, der Launchpad-Dienst aufgerufen wird, wird das entsprechende-Startprogramm RLauncher. Die Verarbeitung von R-Code ähnelt dem Vorgang, R-Code von T-SQL auszuführen.
6. RLauncher ruft die Instanz der R-Laufzeit ab, die auf dem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Computer gespeichert ist.
7. Ergebnisse werden an BxlServer zurückgegeben.
8. Der SQL-Satellit verwaltet die Kommunikation mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] und der Bereinigung verwandter Auftragsobjekte.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] gibt die Ergebnisse dem Client zurück.

## <a name="next-steps"></a>Nächste Schritte

[Übersicht über die Architektur](architecture-overview-sql-server-r.md)

[Sicherheitsübersicht](security-overview-sql-server-r.md)

[Überlegungen zur Sicherheit](security-considerations-for-the-r-runtime-in-sql-server.md)
