---
title: Paket-Standardbibliotheken für Machine Learning auf SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 64b085c2314e4c97694e91924cb15d43315143e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="default-package-libraries-for-machine-learning-on-sql-server"></a>Paket-Standardbibliotheken, für den Machine learning auf SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel beschreibt die Standardbibliotheken für R und Python, die mit SQL Server installiert sind. Dieser Artikel bietet die Standardspeicherorte für diese Bibliotheken, und erläutert, wie Sie die Pakete und welche Version von R ermitteln oder Python in jeder Bibliothek Instanz installiert sind.

## <a name="using-the-default-instance-library"></a>Mithilfe der Standard-Instanz-Bibliothek

Bei der Installation von Machine Learning mit SQL Server wird eine einzelnes Paket-Bibliothek auf Instanzebene für jede Sprache erstellt, die Sie installieren. SQL Server kann nicht mit anderen Bibliotheken installierte Pakete zugreifen.

Wenn Sie von einem Remoteclient aus eine Verbindung mit dem Server herstellen, können alle R oder Python-Code, der in der Server-computekontext ausgeführt werden soll nur Pakete, die in der Bibliothek für die Instanz installiert.

Um Serverressourcen zu schützen, wird die Standardbibliothek Instanz einem gesicherten Ordner installiert, die mit SQL Server registriert ist, und kann nur von einem Computeradministrator geändert werden. Wenn Sie nicht der Besitzer des Computers sind, müssen Sie möglicherweise Berechtigung durch einen Administrator für das Installieren der Pakete in dieser Bibliothek zu erhalten. 

Auch wenn Sie den Computer besitzen, sollten Sie die Nützlichkeit der jedes bestimmten R oder Python-Paket in einer serverumgebung, vor dem Hinzufügen des Pakets auf die Instanz-Bibliothek. Betrachten Sie Faktoren wie z. B. die Größe der Paketdateien und Anforderungen für mehrere Versionen sowie, ob das Paket Netzwerk oder über das Internet erfordert Zugriff.

### <a name="sql-server"></a>SQL Server

