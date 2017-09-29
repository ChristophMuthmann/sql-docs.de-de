---
title: "Homepage für SQL Client-Programmierung | Microsoft Docs"
description: "Hubseite mit Anmerkungen Links zu Downloads und der Dokumentation für zahlreiche Kombinationen von Sprachen und Betriebssysteme, zum Herstellen einer Verbindung mit SQL Server oder Azure SQL-Datenbank."
author: MightyPen
ms.date: 09/13/2017
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.topic: article
ms.reviewer: meetb
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: 000325a2e2c53e36f7a74a725962b8dd3be98988
ms.contentlocale: de-de
ms.lasthandoff: 09/13/2017

---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Startseite für den Client für Microsoft SQL Server-Programmierung


Willkommen Sie bei unserem Homepage zur Clientprogrammierung für die Interaktion mit Microsoft SQL Server und Azure SQL-Datenbank in der Cloud. Dieser Artikel enthält die folgende Informationen an:

- Nennt und beschreibt die verfügbaren Kombinationen von Sprache und -Treiber.
    - Informationen für die Betriebssysteme der Linux (Ubuntu und andere) und MacOS Windows angegeben werden.
- Enthält Links zu den ausführlichen Dokumentationen für jede Kombination aus.
- Zeigt an, der Bereiche und Unterbereiche der hierarchischen Dokumentation für bestimmte Sprachen, falls zutreffend.


#### <a name="azure-sql-database"></a>Azure SQL-Datenbank

In einer beliebigen angegebenen Sprache wird der Code, der mit SQL Server verbunden ist fast identisch mit der Code für die Verbindung mit Azure SQL-Datenbank.

Weitere Informationen zu Verbindungszeichenfolgen für die Verbindung zum Herstellen einer Verbindung mit Azure SQL-Datenbank finden Sie unter:

