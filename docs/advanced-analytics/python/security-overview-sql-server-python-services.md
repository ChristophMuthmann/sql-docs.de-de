---
title: "Sicherheitsübersicht (SQL Server R Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ddfc3ccb67d017dc618cfbb7e7680c0164f3a21
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview"></a>Sicherheitsübersicht

In diesem Thema wird beschrieben, die Sicherheitsarchitektur, die verwendet wird, die Verbindung der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Datenbank-Engine und Python-Komponenten. Des Sicherheitsprozesses sind Beispiele für zwei gängige Szenarien: Ausführen von Python in SQL Server mithilfe einer gespeicherten Prozedur und Ausführen von Python mit dem SQL Server als remote computekontext.

## <a name="security-overview"></a>Sicherheitsübersicht

Ein [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Anmeldename oder Windows-Benutzerkonto ist erforderlich, um die Python-Skript in SQL Server ausführen. Gibt das Konto Anmeldenamen oder Benutzer an der *Sicherheitsprinzipal*, die über die Berechtigung für den Zugriff auf die Datenbank, in dem Daten aus abgerufen werden. Je nachdem, ob die Python-Skript neue Objekte erstellt oder neue Daten schreibt muss der Benutzer möglicherweise Berechtigungen zum Erstellen von Tabellen, Schreiben von Daten oder benutzerdefinierte Funktionen oder gespeicherte Prozeduren zu erstellen.

Daher ist es zwingend erforderlich, die jeder Person, die Python-Code ausführt in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] muss ein Anmeldename oder ein Konto in der Datenbank zugeordnet werden. Diese Einschränkung gilt unabhängig davon, ob das Skript von einem remote Data Science-Client gesendet wird oder mithilfe von T-SQL-Prozedur gestartet wurden.

Nehmen wir beispielsweise an, dass Sie erstellt ein Python-Skript, das auf Ihrem Laptop ausgeführt wird und Sie diesen Code ausführen möchten [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Sie müssen sicherstellen, dass die folgenden Bedingungen erfüllt sind:

+ Die Datenbank lässt Remoteverbindungen zu.
+ Die SQL-Anmeldung oder die Windows-Konto, das Sie für den Datenbankzugriff verwendet wurde hinzugefügt, um die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] auf Instanzebene.
+ Der SQL-Anmeldung oder dem Windows-Benutzer muss die Berechtigung zum Ausführen externer Skripts erteilt werden. Diese Berechtigung kann in der Regel nur von einem Datenbankadministrator hinzugefügt werden.
+ Die SQL-Anmeldung oder die Windows-Benutzer muss als Benutzer mit entsprechenden Berechtigungen in jeder Datenbank hinzugefügt werden, bei denen die Python-Skript für diese Vorgänge ausführt:
    + Abrufen von Daten
    + Schreiben oder Aktualisieren von Daten
    + Neue Objekte wie Tabellen oder gespeicherte Prozeduren erstellen

Nachdem die Anmeldung oder die Windows-Benutzerkonto bereitgestellt und die erforderlichen Berechtigungen erteilt wurde, können Sie die Python-Code ausführen, auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Datenquellenobjekte, die bereitgestellt werden, indem Sie mit der **Revoscalepy** -Bibliothek oder durch Aufrufen einer gespeicherten Prozedur, die Python-Skript enthält.

Wenn ein Python-Skript gestartet wird [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], die Sicherheit der Datenbank-Engine Ruft den Sicherheitskontext des Benutzers, der den Auftrag gestartet, und verwaltet die Zuordnungen von der Benutzer- oder Anmeldename auf sicherungsfähige Objekte ab.

Aus diesem Grund müssen alle Python-Skripts, die von einem Remoteclient aus initiiert werden die Anmeldenamen oder Benutzer als Teil der Verbindungszeichenfolge angeben.


## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interaktion von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Sicherheit und LaunchPad-Sicherheit

