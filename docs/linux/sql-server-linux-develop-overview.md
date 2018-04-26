---
title: Entwickeln von Anwendungen für SQL Server on Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.custom: sql-linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.workload: On Demand
ms.openlocfilehash: 24dca42ea34e6810be4cf015af2dd84d6fa39de9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Erste Schritte Entwickeln von Anwendungen für SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Sie können Anwendungen erstellen, die Herstellen einer Verbindung mit und Verwenden von SQL Server-2017 unter Linux aus einer Vielzahl von Programmiersprachen, z. B. c#, Java, Node.js, PHP, Python, Ruby, und C++. Sie können sich auch auf beliebte webframeworks und Frameworks Objekt Relational Mapping (ORM) aus.

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> Diese gleichen Entwicklungsoptionen ermöglichen Ihnen auch in SQL Server auf anderen Plattformen als Ziel. Anwendungen paketaktualisierungen von SQL Server lokal oder in der Cloud auf MacOS unter Linux, Windows oder Docker. Sie können SQL-Zielserver oder Azure SQL-Datenbank und Azure SQL Data Warehouse.

## <a name="try-the-tutorials"></a>Wiederholen Sie die Lernprogramme

Die beste Möglichkeit, Los und Erstellen von Anwendungen mit SQL Server ist es selbst auszuprobieren.

- Navigieren Sie zu [Lernprogramme "Erste Schritte"](http://aka.ms/sqldev).
- Wählen Sie Ihre Sprache und Entwicklung-Plattform.
- Wiederholen Sie die Codebeispiele aus.

> [!TIP]
> Wenn Sie für SQL Server-2017 auf Docker entwickeln möchten, sehen Sie sich die **MacOS** Lernprogramme.

## <a name="create-new-applications"></a>Erstellen Sie neue Anwendungen

Wenn Sie eine neue Anwendung erstellen, sehen Sie sich eine Liste mit den [verbindungsbibliotheken](sql-server-linux-develop-connectivity-libraries.md) eine Zusammenfassung der Connectors und beliebten Frameworks, die für die verschiedenen Programmiersprachen verfügbar.

## <a name="use-existing-applications"></a>Verwenden Sie vorhandene Anwendungen

Wenn Sie eine vorhandene datenbankanwendung verfügen, können Sie die Verbindungszeichenfolge einfach Ziel 2017 von SQL Server on Linux ändern. Stellen Sie sicher, um zu erfahren, die [bekannte Probleme](sql-server-linux-release-notes.md) in SQL Server-2017 unter Linux.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Verwenden Sie vorhandene SQL-Tools für Windows mit SQL Server on Linux

Tools, die derzeit unter Windows wie SSMS, SSDT und PowerShell ausgeführt, funktionieren auch mit SQL Server-2017 unter Linux. Auch wenn ihnen nicht systemintern unter Linux ausgeführt wird, können Sie weiterhin SQL Server-Remoteinstanz unter Linux verwalten. 

Finden Sie unter den folgenden Themen Weitere Informationen:

- [SQL Server Management Studio (SSMS)](sql-server-linux-develop-use-ssms.md)
- [SQL Server Data Tools (SSDT)](sql-server-linux-develop-use-ssdt.md)
- [SQL-PowerShell](sql-server-linux-manage-powershell.md)

> [!Note] 
> Stellen Sie sicher, dass Sie die neuesten Versionen der Tools für optimale Ergebnisse verwenden.

## <a name="use-new-sql-tools-for-linux"></a>Verwenden Sie neue SQL-Tools für Linux

Sie können die neue [Mssql-Erweiterung](https://aka.ms/mssql-marketplace) für [Visual Studio Code](https://code.visualstudio.com) unter Linux, Mac OS und Windows. Eine schrittweise Anleitung finden Sie im folgenden Lernprogramm:

- [Use Visual Studio Code (Verwenden von Visual Studio Code)](sql-server-linux-develop-use-vscode.md)

Sie können auch neue Befehlszeilentools verwenden, die für Linux native sind. Diese Tools umfassen Folgendes:

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>Nächste Schritte

Installieren Sie SQL Server unter Linux mit einer der folgenden Schnellstarts, um zu beginnen:

- [Installieren Sie auf Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installieren Sie auf SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installieren Sie auf Ubuntu](quickstart-install-connect-ubuntu.md)
- [Führen Sie auf Docker](quickstart-install-connect-ubuntu.md)
