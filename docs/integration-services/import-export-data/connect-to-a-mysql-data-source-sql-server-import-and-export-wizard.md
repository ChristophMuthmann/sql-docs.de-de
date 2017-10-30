---
title: Herstellen einer Verbindung mit einer MySQL-Datenquelle (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3df56fcda5b39c2895de83feac4f302686b1adf3
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer MySQL-Datenquelle (SQL Server-Import / Export-Assistent)
Dieses Thema veranschaulicht das Herstellen von Verbindungen ein **MySQL** Datenquelle aus der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf der Seite der SQL Server-Import / Export-Assistenten. Es sind mehrere Datenanbieter, die Sie verwenden können, für die Verbindung mit MySQL.

> [!IMPORTANT]
> Die detaillierten Anforderungen und erforderliche Komponenten für die Verbindung mit einer MySQL-Datenbank sind nicht Gegenstand dieses Artikels Microsoft. In diesem Artikel wird davon ausgegangen, dass Sie bereits MySQL-Clientsoftware installiert haben und dass Sie bereits das Ziel MySQL-Datenbank hergestellt werden können. Weitere Informationen finden Sie in der MySQL-Datenbank-Administrator oder der MySQL-Dokumentation.

## <a name="get-the-mysql-connectors"></a>Ruft die MySQL-connectors
Laden Sie die Anbieter und-Treiber beschrieben, die in diesem Thema aus dem [MySQL-Connectors](https://dev.mysql.com/downloads/connector/) Seite.

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>Verbinden Sie mit MySQL mit dem .net Framework-Datenanbieter für MySQL
Nach der Auswahl **.NET Framework-Datenanbieter für MySQL** auf die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite des Assistenten die Seite zeigt eine gruppierte Liste von Optionen für den Anbieter. Viele davon werden ungeeignete Namen und Einstellungen nicht vertraut. Glücklicherweise müssen Sie nur wenige Informationen angeben. Sie können die Standardwerte für die anderen Einstellungen ignorieren.

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter sind identisch, ob MySQL Ihrer Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

|Erforderliche Informationen|.NET Framework-Datenanbieter für MySQL-Eigenschaft|
|---|---|
|Servername|**Server**|
|Datenbankname|**Datenbank**|
|Authentifizierungsinformationen (Anmeldenamen)|**Benutzer-Id** und **Kennwort**|

Sie müssen die Verbindungszeichenfolge in geben die **"ConnectionString"** Feld der Liste. Nachdem Sie einzelne Werte für den MySQL Server-Namen eingeben (**Server**) und Anmeldedaten, die der Assistent assembliert die Verbindungszeichenfolge aus der einzelnen Eigenschaften und ihre Werte. 

![Verbinden Sie mit MySQL mit dem .NET-Anbieter 1 von 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![Verbinden Sie mit MySQL mit dem .NET-Anbieter 2 von 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>Verbinden Sie mit MySQL mit der MySQL-ODBC-Treiber
ODBC-Treiber sind nicht in der Dropdown-Liste der Datenquellen aufgeführt. Um mit einem ODBC-Treiber eine Verbindung herzustellen, starten Sie dazu die **.NET Framework-Datenanbieter für ODBC** als Datenquelle für die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Dieser Anbieter dient als Wrapper um die ODBC-Treiber.

Hier ist die generische Bildschirm sofort nach der Auswahl der .NET Framework-Datenanbieter für ODBC.

![Herstellen einer Verbindung mit SQL mit ODBC vor](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>Optionen zum festlegen (MySQL-ODBC-Treiber)

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter und ODBC-Treiber werden die gleichen MySQL Ihrer Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

Stellen Sie zum Verbinden mit MySQL mit der MySQL-ODBC-Treiber eine Verbindungszeichenfolge, die die folgenden Einstellungen und deren Werte enthält. Das Format der eine vollständige Verbindungszeichenfolge folgt unmittelbar auf die Liste der Einstellungen.

> [!TIP]
> Abrufen von Hilfe Zusammenstellen einer Verbindungszeichenfolge, die gerade geeignet ist. Geben Sie statt einer Verbindungszeichenfolge eine vorhandene DSN (Data Source Name) oder erstellen Sie ein neues. Weitere Informationen zu diesen Optionen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Treiber**  
Der Name des ODBC-Treibers.

**Server**  
Der Name der MySQL-Server. 

**Datenbank**  
Der Name der MySQL-Datenbank.

**UID** und **PWD**   
Benutzer-Id und Kennwort für die Verbindung.

### <a name="connection-string-format"></a>Format der Verbindungszeichenfolge
Hier ist das Format für eine typische Verbindungszeichenfolge.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>Geben Sie die Verbindungszeichenfolge
Geben Sie die Verbindungszeichenfolge in der **"ConnectionString"** Feld aus, oder geben Sie den DNS-Namen in der **Dsn** Feld, auf die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Nachdem Sie die Verbindungszeichenfolge eingeben, wird der Assistent analysiert die Zeichenfolge und zeigt die einzelnen Eigenschaften und ihre Werte in der Liste.

Im folgenden Beispiel wird diese Verbindungszeichenfolge.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
    ```

Hier ist der Bildschirm, den nach dem Eingeben der Verbindungszeichenfolge angezeigt.

![Herstellen einer Verbindung mit MySQL mit ODBC](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Weitere Informationen und andere Datenanbieter
Informationen zum Verbinden mit MySQL mit einem Datenanbieter, die hier nicht aufgeführt ist, finden Sie unter [MySQL-Verbindungszeichenfolgen](https://www.connectionstrings.com/mysql/). Diese Drittanbieter-Website enthält auch Informationen über die Datenanbieter und die Verbindungsparameter, die auf dieser Seite beschriebenen.

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


