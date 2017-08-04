---
title: Herstellen einer Verbindung mit einer SQL Server-Datenquelle (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 17910c8e30dee98f39e977896fb67774b54a798d
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer SQL Server-Datenquelle (SQL Server-Import / Export-Assistent)
Dieses Thema veranschaulicht das Herstellen von Verbindungen ein **Microsoft SQL Server** Datenquelle aus der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf der Seite der SQL Server-Import / Export-Assistenten. Es sind mehrere Datenanbieter, die Sie verwenden können, um die Verbindung mit SQL Server.

> [!TIP]
> Wenn Sie in einem Netzwerk mit mehreren Servern sind, kann es einfacher sein, geben den Servernamen, anstatt die Dropdown-Liste der Server zu erweitern. Wenn Sie die Dropdownliste klicken, dauert möglicherweise sehr lange, um das Netzwerk für alle verfügbaren Server abzufragen und die Ergebnisse eventuell noch nicht den gewünschten Server.

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Herstellen einer Verbindung mit SQL Server mithilfe des .NET Framework-Datenanbieters für SQL Server 
Nach der Auswahl **.NET Framework-Datenanbieter für SQL Server** auf die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite des Assistenten die Seite zeigt eine gruppierte Liste von Optionen für den Anbieter. Viele davon werden ungeeignete Namen und Einstellungen nicht vertraut. Zum Enterprise-Datenbank herstellen, müssen Sie Glücklicherweise in der Regel nur wenige Informationen angeben. Sie können die Standardwerte für die anderen Einstellungen ignorieren.

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter sind identisch, ob SQL Server die Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

|Erforderliche Informationen|.NET Framework-Datenanbieter für SQL Server-Eigenschaft|
|---|---|
|Servername|**Datenquelle**|
|Authentifizierungsinformationen (Anmeldenamen)|**Integrierte Sicherheit von**; oder, **Benutzer-ID** und **Kennwort**<br/>Wenn Sie eine Dropdown-Liste der Datenbanken auf dem Server anzeigen möchten, müssen Sie zunächst gültige Anmeldeinformationen bereitstellen.|
|Datenbankname|**Anfangskatalog**|

![Verbinden Sie mit SQL mit .NET-Anbieter](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>Optionen (.NET Framework-Datenanbieter für SQL Server) angeben.

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter sind identisch, ob SQL Server die Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

**Datenquelle**  
 Geben Sie den Namen oder die IP-Adresse des Servers Quell- oder Zielschema, oder wählen Sie einen Server aus der Dropdown-Liste.  
 
 Um einen nicht standardmäßigen TCP-Port anzugeben, geben Sie ein Komma nach dem Servernamen oder IP-Adresse, und geben Sie die Portnummer an.
 
 **Anfangskatalog**  
 Geben Sie den Namen der Quelle oder Ziel-Datenbank, oder wählen Sie eine Datenbank aus der Dropdown-Liste.  
  
 **Integrierte Sicherheit**  
 Geben Sie **"true"** für die Verbindung mit integrierter Windows-Authentifizierung (empfohlen) oder **"false"** für die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung. Wenn Sie **FALSE** angeben, müssen Sie eine Benutzer-ID und ein Kennwort eingeben. Der Standardwert ist **False**.  
  
 **Benutzer-ID**  
 Geben Sie einen Benutzernamen bei Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.  
  
 **Kennwort**  
 Geben Sie das Kennwort bei Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentifizierung.  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>Verbinden Sie mit SQL Server mit dem ODBC-Treiber für SQL Server 
ODBC-Treiber sind nicht in der Dropdown-Liste der Datenquellen aufgeführt. Um mit einem ODBC-Treiber eine Verbindung herzustellen, starten Sie dazu die **.NET Framework-Datenanbieter für ODBC** als Datenquelle. Dieser Anbieter dient als Wrapper um die ODBC-Treiber.

> [!TIP]
> **Abrufen den neuesten Treiber**. Herunterladen der [Microsoft ODBC Driver 13 for SQLServer](https://www.microsoft.com/download/details.aspx?id=53339).

Hier ist die generische Bildschirm sofort nach der Auswahl der .NET Framework-Datenanbieter für ODBC.

![Herstellen einer Verbindung mit SQL mit ODBC vor](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>Optionen (ODBC-Treiber für SQL Server) angeben

> [!NOTE]
> Die Verbindungsoptionen für den ODBC-Treiber sind identisch, ob SQL Server die Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

Um mit den aktuellen ODBC-Treiber mit SQL Server zu verbinden, stellen Sie eine Verbindungszeichenfolge, die die folgenden Einstellungen und deren Werte enthält. Das Format der eine vollständige Verbindungszeichenfolge folgt unmittelbar auf die Liste der Einstellungen.

> [!TIP]
> Abrufen von Hilfe Zusammenstellen einer Verbindungszeichenfolge, die gerade geeignet ist. Geben Sie statt einer Verbindungszeichenfolge eine vorhandene DSN (Data Source Name) oder erstellen Sie ein neues. Weitere Informationen zu diesen Optionen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Treiber**  
Der Name des ODBC-Treibers. Der Name ist für unterschiedliche Versionen des Treibers.

**Server**  
Der Name des SQL-Servers.

**Datenbank**  
Der Name der Datenbank.  

**Trusted_Connection**; oder, **Uid** und **Pwd**  
Geben Sie **Trusted_Connection = Yes** zum Herstellen einer Verbindung mit der integrierten Windows-Authentifizierung; oder geben Sie **Uid** (Benutzer-Id) und **Pwd** (Kennwort) für die Verbindung mit SQL Server-Authentifizierung.

### <a name="connection-string-format"></a>Format der Verbindungszeichenfolge
Hier ist das Format einer Verbindungszeichenfolge, die integrierte Windows-Authentifizierung verwendet.

    Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;

Hier ist das Format einer Verbindungszeichenfolge, die SQL Server-Authentifizierung statt der integrierten Windows-Authentifizierung verwendet.

     Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;

### <a name="enter-the-connection-string"></a>Geben Sie die Verbindungszeichenfolge
Geben Sie die Verbindungszeichenfolge in der **"ConnectionString"** Feld aus, oder geben Sie den DNS-Namen in der **Dsn** Feld, auf die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Nachdem Sie die Verbindungszeichenfolge eingeben, wird der Assistent analysiert die Zeichenfolge und zeigt die einzelnen Eigenschaften und ihre Werte in der Liste.

Im folgenden Beispiel wird diese Verbindungszeichenfolge.

    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;

Hier ist der Bildschirm, den nach dem Eingeben der Verbindungszeichenfolge angezeigt.

![Herstellen einer Verbindung mit SQL mit ODBC nach](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>Verbinden Sie mit SQLServer mit der Microsoft OLE DB-Anbieter für SQLServer oder SQL Server Native Client

> [!IMPORTANT]
> Microsoft OLE DB-Anbieter für SQL Server und SQL Server Native Client werden nicht in Versionen von SQL Server nach SQL Server 2012 unterstützt. Verwenden Sie stattdessen den ODBC-Treiber. Weitere Informationen zu den Übergang zu den ODBC-Treiber finden Sie unter den folgenden Blogbeiträgen.
>   -   [Microsoft ist mit ODBC für systemeigenen relationalen Datenzugriff ausrichten.](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [Einführung in die neue Microsoft ODBC-Treiber für SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>Weitere Informationen und andere Datenanbieter
Informationen zum Verbinden mit SQL Server mit einem Datenanbieter, die hier nicht aufgeführt ist, finden Sie unter [SQL Server-Verbindungszeichenfolgen](https://www.connectionstrings.com/sql-server/). Diese Drittanbieter-Website enthält auch Informationen über die Datenanbieter und die Verbindungsparameter, die auf dieser Seite beschriebenen.

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


