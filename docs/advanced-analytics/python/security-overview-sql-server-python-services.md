---
title: "Übersicht über die Sicherheit für Python in SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 422b1e72c38493b2092a8682ade5077069af24f0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="security-overview-for-python-in-sql-server"></a>Übersicht über die Sicherheit für Python in SQL Server

In diesem Thema wird beschrieben, die Sicherheitsarchitektur, die verwendet wird, die Verbindung der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Datenbank-Engine und Python-Komponenten. Des Sicherheitsprozesses sind Beispiele für zwei gängige Szenarien: Ausführen von Python in SQL Server mithilfe einer gespeicherten Prozedur und Ausführen von Python mit dem SQL Server als remote computekontext.

## <a name="security-overview"></a>Sicherheit (Übersicht)

Ein [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Anmeldename oder Windows-Benutzerkonto ist erforderlich, um die Python-Skript in SQL Server ausführen. Diese *Sicherheitsprinzipale* auf Instanz- und Datenbankebene und verwaltet werden und Benutzer, die über die Berechtigung zum Herstellen einer Verbindung mit der Datenbank, zu lesen und Schreiben von Daten zu identifizieren oder Erstellen von Datenbankobjekten, z. B. Tabellen oder gespeicherte Prozeduren. Darüber hinaus müssen Benutzer, die Python-Skript ausführen, über die Berechtigung zum Ausführen externer Skripts auf Datenbankebene verfügen.

Selbst Benutzer, die mithilfe von Python in einem externen Tool müssen auf einen Anmeldenamen oder das Konto in der Datenbank zugeordnet werden, wenn der Benutzer zum Ausführen von Python-Code in der Datenbank, oder den Zugriff auf Datenbankobjekte und Daten muss. Die gleichen Berechtigungen sind erforderlich, gibt an, ob die Python-Skript von einem remote Data Science-Client gesendet wird, oder mit T-SQL-Prozedur gestartet wird.

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

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interaktion von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Sicherheits- und Launchpad

Wenn ein Python-Skript ausgeführt wird, im Rahmen der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer, die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Dienst Ruft ein Konto Arbeitsthreads verfügbar (ein lokales Benutzerkonto) aus einem Pool von Arbeitsthreads Konten für externe Prozesse eingerichtet und verwendet dieses workerkonto Verwandte Aufgaben.

Nehmen wir beispielsweise an, dass Sie ein Python-Skript mit Ihren Windows-Domänenanmeldeinformationen starten. SQL Server ruft die Anmeldeinformationen ab und ordnet die Aufgabe zu einem verfügbaren Launchpad Worker-Konto, z. B. *SQLRUser01*.

> [!NOTE]
> Der Name der Gruppe von Konten ist identisch, unabhängig davon, ob Sie R oder Python verwenden. Allerdings wird eine separate Gruppe für jede Instanz erstellt, in dem Sie jeder externen Sprache aktivieren.

Nach der Zuordnung zu einem Workerkonto erstellt [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] ein Benutzertoken, das zum Starten von Prozessen verwendet wird. 

Wenn alle [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Vorgänge abgeschlossen sind, wird das Benutzerworkerkonto als frei markiert und an den Pool zurückgegeben.

Weitere Informationen zu [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], finden Sie unter [Komponenten in SQL Server zur Unterstützung der Integration von Python](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md).

### <a name="implied-authentication"></a>Implizite Authentifizierung

**Implizite Authentifizierung** wird der Begriff für den Prozess, unter dem SQL Server der Benutzer erhält, verwendet die Anmeldeinformationen, und führt dann alle externen Skript-Aufgaben im Auftrag von den Benutzern, vorausgesetzt der Benutzer die richtigen Berechtigungen besitzt, in der Datenbank. Implizite Authentifizierung ist besonders wichtig, wenn die Python-Skript einen ODBC-Aufruf außerhalb der SQL Server-Datenbank ausführen muss. Der Code kann z. B. eine kürzere Listen von Faktoren aus einem Tabellenblatt oder einer anderen Quelle abgerufen werden.

Für solche Loopback-Aufrufe erfolgreich ausgeführt werden kann muss die Gruppe mit den Konten, SQLRUserGroup, aus "Lokal anmelden zulassen" berechtigt. Standardmäßig erhält dieses Recht für alle neuen lokalen Benutzer jedoch in einigen Organisationen strengere Gruppenrichtlinien erzwungen werden können.

![Implizite Authentifizierung für R](media/implied-auth-python2.png)

## <a name="security-of-worker-accounts"></a>Sicherheit der Konten

Die Zuordnung eines externen Windows-Benutzer oder die gültige SQL-Anmeldekennwort für ein workerkonto gilt nur für die Lebensdauer des SQL-Prozedur gespeicherte, die Python-Skript ausführt.

Parallele Abfragen von derselben Anmeldung werden demselben Benutzerworkerkonto zugeordnet.

Die Verzeichnisse, in denen für die Prozesse werden vom verwaltet die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], und Verzeichnisse werden Zugriff eingeschränkt. Für Python wird PythonLauncher diese Aufgabe ausgeführt. Jede einzelne workerkonto ist auf einem eigenen Ordner beschränkt und Dateien in Ordnern über eine eigene Ebene kann nicht zugegriffen werden kann. Allerdings kann das workerkonto lesen, schreiben oder löschen die untergeordneten Elemente unter den Arbeitsordner für Sitzung, der erstellt wurde.

Weitere Informationen dazu, wie Sie die Anzahl der Konten, Kontonamen oder Kennwörter ändern, finden Sie unter [Ändern des benutzerkontenpools für SQL Server-Machine Learning](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).


## <a name="security-isolation-for-multiple-external-scripts"></a>Die Sicherheitsisolation für mehrere externe Skripts

Der Mechanismus für die Sicherheitsisolation basiert auf physischen Benutzerkonten. Da Satellitenprozesse für eine bestimmte Sprachlaufzeit gestartet werden, verwendet jede Satellitenaufgabe das von [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] angegebene Workerkonto. Wenn für eine Aufgabe mehrere Satelliten erforderlich sind, wie z.B. bei parallelen Abfragen, wird ein einziges Workerkonto für alle zusammenhängenden Aufgaben verwendet.

Kein Workerkonto kann Dateien finden oder bearbeiten, die von anderen Workerkonten verwendet werden.

Wenn Sie Administrator auf dem Computer sind, können Sie die Verzeichnisse anzeigen, die für jeden Prozess erstellt wurden. Jedes Verzeichnis wird durch die Sitzungs-GUID identifiziert.

## <a name="see-also"></a>Siehe auch

[Übersicht über die Architektur](../../advanced-analytics/python/architecture-overview-sql-server-python.md)