|Version | Instanzname|Standardpfad|
|------|------|------|
| SQL Server 2016 |Standardinstanz|`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`|
| SQL Server 2016 |Benannte Instanz |`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES\library`|
| SQLServer 2017 mit R|Standardinstanz |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` |
| SQLServer 2017 mit R|Benannte Instanz|`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` |
| SQLServer 2017 mit Python |Standardinstanz |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library` |
| SQLServer 2017 mit Python|Benannte Instanz|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES\library` |

### <a name="r-server-standalone-or-machine-learning-server-standalone"></a>R Server (eigenständig) oder Machine Learning-Server (eigenständig)

Diese Tabelle enthält die Standardpfade der Binärdateien aus, bei der Installation des eigenständigen Servers mit SQL Server-Setup. 

|Version| Installation|Standardpfad|
|------|------|------|
| SQL Server 2016|R-Server (eigenständig)| |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|Machine Learning-Server mit R |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|Machine Learning-Server mit Python |`C:\Program Files\Microsoft SQL Server\130\PYTHON_SERVER`|

Bei der Installation von Microsoft R Server oder separaten Windows Installer verwenden Machine Learning-Server die Standardpfaden unterscheiden: in der Regel, ungefähr wie `C:\Program Files\Microsoft\R Server\R_SERVER`. Weitere Informationen finden Sie in den folgenden Themen:
 
+ [Installieren Sie Machine Learning-Server für Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Installieren von R Server 9.1 für Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="what-is-included-in-a-default-installation"></a>Was ist in einer Standardinstallation enthalten.

Dieser Abschnitt enthält eine Zusammenfassung der R oder Python-Funktionen, die standardmäßig installiert sind.

### <a name="default-r-installation-for-sql-server"></a>Standardmäßige R-Installation für SQL Server

Standardmäßig R **Basis** Pakete installiert sind. Basis-Pakete enthalten Kernfunktionalität von Paketen bereitgestellt, z. B. `stats` und `utils`.

Eine Basisinstallation von R hinaus zahlreiche beispieldatasets und R-Standardtools wie "rgui.exe" (eine einfache interaktive-Editor) und RTerm (ein R-Eingabeaufforderung).

Installation von R in SQL Server 2016 oder SQL Server-2017 enthält auch die **"revoscaler"** Pakets sowie verwandte verbesserten Pakete und Anbieter, die unterstützt remote rechenkontexte, streaming, parallele Ausführung Rx-Funktion und viele weitere Funktionen.

Um die RevoScaleR-Paket zu aktualisieren, verwenden Sie entweder Bindung nur Machine learning-Komponenten, aktualisieren oder gepatcht oder aktualisieren Sie die Instanz auf eine neuere Version von SQL Server.

+ Einen Überblick über die erweiterten R-Funktionen finden Sie unter [zu Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ Informationen zum Herunterladen der Bibliotheken "revoscaler" auf einem Clientcomputer installieren [Microsoft R-Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

### <a name="default-python-installation-for-sql-server"></a>Python-Installation für SQL Server Standard

Wenn Sie die Machine learning-Funktionen und die Python-Language-Option auswählen, wird eine Anaconda-Verteilung installiert. Die genaue Version hängt davon ab, die Version von SQL Server, die Sie installiert haben und gibt an, ob Sie die Instanz unter Verwendung von Machine Learning-Server-Installation aktualisiert haben.

|Release| Anaconda-version| Andere Änderungen|
|------|------|------|
| RTM-Version von SQL Server 2017| 3.5.2| Neu: Revoscalepy|
| Aktualisierung über Machine Learning-Server 9.2.1 September 2017| Anaconda 4.2| Updates für revoscalepy |
| SQL Server 2017 CU3| Anaconda 4.2| Updates für revoscalepy |

Zusätzlich zu den Python-Code-Bibliotheken enthält die Standardinstallation Beispieldaten, Komponententests und Beispielskripts.

## <a name="restrictions-and-known-issues"></a>Einschränkungen und bekannte Probleme

Können Sie jede Lösung, die in SQL Server ausgeführt wird **nur** Pakete, die in der Standardbibliothek der Instanz zugeordneten installiert sind.

Wenn Sie die Bindung verwenden, die R-Komponenten in einer Instanz aktualisiert, können den Pfad zur Bibliothek Instanz ändern. Achten Sie darauf, dass Sie den Pfad der aktuell von SQL Server verwendeten Bibliothek zu überprüfen.

## <a name="administrative-permissions-required-for-package-installation"></a>Administratorberechtigungen für die Paketinstallation erforderlich

Die erforderlichen Berechtigungen für die Paketinstallation wurden zwischen SQL Server 2016 und SQL Server-2017 geändert.

+ In SQL Server 2016 ist Administratorzugriff erforderlich ist, für die Installation der neuen R-Pakete.

+ In SQL Server-2017 können Sie weiterhin Pakete als Administrator für R und Python zu installieren, und dies ist wahrscheinlich die einfachste Methode.

    Die DDL-Anweisung, externe Bibliothek erstellen kann den Datenbankadministrator, um Pakete zu installieren, ohne Verwendung von R-Tools. 

    Wenn Sie die Paket-Verwaltungsfunktion für Machine Learning-Server verwenden, können Sie "revoscaler" verwenden, Installieren von R-Pakete auf Datenbankebene. Der Datenbankadministrator muss das Feature aktivieren, und gewähren Sie Benutzern die Möglichkeit, ihre eigenen Pakete auf jede Datenbank separat zu installieren. Weitere Informationen finden Sie unter [aktivieren paketverwaltung mit DDLs](r-package-how-to-enable-or-disable.md).

### <a name="user-libraries-are-not-supported"></a>Benutzerbibliotheken werden nicht unterstützt.

Benutzer, die ein Paket nicht häufig an einem sicheren Speicherort installieren können, installieren ein Paket in einer Benutzerbibliothek verwenden. Allerdings ist dies nicht möglich, in der SQL Server-Umgebung. Sogar Dateisystemzugriff wird oft auf dem Server beschränkt.

Auch wenn Sie in einen Benutzer Dokumentordner auf dem Server Administratorrechte sowie über Zugriff verfügt, kann nicht externes Skript-Laufzeit, die in SQL Server ausgeführt wird Pakete außerhalb der Standardbibliothek für die Instanz installiert zugreifen.

Tipps zum Beheben von Problemen im Zusammenhang mit benutzerbibliotheken, finden Sie unter [Paket installiert wird, in benutzerbibliotheken](packages-installed-in-user-libraries.md).