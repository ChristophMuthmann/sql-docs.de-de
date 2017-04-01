---
title: "Sicherheits&#252;bersicht (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# Sicherheits&#252;bersicht (SQL Server R Services)

In diesem Thema wird beschrieben, die gesamten Sicherheitsarchitektur, die verwendet wird, die Verbindung der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Datenbank-Engine und zugehörigen Komponenten zur Laufzeit R. Beispiele für den Prozess der Sicherheitsupdates stehen für zwei häufige Szenarios für die Verwendung von R in einem Unternehmen zur Verfügung:

+ Ausführen von RevoScaleR-Funktionen in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] von einem Data Science-Client
+ Ausführen von R direkt von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mithilfe von gespeicherten Prozeduren

## Sicherheitsübersicht

Ein [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Anmeldename oder Windows-Benutzerkonto ist erforderlich, um alle R-Aufträge ausgeführt werden, die nutzen [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. Der Anmeldename oder ein Benutzerkonto identifiziert die *Sicherheitsprinzipal*, benötigen, die über die Berechtigung zum Zugriff auf die Datenbank, wenn R ausgeführt wird, sowie Berechtigungen zum Lesen von Daten aus einer gesicherten Objekten wie Tabellen, oder zum Schreiben neuer Daten oder neue Objekte hinzuzufügen, ggf. durch den R-Auftrag.

Daher ist es zwingend erforderlich, jede Person, die R-Code wird ausgeführt für [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] muss eine Anmeldung in der Datenbank, unabhängig davon, ob dieser Code von einem remote Data Science-Client mithilfe der Funktionen RevoScaleR gesendet wird, oder mit einer T-SQL-Prozedur gestartet zugeordnet werden. 

Nehmen wir beispielsweise an, dass Sie erstellt einen R-Code, der auf Ihren Laptop ausgeführt wird, und Sie diesen Code ausführen möchten [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Sie müssen sicherstellen, dass die folgenden Bedingungen erfüllt sind:

+ Die Datenbank lässt Remoteverbindungen zu.
+ Mit dem Namen und das Kennwort, das Sie in den R-Code verwendet eine SQL-Anmeldung hinzugefügt wurde die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] auf Instanzebene. Oder, wenn Sie die integrierte Windows-Authentifizierung verwenden, muss in der Verbindungszeichenfolge angegebene Windows-Benutzer auf die Instanz als Benutzer hinzugefügt werden.
+ Der SQL-Anmeldung oder ein Windows-Benutzer muss die Berechtigung zum Ausführen von externen Skripts erteilt werden. Mit dieser Berechtigung kann in der Regel nur von einem Datenbankadministrator hinzugefügt werden.
+ Der SQL-Anmeldung oder ein Windows-Benutzer muss als Benutzer mit entsprechenden Berechtigungen können in jeder Datenbank hinzugefügt werden, bei denen der Auftrag R dieser Operationen ausführt:
    + Abrufen von Daten
    + Schreiben oder Aktualisieren von Daten 
    + Erstellen neuer Objekte, z. B. Tabellen oder gespeicherte Prozeduren

Nachdem die Anmeldung oder ein Windows-Benutzerkonto bereitgestellt und die erforderlichen Berechtigungen erteilt wurde, können Sie auf R-Code ausführen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mithilfe eines Datenquellenobjekts R oder durch Aufrufen von gespeicherten Prozeduren. Wenn R wird von gestartet, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], die Sicherheit der Datenbank-Engine Ruft den Sicherheitskontext des Benutzers, der den R-Auftrag gestartet und verwaltet die Zuordnung von der Benutzer- oder Anmeldename auf sicherungsfähige Objekte. 

Aus diesem Grund müssen alle R-Aufträge, die von einem Remoteclient aus initiiert werden die Anmeldenamen oder Benutzer als Teil der Verbindungszeichenfolge angeben.


## Interaktion von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Sicherheit und LaunchPad-Sicherheit

Wenn ein R-Skript ausgeführt wird, im Rahmen der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer, die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Dienst Ruft ein Konto Arbeitsthreads verfügbar (ein lokales Benutzerkonto) aus einem Pool von Konten für externe Prozess eingerichtet und verwendet dieses workerkonto für die verknüpften Aufgaben. 

Z. B. Wenn Sie Ihren Windows-Domänenanmeldeinformationen einen R-Auftrag zu starten, Ihrem Konto zugeordnet werden könnte dem Launchpad-Worker-Konto *SQLRUser01*.

Nach der Zuordnung zu einem Worker [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] erstellt ein Benutzertoken, die zum Starten von Prozessen verwendet wird. 

Wenn alle [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Vorgänge abgeschlossen sind, die Worker-Benutzerkonto als frei markiert und an den Pool zurückgegeben.

Weitere Informationen zu [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], finden Sie unter [neuer Komponenten in SQL Server, um R-Integration unterstützen](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md).

## Sicherheit der Konten
Diese Zuordnung eines externen Windows-Benutzer oder eine gültige SQL-Anmeldung mit einem workerkonto gilt nur für die Lebensdauer der Lebensdauer der SQL-Abfrage, die das R-Skript ausgeführt wird. 

Parallele Abfragen aus der gleichen Anmeldung werden auf dem gleichen Benutzerkonto Arbeitskraft zugeordnet.

Die Verzeichnisse, die für die Prozesse verwendet, die von verwaltet werden die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] mit RLauncher, und Verzeichnisse sind der Zugriff eingeschränkt. Der workerkonto kann nicht zugegriffen werden alle Dateien im Ordner über einen eigenen, jedoch können lesen, schreiben oder Löschen von untergeordneten Elementen im Ordner Sitzung arbeiten, die für die SQL-Abfrage mit dem R-Skript erstellt wurde.

Weitere Informationen dazu, wie Sie die Anzahl der Konten, Benutzernamen oder Kennwörter ändern, finden Sie unter [Ändern Sie den Benutzer-Konto-Pool für SQL Server-R-Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).


## Sicherheitsisolation für mehrere externe Skripts

Der Isolationsmechanismus basiert auf physischen Benutzerkonten. Wie Satelliten-Prozesse für eine bestimmte Sprachlaufzeit gestartet werden, verwendet jede Aufgabe Satelliten angegebene workerkonto der [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Wenn eine Aufgabe mehrere Satelliten erforderlich ist, wird z. B. bei parallelen Abfragen einen einzelnen Worker-Konto für alle Aufgaben verwendet.

Kein workerkonto kann finden Sie unter oder Bearbeiten von Dateien, die von anderen Konten verwendet.
 
Wenn Sie Administrator auf dem Computer sind, können Sie die Verzeichnisse erstellt für jeden Prozess anzeigen. Jedes Verzeichnis wird durch die Sitzung GUID identifiziert.

## Siehe auch
[Übersicht über die Architektur](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)