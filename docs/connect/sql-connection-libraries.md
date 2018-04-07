---
title: Datenverbindungsbibliotheken für Microsoft SQL-Datenbanken | Microsoft Docs
description: Bietet Downloadlinks für Module, die Verbindung mit Microsoft SQL Server und Azure SQL-Datenbank aus einer Vielzahl von Programmiersprachen Client zu aktivieren.
author: MightyPen
ms.service: ''
ms.component: connect
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.technology: dbe-data-tier-apps
ms.custom: ''
ms.workload: data-management
ms.topic: article
ms.date: 03/29/2018
ms.author: genemi
ms.openlocfilehash: c6c459949c63dc11308ac5bf042149775950882d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Verbindung von Modulen für Microsoft SQL-Datenbanken

Dieser Artikel bietet Downloadlinks für Verbindung Module oder *Treiber* , die Ihre Clientprogramme können für die Interaktion mit [Microsoft SQL Server](../index.md), und mit seiner und in der Cloud [Azure SQL-Datenbank](http://docs.microsoft.com/azure/sql-database/). Treiber sind verfügbar für eine Vielzahl von Programmiersprachen, auf die folgenden Betriebssysteme ausgeführt wird:

- Linux (Ubuntu)
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP-relationale Konflikt

*Relationale*: Clientprogramme, die in einer objektorientierten Programmierung (OOP) Sprache, oft geschrieben werden verwenden SQL-Treiber die abgefragte Daten in einem Format zurückgeben, die mehr als objektorientierte relational ist. C# mithilfe von ADO.NET ist ein Beispiel. Der OOP-relationalen Format Konflikt erschwert manchmal den OOP-Code zu schreiben und zu verstehen.

*Verwendung von ORM*: andere Treiber oder Frameworks abgefragte Daten zurückgeben, in der OOP-Format, das den Konflikt zu vermeiden. Diese Treiber funktionieren erwartet, dass die Klassen entsprechend die Datenspalten von bestimmten SQL-Tabellen definiert wurden. Der Treiber führt dann die *objektrelationales Mapping* (ORM), um die abgefragte Daten als eine Instanz einer Klasse zurückgeben. Microsofts Entity Framework (EF) für C#- und Ruhezustand für Java, sind zwei Beispiele.

In diesem Artikel Baus separate Abschnitten an diese zwei Arten von Verbindungs-Treiber.

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>Treiber für den relationalen Zugriff


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  http://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is http://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| Sprache | Herunterladen des SQL-Treibers |
| :------- | :---------------------- |
| C# | [ADO.NET](http://www.microsoft.com/net/download/)<br /><br />[.NET Core, für Linux – Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core, für Mac OS](https://www.microsoft.com/net/core#macos)<br />[.NET Core für Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/oledb-driver-for-sql-server-programming.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js-Treiber installationsanweisungen](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | *Betriebssystem:*<br /><br />[Windows-PHP-Treiber](https://www.microsoft.com/download/details.aspx?id=55642)<br />[Linux oder MacOS PHP-Treiber von Github](http://github.com/Microsoft/msphpsql/) |
| Python | [Pyodbc installationsanweisungen](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[Herunterladen von ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby-Treiber installationsanweisungen](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby-Downloadseite](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>Treiber für ORM-Zugriff


Die folgende Tabelle enthält Beispiele für Objekt Relational Mapping (ORM)-Frameworks, die Clientanwendungen für die Verbindung mit Microsoft SQL-Datenbanken verwenden.


| Sprache | Verwendung von ORM-Treiber-download |
| :------- | :------------------ |
| C# | [Entity Framework Core](http://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x oder höher)](http://docs.microsoft.com/ef/) |
| Java | [Ruhezustand ORM](http://hibernate.org/orm)|
| PHP | [Selbsterklärende ORM in Laravel Installation eingeschlossen wurden](http://laravel.com/docs/) |
| Node.js | [Verwendung von ORM sequelize](http://docs.sequelizejs.com) |
| Python | [Django](http://www.djangoproject.com/) |
| Ruby | [Ruby Schienen](http://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Erstellen eines app-Webseiten
[http://aka.ms/sqldev](http://aka.ms/sqldev) gelangen Sie auf einen Satz von *Build eine app* Webseiten. Die Webseiten Aufschluss darüber geben zahlreiche Kombinationen von programming Language, Betriebssystem und Treiber für SQL-Verbindung. Die folgenden Elemente sind, zwischen den Informationen, die von der Build ein app-Webseiten bereitgestellt:

- Ausführliche Informationen zum ganz von vorn, für jede Kombination aus Sprache, Betriebssystem + Treiber beginnen.
    - Anweisungen zum Installieren der neuesten Treiber von SQL-Verbindung.
- Codebeispiele für jede der folgenden Elemente:
    - Objektrelationales Codebeispiele.
    - Verwendung von ORM-Codebeispiele.
    - Columnstore-Index Demonstrationen für eine schnellere Leistung.

#### <a name="first-page-of-build-an-app-webpages"></a>Erste Seite der Build ein app-Webseiten
![Screenshot der ersten Build ein app-Webseiten][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Menü für Java - Ubuntu, der Build ein app-Webseiten
![Erstellen eines app-Webseiten, Menü Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>Verwandte Links
- [Codebeispiele für die Verbindung mit Azure SQL-Datenbank in der Cloud, mit Java und anderen Sprachen](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java).

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
