---
title: "Sicherheit für SQL Server-Machine Learning und R | Microsoft Docs"
ms.custom: 
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dba0ea904e9b22cb99e4e0deb9befc32dd9e1abe
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="security-for-sql-server-machine-learning-and-r"></a>Sicherheit für SQL Server-Machine Learning und R

Dieser Artikel beschreibt die Sicherheit der Gesamtarchitektur, die verwendet wird, die Verbindung der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Datenbank-Engine und zugehöriger Komponenten, die R-Laufzeit. Beispiele für die Sicherheitsprozesse werden für die folgenden allgemeinen Szenarien für die Verwendung von R in einer unternehmensumgebung bereitgestellt:

+ Ausführen von RevoScaleR-Funktionen in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] aus einem Data Science-Client
+ Ausführen von R direkt aus [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mithilfe von gespeicherten Prozeduren

## <a name="security-overview"></a>Sicherheit (Übersicht)

Ein [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Anmeldename oder Windows-Benutzerkonto ist erforderlich, um R-Skripts ausführen, die SQL Server-Daten verwenden oder, die mit SQL Server als computekontext auszuführen. Diese Anforderung gilt für beide [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] und SQL Server-2017 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)].

Gibt das Konto Anmeldenamen oder Benutzer an der *Sicherheitsprinzipal*, benötigen möglicherweise mehrere Ebenen des Zugriffs, abhängig von den Anforderungen der R-Skript:

+ Über die Berechtigung zum Zugriff auf die Datenbank, in denen R aktiviert ist
+ Berechtigungen zum Lesen von Daten aus gesicherte Objekte wie Tabellen
+ Die Fähigkeit zum Schreiben neuer Daten in eine Tabelle, z. B. ein Modell oder die Bewertung der Ergebnisse
+ Die Fähigkeit zum Erstellen neuer Objekte, z. B. Tabellen, gespeicherte Prozeduren, die R-Skript verwenden oder benutzerdefinierte Funktionen, verwenden Sie R-Auftrag
+ Das Recht, installieren neue Pakete auf dem SQL Server-Computer, oder verwenden Sie R-Pakete, die zu einer Gruppe von Benutzern bereitgestellt. 