- [Verwenden von .NET Core (c#) zum Abfragen einer Azure SQL-Datenbank](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core).
- Andere Azure SQL-Datenbank, die in der Nähe der vorherigen Artikel in der Tabelle des Inhalts zu anderen Sprachen sind. Beispielsweise finden Sie unter [verwenden PHP zum Abfragen einer Azure SQL-Datenbank](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php).


#### <a name="build-an-app-webpages"></a>Erstellen eines app-Webseiten

Unsere *Build eine app* Webseiten Codebeispiele, zusammen mit den Konfigurationsinformationen in einem anderen Format vorhanden. Weitere Informationen finden Sie weiter unten in diesem Artikel die [Abschnitt mit der Bezeichnung *Build ein app-Website*](#an-204-aka-ms-sqldev).



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>Sprachen und-Treiber für Clientprogramme


In der folgenden Tabelle wird jede Sprache Bild einen Link zu den Details zu SQL Server mit der Sprache. Jeder Link führt zu einem späteren Abschnitt in diesem Artikel.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp;[! [C#-Logo] [Abbildung-Ref-320-Csharp]](#an-110-ado-net-docu) | &nbsp;[! [ORM-Entity Framework von .NET Framework] [Abbildung-Ref-333-Ef]](#an-116-csharp-ef-orm) | &nbsp;[! [Java-Logo] [Abbildung-Ref-330-Java]](#an-130-jdbc-docu) |
| &nbsp;[! [Node.js-Logo] [Abbildung-Ref-340-Node]](#an-140-node-js-docu) | &nbsp; [**`ODBC for C++`**](#an-160-odbc-cpp-docu) | &nbsp;[! [PHP-Logo] [Abbildung-Ref-360-Php]](#an-170-php-docu) |
| &nbsp;[! [Python-Logo] [Abbildung-Ref-370-Python]](#an-180-python-docu) | &nbsp;[! [Ruby Logo] [Abbildung-Ref-380-Ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>Herunterlädt und installiert

Im folgende Artikel dient zum Download und installieren die verschiedenen SQL-Verbindung-Treiber, für die Verwendung in Programmiersprachen zu vergleichen:

- [SQL Server-Treiber](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C#-logo][image-ref-320-csharp] C# mithilfe von ADO.NET

Die .NET-verwaltete-Sprachen wie c# und Visual Basic sind die häufigsten Benutzer von ADO.NET. *ADO.NET* gelegentlichen Name ist für eine Teilmenge von .NET Framework-Klassen.

#### <a name="code-examples"></a>Codebeispiele

|||
| :-- | :-- |
| [Herstellen einer Verbindung mit SQL mithilfe von ADO.NET Machbarkeitsstudie](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | Ein kleines Codebeispiel konzentriert sich auf eine Verbindung herstellen und Abfragen von SQL Server. |
| [Herstellen Sie belastbarer SQL mit ADO.NET](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | Wiederholen Sie die Logik in ein Codebeispiel, da Verbindungen zeitmomente Konnektivitätsverlust gelegentlich auftreten können.<br /><br />Wiederholungslogik gilt auch für Verbindungen über das Internet wie Azure SQL-Datenbank in eine beliebige Clouddatenbank verwaltet. |
| [Azure SQL-Datenbank: Zeigt, wie mit .NET Core auf Linux/Windows/MacOS erstellt ein C#-Programm, eine Verbindung herstellen und Abfragen](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Beispiel für Azure SQL-Datenbank. |
| [Erstellen einer app: C#, ADO.NET, Windows](http://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | Informationen zu Konfigurationen sowie Codebeispiele. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Dokumentation

|||
| :-- | :-- |
| [C# mithilfe von ADO.NET](./ado-net/index.md)| Der Stamm der unserer Dokumentation erfahren. |
| [Namespace: "System.Data"](http://docs.microsoft.com/dotnet/api/system.data) | Ein Satz von Klassen, die für ADO.NET. |
| [Namespace: System.Data.SqlClient](http://docs.microsoft.com/dotnet/api/system.data.SqlClient) | Der Satz von Klassen, die meisten direkt Center ADO.NET. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework-logo][image-ref-333-ef] Entity Framework (EF) mit C&#x23;

Entity Framework (EF) bietet objektrelationales Mapping (ORM). ORM erleichtert es den Quellcode objektorientiertes Programmierung (OOP) zum Bearbeiten von Daten, die aus einer relationalen SQL­Datenbank abgerufen wurden.

EF hat direkte oder indirekte Beziehungen mit den folgenden Technologien:

- .NET Framework
- [LINQ to SQL](http://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/), oder [LINQ to Entities](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- Syntax-spracherweiterungen, wie z. B. die ** => ** Operator in C# geschrieben.
- Praktisch Programme, die Quellcode für Klassen zu generieren, die die Tabellen in der SQL-Datenbank zuordnen. Z. B. [EdmGen.exe](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>Ursprüngliche EF und neue EF

Die [Startseite für Entity Framework](http://docs.microsoft.com/ef/) führt EF mit einer Beschreibung der folgenden ähnelt:

- Entity Framework ist eine objektrelationale Mapper (O/RM), die .NET Entwicklern mit einer Datenbank mithilfe von .NET Objekten arbeiten. Er wird für die meisten der Datenzugriffs-Quellcode, den in der Regel Entwickler schreiben müssen überflüssig.

*Entity Framework* ist ein Name, der von zwei separaten Quellcodefenster codeverzweigungen gemeinsam verwendet werden. Eine EF-Verzweigung ist älter, und der Quellcode jetzt von den öffentlichen verwaltet werden kann. Andere EF ist neu. Die zwei EFs werden nachfolgend beschrieben:

|     |     |
| :-- | :-- |
| [EF 6.x](http://docs.microsoft.com/ef/ef6/) | Microsoft hat EF zuerst im August 2008 veröffentlicht. Im März 2015 kündigte Microsoft, die EF 6.x wurde der endgültigen Version, die Microsoft entwickeln möchten. Microsoft hat den Quellcode in der öffentlichen Domäne veröffentlicht.<br /><br />Anfangs war EF Teil von .NET Framework. Aber EF 6.x aus .NET Framework entfernt wurde.<br /><br />[EF 6.x-Quellcode für Github erstellt im Repository *Aspnet/EntityFramework6*](http://github.com/aspnet/EntityFramework6) |
| [EF Core](http://docs.microsoft.com/ef/core/) | Microsoft hat die neu entwickelten EF Core im Juni 2016 veröffentlicht. EF Core dient für eine größere Flexibilität und Portabilität. EF Core kann auf hinter nur Microsoft-Windows-Betriebssystemen ausführen. Und EF-Core mit hinter nur Microsoft SQL Server-Datenbanken und andere relationalen Datenbanken interagieren kann.<br /><br />**C&#x23; Codebeispiele:**<br />[Erste Schritte mit Entity Framework Core](https://docs.microsoft.com/ef/core/get-started/index)<br />[Erste Schritte mit EF Core unter .NET Framework mit einer vorhandenen Datenbank](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF und verwandten Technologien sind leistungsstarke, und viele für den Entwickler erfahren Sie, den gesamten Bereich "master" möchte.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java-logo][image-ref-330-java] Java- und JDBC

Microsoft bietet einen Java Database Connectivity (JDBC)-Treiber für die Verwendung mit SQL Server (oder mit Azure SQL-Datenbank, natürlich). Es ist ein Typ-4-JDBC-Treiber, und es stellt Datenbankverbindungen über die standardmäßigen JDBC-Anwendungsprogrammierschnittstellen (APIs).

#### <a name="code-examples"></a>Codebeispiele

|||
| :-- | :-- |
| [Codebeispiele](./jdbc/code-samples/index.md) | Codebeispiele, die Informationen zu Datentypen, Resultsets und große Datenmengen werden folgende Themen behandelt. |
| [Verbindungs-URL – Beispiel](./jdbc/connection-url-sample.md) | Beschreibt, wie eine Verbindungs-URL für die Verbindung mit SQL Server verwenden. Verwenden Sie dieses dann zum SQL-Anweisung verwenden, um Daten abzurufen. |
| [Beispiel für Datenquellen](./jdbc/data-source-sample.md) | Beschreibt, wie eine Datenquelle zu verwenden, um die Verbindung mit SQL Server. Klicken Sie dann verwenden Sie eine gespeicherte Prozedur, um Daten abzurufen. |
| [Verwenden von Java zum Abfragen einer Azure SQL-Datenbank](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Beispiel für Azure SQL-Datenbank. |
| [Erstellen von Java-apps, die mit SQL Server auf Ubuntu](http://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | Informationen zu Konfigurationen sowie Codebeispiele. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Dokumentation

Die JDBC-Dokumentation enthält die folgenden Hauptbereichen:

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | Stamm der JDBC-Dokumentation. |
| [Referenz](./jdbc/reference/index.md) | Schnittstellen, Klassen und Member. |
| [Programmierhandbuch für JDBC-Treiber](./jdbc/programming-guide-for-jdbc-sql-driver.md) | Informationen zu Konfigurationen sowie Codebeispiele. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js-logo][image-ref-340-node] Node.js

Mit Node.js können Sie SQL Server von Windows, Linux oder Mac herstellen Der Stamm der Node.js-Dokumentation ist [hier](./node-js/index.md).

Der Node.js-Verbindungs-Treiber für SQL Server wird in JavaScript implementiert. Der Treiber verwendet die TDS-Protokolls, das von allen modernen SQL Server-Versionen unterstützt wird. Der Treiber ist ein open Source-Projekt [auf Github verfügbar](http://tediousjs.github.io/tedious/).

#### <a name="code-examples"></a>Codebeispiele

|||
| :-- | :-- |
| [Herstellen einer Verbindung mit SQL mit Node.js Machbarkeitsstudie](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | Texten Quellcode für das Herstellen einer Verbindung mit SQL Server und eine Abfrage ausführt. |
| [Azure SQL-Datenbank: Verwenden von Node.js abzufragende](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | Beispiel für Azure SQL-Datenbank in der Cloud. |
| [Erstellen Sie Node.js-apps zur Verwendung von SQL Server auf macOS](http://www.microsoft.com/sql-server/developer-get-started/node/mac/) | Informationen zu Konfigurationen sowie Codebeispiele. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBC für C++ 

![ODBC-logo][image-ref-350-odbc]

Open Database Connectivity (ODBC) in den 1990ern entwickelt wurde, und es ist ein Vorläufer des .NET Framework. ODBC wurde entwickelt, unabhängig von allen Systemen bestimmte Datenbank und des Betriebssystems unabhängig ist.

Im Laufe der Jahre wurden zahlreichen ODBC-Treiber erstellt und von Gruppen innerhalb und außerhalb von Microsoft veröffentlicht. Der Bereich der Treiber umfassen mehrere Client-Programmiersprachen. Die Liste der Datenziele hinausgeht auch SQL Server.

Einige andere verbindungstreiber mithilfe von ODBC intern.

#### <a name="code-example"></a>Codebeispiel

- [C++-Codebeispiel zur Verwendung von ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>Gliederung

Der ODBC-Inhalt in diesem Abschnitt konzentriert sich auf den Zugriff auf SQL Server oder Azure SQL-Datenbank von C++. Die folgende Tabelle enthält einen ungefähre Überblick über die wichtigsten Dokumentation für ODBC.


| Bereich | Unterbereich | Description |
| :--- | :------ | :---------- |
| [ODBC für C++](./odbc/index.md) | Der Stamm der unserer Dokumentation erfahren. |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | Informationen zum Verwenden von ODBC unter den Betriebssystemen Linux oder MacOS. |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Informationen zur Verwendung von ODBC in Windows-Betriebssystems. |
| [Verwaltung](../odbc/admin/index.md) | &nbsp; | Das Verwaltungstool für die Verwaltung von ODBC-Datenquellen. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Verschiedene ODBC-Treiber, die erstellt und von Microsoft bereitgestellt werden. |
| [Konzept- und](../odbc/reference/index.md) | &nbsp; | Grundlegende Informationen über die ODBC-Schnittstelle, zusätzlich zu herkömmlichen Verweis. |
| &nbsp; " | [Anhängen](../odbc/reference/appendixes/index.md)    | Zustandsübergang Tabellen, ODBC-Cursorbibliothek und mehr. |
| &nbsp; " | [Entwickeln der app](../odbc/reference/develop-app/index.md)  | Funktionen, Handles und vieles mehr. |
| &nbsp; " | [Entwickeln Sie Treiber](../odbc/reference/develop-driver/index.md) | Wie Sie eigene ODBC-Treiber zu entwickeln, wenn Sie eine spezielle Datenquelle verfügen. |
| &nbsp; " | [Installieren](../odbc/reference/install/index.md) | ODBC-Installation, Unterschlüssel und mehr. |
| &nbsp; " | [Syntax](../odbc/reference/syntax/index.md)   | APIs für Setup, Installer, Übersetzung und Daten zugreifen. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP-logo][image-ref-360-php] PHP

Sie können die PHP verwenden, für die Interaktion mit SQL Server. Der Stamm der Node.js-Dokumentation ist [hier](./php/index.md).

#### <a name="code-examples"></a>Codebeispiele

|||
| :-- | :-- |
| [Herstellen einer Verbindung mit SQL mithilfe von PHP Machbarkeitsstudie](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | Ein kleines Codebeispiel konzentriert sich auf eine Verbindung herstellen und Abfragen von SQL Server. |
| [Herstellen Sie belastbarer SQL mit PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | Wiederholen Sie die Logik in ein Codebeispiel, da Verbindungen über das Internet und der Cloud zeitmomente Konnektivitätsverlust gelegentlich auftreten können. |
| [Azure SQL-Datenbank: Verwenden Sie PHP abzufragende](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Beispiel für Azure SQL-Datenbank. |
| [Erstellen Sie PHP-apps zur Verwendung von SQL Server auf dem RHEL](http://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | Informationen zu Konfigurationen sowie Codebeispiele. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python-logo][image-ref-370-python] Python


Für die Interaktion mit SQL Server können Sie Python verwenden.

#### <a name="code-examples"></a>Codebeispiele

|||
| :-- | :-- |
| [Herstellen einer Verbindung mit SQL mit Python mithilfe Pyodbc Machbarkeitsstudie](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | Ein kleines Codebeispiel konzentriert sich auf eine Verbindung herstellen und Abfragen von SQL Server. |
| [Azure SQL-Datenbank: Verwenden von Python abzufragende](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Beispiel für Azure SQL-Datenbank. |
| [Erstellen von PHP-apps zur Verwendung von SQL Server auf SLES](http://www.microsoft.com/sql-server/developer-get-started/python/sles/) | Informationen zu Konfigurationen sowie Codebeispiele. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>Dokumentation

| Bereich | Description |
| :--- | :---------- |
| [Python mit SQLServer](./python/index.md) | Der Stamm der unserer Dokumentation erfahren. |
| [Pymssql-Treiber](./python/pymssql/index.md) | Microsoft nicht beibehält oder testen den Pymssql-Treiber.<br /><br />Der Pymssql-Verbindungs-Treiber ist eine einfache Schnittstelle für die SQL-Datenbanken, für die Verwendung in Python-Programme. Pymssql beruht auf FreeTDS, eine Python-DB-API (PEP 249)-Schnittstelle für Microsoft SQL Server bereitzustellen. |
| [Pyodbc-Treiber](./python/pyodbc/index.md)   | Der Pyodbc-Verbindungs-Treiber ist ein open-Source-Python-Modul, das Zugriff auf ODBC-Datenbanken auf einfache Weise. Die DB-API 2.0-Spezifikation implementiert, aber mit noch mehr Pythonic halber gepackt ist. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby-logo][image-ref-380-ruby] Ruby

Sie können die Ruby verwenden, für die Interaktion mit SQL Server. Der Stamm der Ruby-Dokumentation ist [hier](./ruby/index.md).

#### <a name="code-examples"></a>Codebeispiele

|||
| :-- | :-- |
| [Herstellen einer Verbindung mit SQL mit Ruby Machbarkeitsstudie](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | Ein kleines Codebeispiel konzentriert sich auf eine Verbindung herstellen und Abfragen von SQL Server. |
| [Azure SQL-Datenbank: Verwenden von Ruby abzufragende](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Beispiel für Azure SQL-Datenbank. |
| [Erstellen von Ruby-apps zur Verwendung von SQL Server auf MacOS](http://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | Informationen zu Konfigurationen sowie Codebeispiele. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpwwwmicrosoftcomsql-serverdeveloper-get-started"></a>[Erstellen eines app-Website für SQL Client-Entwicklung](http://www.microsoft.com/sql-server/developer-get-started/)


Auf unserer [ *Build eine app* ](https://www.microsoft.com/sql-server/developer-get-started/) Webseiten, die Sie aus einer langen Liste von Programmiersprachen für die Verbindung mit SQL Server auswählen können. Und Ihr Clientprogramm kann eine Vielzahl von Betriebssystemen ausgeführt.

*Erstellen einer app* Einfachheit und Vollständigkeit für Entwickler noch die ersten Schritte wird hervorgehoben. Die Schritte erläutern die folgenden Aufgaben:

1. Gewusst wie: Installieren von Microsoft SQL Server
2. Zum Herunterladen und Installieren von Tools und Treiber.
3. Stellen Sie alle erforderlichen Konfigurationen für Ihr Betriebssystem geeignete Vorgehensweise.
4. Wie Sie die bereitgestellten Quellcode zu kompilieren.
5. Wie das Programm ausgeführt werden.

Darauf folgen einige ungefähre Umrisse von Details auf der Website bereitgestellt:

#### <a name="java-on-ubuntu"></a>Java auf Ubuntu:

1. Einrichten der Umgebung
    - Schritt 1.1 Installieren von SQLServer
    - Schritt 1.2 Installation Java
    - Schritt 1.3 Installieren des Java Development Kit (JDK)
    - Schritt 1.4 installieren Maven
2. Erstellen von Java-Anwendung mit SQL Server
    - Schritt 2.1: Erstellen einer Java-app, die eine Verbindung mit SQL Server her und führt Abfragen
    - Schritt 2.2: Erstellen einer Java-app, die Verbindung mit SQL Server mithilfe des beliebten Frameworks Ruhezustand
3. Machen Sie die Java-app bis zu 100 X schneller
    - Schritt 3.1 Erstellen einer Java-app, um zu veranschaulichen, columnstore-Indizes

#### <a name="python-on-windows"></a>Python unter Windows:

1. Einrichten der Umgebung
    - Schritt 1.1 Installieren von SQLServer
    - Schritt 1.2 Installation Python
    - Schritt 1.3 Installieren des ODBC-Treibers und SQL-Befehlszeilen-Hilfsprogramm für SQLServer
2. Erstellen von Python-Anwendung mit SQL Server
    - Schritt 2.1 installieren Sie den Python-Treiber für SQL Server
    - Schritt 2.2: Erstellen einer Datenbank für Ihre Anwendung
    - Schritt 2.3 Erstellen Sie eine Python-app, die eine Verbindung mit SQL Server her und führt Abfragen
3. Machen Sie die Python-app bis zu 100 X schneller
    - Schritt 3.1 erstellen Sie eine neue Tabelle mit 5 Millionen mithilfe von sqlcmd
    - Schritt 3.2 Erstellen Sie eine Python-app, die diese Tabelle Abfragen und misst die Zeit
    - Schritt 3.3 zu messen, wie lange es dauert, um die Abfrage auszuführen
    - Schritt 3.4 hinzufügen einen columnstore-Index zur Tabelle
    - Schritt 3.5 zu messen, wie lange es dauert, zum Ausführen der Abfrage mit einem columnstore-index

Die folgenden Screenshots vermitteln Ihnen einen Eindruck von unsere SQL Development-Dokumentationswebsite aussieht.

#### <a name="choose-a-language"></a>Wählen Sie eine Sprache aus:

![SQL-Dev-Website, erste Schritte][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>Wählen Sie ein Betriebssystem aus:

![SQL-Dev-Website Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>Andere Entwicklung


Dieser Abschnitt enthält Links zu anderen Entwicklungsoptionen. Dazu gehören, verwenden diese gleichen Sprachen für Azure-Entwicklung im Allgemeinen. Die Informationen hinausgeht zielt auf nur Azure SQL-Datenbank und Microsoft SQL Server.

#### <a name="developer-hub-for-azure"></a>Developer-Hub für Azure

- [Developer-Hub für Azure](http://docs.microsoft.com/azure/)
- [Azure für .NET-Entwickler](http://docs.microsoft.com/dotnet/azure/)
- [Azure für Java-Entwickler](http://docs.microsoft.com/java/azure/)
- [Azure für Node.js-Entwickler](http://docs.microsoft.com/nodejs/azure/)
- [Azure für Python-Entwickler](http://docs.microsoft.com/python/azure/)
- [Erstellen einer PHP-Web-app in Azure](http://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>Andere Sprachen

- [Erstellen von Go-apps mithilfe von SQL Server unter Windows](http://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-310-ado-net]: ./media/homepage-sql-connection-drivers/gm-ado-net-an51.png
[image-ref-322-cpp]: ./media/homepage-sql-connection-drivers/gm-cpp-4point-p61f.png
[image-ref-320-csharp]: ./media/homepage-sql-connection-drivers/gm-csharp-c10c.png
[image-ref-333-ef]: ./media/homepage-sql-connection-drivers/gm-entity-framework-ef20d.png
[image-ref-330-java]: ./media/homepage-sql-connection-drivers/gm-java-j18c.png
[image-ref-340-node]: ./media/homepage-sql-connection-drivers/gm-node-n30.png
[image-ref-350-odbc]: ./media/homepage-sql-connection-drivers/gm-odbc-ic55826-o35.png
[image-ref-360-php]: ./media/homepage-sql-connection-drivers/gm-php-php60.png
[image-ref-370-python]: ./media/homepage-sql-connection-drivers/gm-python-py72.png
[image-ref-380-ruby]: ./media/homepage-sql-connection-drivers/gm-ruby-un-r82.png
[image-ref-390-aka-ms-sqldev-choose-language]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-400-aka-ms-sqldev-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png


