---
title: Herstellen einer Verbindung mit einer Oracle-Datenquelle (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e589e7f7a0262d258342bf887ec84c57d57dc978
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer Oracle-Datenquelle (SQL Server-Import / Export-Assistent)
Dieses Thema veranschaulicht das Herstellen von Verbindungen ein **Oracle** Datenquelle aus der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf der Seite der SQL Server-Import / Export-Assistenten. Es sind mehrere Datenanbieter, die Sie verwenden können, für die Verbindung zu Oracle.

> [!IMPORTANT]
> Die detaillierten Anforderungen und erforderliche Komponenten für die Verbindung mit einer Oracle-Datenbank sind nicht Gegenstand dieses Artikels Microsoft. In diesem Artikel wird davon ausgegangen, dass Sie bereits die Oracle-Clientsoftware installiert haben und dass Sie bereits mit dem Ziel-Oracle-Datenbank hergestellt werden können. Weitere Informationen finden Sie in der Oracle-Datenbankadministrator oder der Oracle-Dokumentation.

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>Verbinden Sie mit Oracle mit der .net Framework-Datenanbieter für Oracle
Nach der Auswahl **.NET Framework-Datenanbieter für Oracle** auf die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite des Assistenten die Seite zeigt eine gruppierte Liste von Optionen für den Anbieter. Viele davon werden ungeeignete Namen und Einstellungen nicht vertraut. Glücklicherweise müssen Sie nur zwei oder drei Arten von Informationen angeben. Sie können die Standardwerte für die anderen Einstellungen ignorieren.

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter sind identisch, ob Oracle Ihrer Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

|Erforderliche Informationen|.NET Framework-Datenanbieter für Oracle-Eigenschaft|
|---|---|
|Servername|**Datenquelle**|
|Authentifizierungsinformationen (Anmeldenamen)|**Benutzer-ID** und **Kennwort**; oder, **integrierte Sicherheit**|

Sie müssen die Verbindungszeichenfolge in geben die **"ConnectionString"** Feld der Liste. Nach dem Eingeben der einzelnen Werte für den Oracle-Servernamen (**Datenquelle**) und Anmeldedaten, die der Assistent assembliert die Verbindungszeichenfolge aus der einzelnen Eigenschaften und ihre Werte. 

![Verbinden Sie mit Oracle mit .NET-Anbieter](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Mit dem Microsoft ODBC-Treiber für Oracle mit Oracle verbinden
ODBC-Treiber sind nicht in der Dropdown-Liste der Datenquellen aufgeführt. Um mit einem ODBC-Treiber eine Verbindung herzustellen, starten Sie dazu die **.NET Framework-Datenanbieter für ODBC** als Datenquelle für die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Dieser Anbieter dient als Wrapper um die ODBC-Treiber.

Hier ist die generische Bildschirm sofort nach der Auswahl der .NET Framework-Datenanbieter für ODBC.

![Herstellen einer Verbindung mit Oracle ODBC vor](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>Optionen (ODBC-Treiber für Oracle) angeben

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter und ODBC-Treiber sind identisch, ob Oracle Ihrer Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

Stellen Sie eine Verbindungszeichenfolge, die die folgenden Einstellungen und deren Werte enthält, zur Verbindung mit Oracle mit der ODBC-Treiber für Oracle. Das Format der eine vollständige Verbindungszeichenfolge folgt unmittelbar auf die Liste der Einstellungen.

> [!TIP]
> Abrufen von Hilfe Zusammenstellen einer Verbindungszeichenfolge, die gerade geeignet ist. Geben Sie statt einer Verbindungszeichenfolge eine vorhandene DSN (Data Source Name) oder erstellen Sie ein neues. Weitere Informationen zu diesen Optionen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Treiber**  
Der Name des ODBC-Treibers **Microsoft ODBC für Oracle**.

**Server**  
Der Name des Oracle-Servers. 

**UID** und **Pwd**   
Benutzer-Id und Kennwort für die Verbindung.

### <a name="connection-string-format"></a>Format der Verbindungszeichenfolge
Hier ist das Format für eine typische Verbindungszeichenfolge.

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>Geben Sie die Verbindungszeichenfolge
Geben Sie die Verbindungszeichenfolge in der **"ConnectionString"** Feld aus, oder geben Sie den DNS-Namen in der **Dsn** Feld, auf die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Nachdem Sie die Verbindungszeichenfolge eingeben, wird der Assistent analysiert die Zeichenfolge und zeigt die einzelnen Eigenschaften und ihre Werte in der Liste.

Hier ist der Bildschirm, den nach dem Eingeben der Verbindungszeichenfolge angezeigt.

![Herstellen einer Verbindung mit Oracle mit ODBC](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>Wie lautet meine Oracle Servername?
Führen Sie einen der folgenden Abfragen, um den Namen des Oracle-Server abzurufen.

`SELECT host_name FROM v$instance`

oder

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>Weitere Informationen und andere Datenanbieter
Weitere Informationen dazu, wie die Verbindung mit Oracle mit einem Datenanbieter, die hier nicht aufgeführt ist, finden Sie unter [Oracle-Verbindungszeichenfolgen](https://www.connectionstrings.com/oracle/). Diese Drittanbieter-Website enthält auch Informationen über die Datenanbieter und die Verbindungsparameter, die auf dieser Seite beschriebenen.

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