Aus diesem Grund jede Person, die mithilfe von R-Code ausführt [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Kontext muss wie die Ausführung einer Anmeldung in der Datenbank zugeordnet werden. Unter SQL Server-Sicherheit ist es im Allgemeinen am einfachsten erstellen Sie Rollen, um Berechtigungssätze, verwalten und Zuweisen von Benutzern zu diesen Rollen, statt Berechtigungen einzeln festzulegen. 

Als Beispiel wird davon ausgegangen, dass Sie einige R-Code, der auf Ihrem Laptop ausgeführt wird erstellt und dieser Code ausgeführt werden sollen [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Dies ist möglich, nur dann, wenn diese Bedingungen erfüllt sind:

+ Die Datenbank lässt Remoteverbindungen zu.
+ Eine SQL-Anmeldung mit dem Namen und dem Kennwort, die Sie im R-Code verwendet haben, wurde dem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] auf Instanzebene hinzugefügt. Wenn Sie stattdessen die integrierte Windows-Authentifizierung verwenden, muss der in der Verbindungszeichenfolge angegebene Windows-Benutzer der Instanz als Benutzer hinzugefügt werden.
+ Die SQL-Anmeldung oder die Windows-Benutzer benötigen die Berechtigung zum Ausführen externer Skripts. Diese Berechtigung kann in der Regel nur von einem Datenbankadministrator hinzugefügt werden.
+ Die SQL-Anmeldung oder der Windows-Benutzer muss als Benutzer mit entsprechenden Berechtigungen in jeder Datenbank hinzugefügt werden, in der der R-Auftrag eine dieser Operationen ausführt:
    + Abrufen von Daten
    + Schreiben oder Aktualisieren von Daten 
    + Neue Objekte wie Tabellen oder gespeicherte Prozeduren erstellen

Nachdem die Anmeldung oder die Windows-Benutzerkonto bereitgestellt und die erforderlichen Berechtigungen erteilt wurde, können Sie R-Code ausführen, auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mithilfe einer R-Datenquellenobjekt oder durch Aufrufen einer gespeicherten Prozedur. Wenn R aus gestartet wird [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], die Sicherheit der Datenbank-Engine Ruft den Sicherheitskontext des Benutzers, der den R-Auftrag gestartet oder die gespeicherte Prozedur ausgeführt und verwaltet die Zuordnungen von der Benutzer- oder Anmeldename auf sicherungsfähige Objekte ab. 

Daher müssen alle R-Aufträge, die von einem Remoteclient aus initiiert werden die Anmeldenamen oder Benutzer als Teil der Verbindungszeichenfolge angeben.

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interaktion von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Sicherheits- und Launchpad

Wenn ein R-Skript im Kontext des [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Computers ausgeführt wird, ruft der [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]-Dienst ein verfügbares Workerkonto (ein lokales Benutzerkonto) aus einem Pool von Workerkonten für externe Prozesse ab und verwendet dieses Workerkonto für die verknüpften Aufgaben. 

Wenn Sie beispielsweise unter Ihren Windows-Domänenanmeldeinformationen einen R-Auftrag starten, wird Ihr Konto möglicherweise dem Launchpad-Workerkonto *SQLRUser01* zugeordnet.

Nach der Zuordnung zu einem Workerkonto erstellt [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] ein Benutzertoken, das zum Starten von Prozessen verwendet wird. 

Wenn alle [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Vorgänge abgeschlossen sind, wird das Benutzerworkerkonto als frei markiert und an den Pool zurückgegeben.

Weitere Informationen zu [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], finden Sie unter [Komponenten in SQL Server zur Unterstützung der Integration von R](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md).

### <a name="implied-authentication"></a>Implizite Authentifizierung

**Implizite Authentifizierung** wird der Begriff für den Prozess, unter dem SQL Server der Benutzer erhält, verwendet die Anmeldeinformationen, und führt dann alle externen Skript-Aufgaben im Auftrag von den Benutzern, vorausgesetzt der Benutzer die richtigen Berechtigungen besitzt, in der Datenbank. Implizite Authentifizierung ist besonders wichtig, wenn das R-Skript einen ODBC-Aufruf außerhalb der SQL Server-Datenbank ausführen muss. Der Code kann z. B. eine kürzere Listen von Faktoren aus einem Tabellenblatt oder einer anderen Quelle abgerufen werden.

Für solche Loopback-Aufrufe erfolgreich ausgeführt werden kann muss die Gruppe mit den Konten, SQLRUserGroup, aus "Lokal anmelden zulassen" berechtigt. Standardmäßig erhält dieses Recht für alle neuen lokalen Benutzer jedoch in einigen Organisationen strengere Gruppenrichtlinien erzwungen werden können.

![Implizite Authentifizierung für R](media/implied-auth-rsql.png)

## <a name="security-of-worker-accounts"></a>Sicherheit der Konten

Die Zuordnung eines externen Windows-Benutzer oder die gültige SQL-Anmeldekennwort für ein workerkonto gilt nur für die Lebensdauer der Lebensdauer der SQL-Abfrage, die die R-Skript ausgeführt wird.

Parallele Abfragen von derselben Anmeldung werden demselben Benutzerworkerkonto zugeordnet.

Die Verzeichnisse, die für die Prozesse verwendet werden, werden von [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] mit RLauncher verwaltet, und der Zugriff auf die Verzeichnisse ist eingeschränkt. Das Workerkonto kann nicht auf Dateien in Ordnern über dem eigenen zugreifen, kann aber untergeordnete Elemente des Arbeitsordners der Sitzung, der für die SQL-Abfrage mit dem R-Skript erstellt wurde, lesen, schreiben oder löschen.

Weitere Informationen dazu, wie Sie die Anzahl der Konten, Kontonamen oder Kennwörter ändern, finden Sie unter [Ändern des benutzerkontenpools für SQL Server-Machine Learning](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

## <a name="security-isolation-for-multiple-external-scripts"></a>Die Sicherheitsisolation für mehrere externe Skripts

Der Isolationsmechanismus basiert auf physischen Benutzerkonten. Da Satellitenprozesse für eine bestimmte Sprachlaufzeit gestartet werden, verwendet jede Satellitenaufgabe das von [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] angegebene Workerkonto. Wenn für eine Aufgabe mehrere Satelliten erforderlich sind, wie z.B. bei parallelen Abfragen, wird ein einziges Workerkonto für alle zusammenhängenden Aufgaben verwendet.

Kein Workerkonto kann Dateien finden oder bearbeiten, die von anderen Workerkonten verwendet werden.
 
Wenn Sie Administrator auf dem Computer sind, können Sie die Verzeichnisse anzeigen, die für jeden Prozess erstellt wurden. Jedes Verzeichnis wird durch die Sitzungs-GUID identifiziert.

## <a name="see-also"></a>Siehe auch

[Übersicht über die Architektur für SQL Server-Machine learning](../../advanced-analytics/r/architecture-overview-sql-server-r.md)
