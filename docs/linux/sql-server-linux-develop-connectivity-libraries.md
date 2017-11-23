---
title: Verbindungsbibliotheken und Frameworks | Microsoft Docs
description: "Listet die Client-apps aus verschiedenen Sprachen verwenden können, die Verbindung mit Microsoft SQL Server lokal oder in der Cloud, auf Linux, Windows oder Docker und auch für Azure SQL-Datenbank und Azure SQL Data Warehouse-verbindungstreiber an."
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.workload: Inactive
ms.openlocfilehash: 765fb054ab4fb5332df7b2f9d2e202188f621b67
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Verbindungsbibliotheken und Frameworks für Microsoft SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Sehen Sie sich unsere [Lernprogramme für erste Schritte](http://aka.ms/sqldev) können Sie schnell erste Schritte mit Programmiersprachen wie c#, Java, Node.js, PHP und Python und erstellen Sie eine Anwendung mithilfe von SQL Server auf MacOS auf Linux, Windows oder Docker.

Die folgende Tabelle listet verbindungsbibliotheken oder *Treiber* , dass Clientanwendungen aus einer Vielzahl von Sprachen zum Verbinden mit und Verwenden von Microsoft SQL Server lokal ausgeführt wird oder in der Cloud, auf Linux, Windows oder Docker und auch für Azure SQL-Datenbank und Azure SQL Data Warehouse verwenden können. 

| Sprache | Platform | Weitere Ressourcen | Herunterladen | Erste Schritte |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, Mac OS | [Microsoft ADO.NET für SQL Server](http://msdn.microsoft.com/library/mt657768.aspx) | [Download](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [Erste Schritte](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, Mac OS | [Microsoft JDBC-Treiber für SQL Server](http://msdn.microsoft.com/library/mt484311.aspx) | [Download](http://go.microsoft.com/fwlink/?LinkId=245496) |  [Erste Schritte](https://www.microsoft.com/en-us/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, Mac OS| [PHP-SQL-Treiber für SQLServer](http://msdn.microsoft.com/library/dn865013.aspx) | Betriebssystem: <br/> \*[Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \*[Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \*[MacOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Erste Schritte](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, Mac OS | [Node.js-Treiber für SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [Erste Schritte](https://www.microsoft.com/en-us/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, Mac OS | [Python-SQL-Treiber](../connect/python/python-driver-for-sql-server.md) <br/> \*[Pyodbc](http://msdn.microsoft.com/library/mt763257.aspx) |  [Erste Schritte](https://www.microsoft.com/en-us/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, Mac OS | [Ruby-Treiber für SQL Server](../connect/ruby/ruby-driver-for-sql-server.md) | [Erste Schritte](https://www.microsoft.com/en-us/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, Mac OS | [Microsoft ODBC Driver for SQL Server](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) | [Download](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) |  

In der folgenden Tabelle sind einige Beispiele von Objekt Relational Mapping (ORM)-Frameworks und webframeworks, die Clientanwendungen mit Microsoft SQL Server lokal ausgeführt wird, oder verwenden können, in der Cloud auf Linux, Windows oder Docker und auch für Azure SQL-Datenbank und Azure SQL Data Warehouse aufgeführt. 

| Sprache | Platform | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, Mac OS | [Entity Framework](https://docs.microsoft.com/en-us/ef)<br>[Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/index) |
| Java | Windows, Linux, Mac OS |[Ruhezustand ORM](http://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (selbsterklärende)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, Mac OS | [Verwendung von ORM sequelize](http://docs.sequelizejs.com) |
| Python | Windows, Linux, Mac OS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, Mac OS | [Ruby Schienen](http://rubyonrails.org/) |

## <a name="related-links"></a>Verwandte Links
- [SQL Server-Treiber](http://msdn.microsoft.com/library/mt654049.aspx) für die Verbindung von Clientanwendungen