Wenn ein Python-Skript ausgeführt wird, im Rahmen der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer, die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Dienst Ruft ein Konto Arbeitsthreads verfügbar (ein lokales Benutzerkonto) aus einem Pool von Arbeitsthreads Konten für externe Prozesse eingerichtet und verwendet dieses workerkonto Verwandte Aufgaben.

Nehmen wir beispielsweise an, dass Sie ein Python-Skript mit Ihren Windows-Domänenanmeldeinformationen starten. SQL Server die Anmeldeinformationen abrufen und es verfügbaren Launchpad workerkonto zugeordnet, wie z. B. *SQLRUser01*.

> [!NOTE]
> Der Name der Gruppe von Konten ist identisch, unabhängig davon, ob Sie R oder Python verwenden. Allerdings wird eine separate Gruppe für jede Instanz erstellt, in dem Sie jeder externen Sprache aktivieren.

Nach der Zuordnung zu einem Workerkonto erstellt [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] ein Benutzertoken, das zum Starten von Prozessen verwendet wird. 

Wenn alle [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Vorgänge abgeschlossen sind, wird das Benutzerworkerkonto als frei markiert und an den Pool zurückgegeben.

Weitere Informationen zu [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], finden Sie unter [neue Komponenten in SQL Server-Unterstützung der Integration von Python](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md).

> [!NOTE]
> Für Launchpad, um die Worker-Konten verwalten und Ausführen von Python-Aufträge, die Gruppe, die Konten Worker enthält *SQLRUserGroup*, benötigen die Berechtigungen "Lokal anmelden zulassen"; andernfalls die Python-Laufzeit nicht gestartet werden kann. Standardmäßig erhält dieses Recht für alle neuen lokalen Benutzer jedoch in einigen Organisationen strengere Gruppenrichtlinien möglicherweise nicht erzwungen werden, die verhindern, dass die Konten Python Aufträge die Verbindung zu SQL Server.

## <a name="security-of-worker-accounts"></a>Sicherheit von Workerkonten

Die Zuordnung eines externen Windows-Benutzer oder die gültige SQL-Anmeldekennwort für ein workerkonto gilt nur für die Lebensdauer des SQL-Prozedur gespeicherte, die Python-Skript ausführt.

Parallele Abfragen von derselben Anmeldung werden demselben Benutzerworkerkonto zugeordnet.

Die Verzeichnisse, in denen für die Prozesse werden vom verwaltet die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], und Verzeichnisse werden Zugriff eingeschränkt. Für Python wird PythonLauncher diese Aufgabe ausgeführt. Jede einzelne workerkonto ist auf einem eigenen Ordner beschränkt und Dateien in Ordnern über eine eigene Ebene kann nicht zugegriffen werden kann. Allerdings kann das workerkonto lesen, schreiben oder löschen die untergeordneten Elemente unter den Arbeitsordner für Sitzung, der erstellt wurde.

Weitere Informationen dazu, wie Sie die Anzahl der Workerkonten, Kontonamen oder Kennwörter ändern können, finden Sie unter [Ändern des Benutzerkontenpools für SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).


## <a name="security-isolation-for-multiple-external-scripts"></a>Sicherheitsisolation für mehrere externe Skripts

Der Isolationsmechanismus basiert auf physischen Benutzerkonten. Da Satellitenprozesse für eine bestimmte Sprachlaufzeit gestartet werden, verwendet jede Satellitenaufgabe das von [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] angegebene Workerkonto. Wenn für eine Aufgabe mehrere Satelliten erforderlich sind, wie z.B. bei parallelen Abfragen, wird ein einziges Workerkonto für alle zusammenhängenden Aufgaben verwendet.

Kein Workerkonto kann Dateien finden oder bearbeiten, die von anderen Workerkonten verwendet werden.

Wenn Sie Administrator auf dem Computer sind, können Sie die Verzeichnisse anzeigen, die für jeden Prozess erstellt wurden. Jedes Verzeichnis wird durch die Sitzungs-GUID identifiziert.

## <a name="see-also"></a>Siehe auch

[Übersicht über die Architektur](../../advanced-analytics/python/architecture-overview-sql-server-python.md)

