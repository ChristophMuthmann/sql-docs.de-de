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
ms.openlocfilehash: 8388d7c9d22a49a49a1a45a6fa6b479107f9ccae
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview-sql-server-r-services"></a>Sicherheitsübersicht (SQL Server R Services)

In diesem Thema wird die Sicherheitsarchitektur beschrieben, die verwendet wird, um das [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Datenbankmodul und zugehörige Komponenten mit der R-Laufzeit zu verbinden. Beispiele für den Sicherheitsprozess werden für zwei häufige Szenarios gegeben, in denen R in einer Unternehmensumgebung verwendet wird:

+ Ausführen von RevoScaleR-Funktionen in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] aus einem Data Science-Client
+ Ausführen von R direkt aus [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mithilfe von gespeicherten Prozeduren

## <a name="security-overview"></a>Sicherheitsübersicht

Ein [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -Anmeldename oder Windows-Benutzerkonto ist erforderlich, um R-Skripts ausführen, die SQL Server-Daten verwenden oder, die mit SQL Server als computekontext auszuführen. Diese Anforderung gilt für beide [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] und SQL Server 2017 Machine Learning Services. 

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

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interaktion von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Sicherheit und LaunchPad-Sicherheit

Wenn ein R-Skript im Kontext des [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Computers ausgeführt wird, ruft der [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]-Dienst ein verfügbares Workerkonto (ein lokales Benutzerkonto) aus einem Pool von Workerkonten für externe Prozesse ab und verwendet dieses Workerkonto für die verknüpften Aufgaben. 

Wenn Sie beispielsweise unter Ihren Windows-Domänenanmeldeinformationen einen R-Auftrag starten, wird Ihr Konto möglicherweise dem Launchpad-Workerkonto *SQLRUser01* zugeordnet.

Nach der Zuordnung zu einem Workerkonto erstellt [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] ein Benutzertoken, das zum Starten von Prozessen verwendet wird. 

Wenn alle [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Vorgänge abgeschlossen sind, wird das Benutzerworkerkonto als frei markiert und an den Pool zurückgegeben.

Weitere Informationen zu [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] finden Sie unter [New Components in SQL Server to Support R Integration (Neue Komponenten in SQL Server zur Unterstützung der R-Integration)](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md).

> [!NOTE]
Damit Launchpad die Workerkonten verwalten und R-Aufträge ausführen kann, muss die Gruppe „SQLRUserGroup“, die die Workerkonten enthält, über die Berechtigung „Lokale Anmeldung zulassen“ verfügen, andernfalls funktionieren R-Dienste möglicherweise nicht. In der Standardeinstellung wird dieses Recht allen neuen lokalen Benutzern erteilt, aber in einigen Organisationen werden möglicherweise strengere Gruppenrichtlinien erzwungen, die verhindern, dass die Workerkonten eine Verbindung zu SQL Server herstellen, um R-Aufträge auszuführen.  

## <a name="security-of-worker-accounts"></a>Sicherheit von Workerkonten

Die Zuordnung eines externen Windows-Benutzer oder die gültige SQL-Anmeldekennwort für ein workerkonto gilt nur für die Lebensdauer der Lebensdauer der SQL-Abfrage, die die R-Skript ausgeführt wird. 

Parallele Abfragen von derselben Anmeldung werden demselben Benutzerworkerkonto zugeordnet.

Die Verzeichnisse, die für die Prozesse verwendet werden, werden von [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] mit RLauncher verwaltet, und der Zugriff auf die Verzeichnisse ist eingeschränkt. Das Workerkonto kann nicht auf Dateien in Ordnern über dem eigenen zugreifen, kann aber untergeordnete Elemente des Arbeitsordners der Sitzung, der für die SQL-Abfrage mit dem R-Skript erstellt wurde, lesen, schreiben oder löschen.

Weitere Informationen dazu, wie Sie die Anzahl der Workerkonten, Kontonamen oder Kennwörter ändern können, finden Sie unter [Ändern des Benutzerkontenpools für SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).


## <a name="security-isolation-for-multiple-external-scripts"></a>Sicherheitsisolation für mehrere externe Skripts

Der Isolationsmechanismus basiert auf physischen Benutzerkonten. Da Satellitenprozesse für eine bestimmte Sprachlaufzeit gestartet werden, verwendet jede Satellitenaufgabe das von [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] angegebene Workerkonto. Wenn für eine Aufgabe mehrere Satelliten erforderlich sind, wie z.B. bei parallelen Abfragen, wird ein einziges Workerkonto für alle zusammenhängenden Aufgaben verwendet.

Kein Workerkonto kann Dateien finden oder bearbeiten, die von anderen Workerkonten verwendet werden.
 
Wenn Sie Administrator auf dem Computer sind, können Sie die Verzeichnisse anzeigen, die für jeden Prozess erstellt wurden. Jedes Verzeichnis wird durch die Sitzungs-GUID identifiziert.

## <a name="see-also"></a>Siehe auch
[Übersicht über die Architektur](../../advanced-analytics/r-services/architecture-overview-sql-server-r.md)

