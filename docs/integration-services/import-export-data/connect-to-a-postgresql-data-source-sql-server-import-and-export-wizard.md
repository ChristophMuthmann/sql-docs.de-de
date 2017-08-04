---
title: Herstellen einer Verbindung mit einer PostgreSQL-Datenquelle (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4c82ae7eedc3e18e7591cf7ab30a507920695247
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer PostgreSQL-Datenquelle (SQL Server-Import / Export-Assistent)
Dieses Thema veranschaulicht das Herstellen von Verbindungen ein **PostgreSQL** Datenquelle aus der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf der Seite der SQL Server-Import / Export-Assistenten. 

> [!IMPORTANT]
> Die detaillierten Anforderungen und erforderliche Komponenten für die Verbindung mit einer PostgreSQL-Datenbank sind nicht Gegenstand dieses Artikels Microsoft. In diesem Artikel wird davon ausgegangen, dass Sie bereits PostgreSQL-Clientsoftware installiert haben und dass Sie bereits das Ziel PostgreSQL-Datenbank hergestellt werden können. Weitere Informationen finden Sie in Ihrem Datenbankadministrator PostgreSQL oder PostgreSQL-Dokumentation.

## <a name="get-the-postgresql-odbc-driver"></a>Abrufen des PostgreSQL-ODBC-Treibers

### <a name="install-the-odbc-driver-with-stack-builder"></a>Installieren Sie den ODBC-Treiber mit dem Stack-Generator
Führen Sie Stapel-Generator, um die Installation von PostgreSQL PostgreSQL-ODBC-Treiber (PsqlODBC) hinzuzufügen.

![Installieren Sie PostgreSQL ODBC mit dem Stack-Generator](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>Oder Herunterladen den neuesten ODBC-Treiber
Oder Laden Sie Windows Installer für die neueste Version des PostgreSQL-ODBC-Treibers (PsqlODBC) direkt aus dieser FTP-Site - [https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/). Extrahieren Sie die Dateien aus der ZIP-Datei, und führen Sie die MSI-Datei.

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>Verbinden Sie mit PostgreSQL mit dem PostgreSQL ODBC-Treiber (PsqlODBC)
ODBC-Treiber sind nicht in der Dropdown-Liste der Datenquellen aufgeführt. Um mit einem ODBC-Treiber eine Verbindung herzustellen, starten Sie dazu die **.NET Framework-Datenanbieter für ODBC** als Datenquelle für die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Dieser Anbieter dient als Wrapper um die ODBC-Treiber.

Hier ist die generische Bildschirm sofort nach der Auswahl der .NET Framework-Datenanbieter für ODBC.

![Herstellen einer Verbindung mit PostgreSQL mit ODBC vor](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>Optionen zum festlegen (PostgreSQL-ODBC-Treiber)

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter und ODBC-Treiber werden die gleichen PostgreSQL Ihrer Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

Zum Herstellen von PostgreSQL mit dem PostgreSQL ODBC-Treiber, stellen Sie eine Verbindungszeichenfolge, die die folgenden Einstellungen und deren Werte enthält. Das Format der eine vollständige Verbindungszeichenfolge folgt unmittelbar auf die Liste der Einstellungen.

> [!TIP]
> Abrufen von Hilfe Zusammenstellen einer Verbindungszeichenfolge, die gerade geeignet ist. Geben Sie statt einer Verbindungszeichenfolge eine vorhandene DSN (Data Source Name) oder erstellen Sie ein neues. Weitere Informationen zu diesen Optionen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Treiber**  
Der Name des ODBC-Treibers – entweder **PostgreSQL ODBC Driver(UNICODE)** oder **PostgreSQL ODBC Driver(ANSI)**.

**Server**  
Der Name des Servers PostgreSQL. 

**Port**  
Der Port für die Verbindung mit dem PostgreSQL-Server verwendet werden soll.

**Datenbank**  
Der Name des PostgreSQL-Datenbank.

**UID** und **Pwd**   
Die **Uid** (Benutzer-Id) und **Pwd** (Kennwort) für die Verbindung.

### <a name="connection-string-format"></a>Format der Verbindungszeichenfolge
Hier ist das Format für eine typische Verbindungszeichenfolge. 

    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>

### <a name="enter-the-connection-string"></a>Geben Sie die Verbindungszeichenfolge
Geben Sie die Verbindungszeichenfolge in der **"ConnectionString"** Feld aus, oder geben Sie den DNS-Namen in der **Dsn** Feld, auf die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Nachdem Sie die Verbindungszeichenfolge eingeben, wird der Assistent analysiert die Zeichenfolge und zeigt die einzelnen Eigenschaften und ihre Werte in der Liste.

Im folgenden Beispiel wird diese Verbindungszeichenfolge.

    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********

Hier ist der Bildschirm, den nach dem Eingeben der Verbindungszeichenfolge angezeigt.

![Herstellen einer Verbindung mit PostgreSQL mit ODBC](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Weitere Informationen und andere Datenanbieter
Informationen zur Vorgehensweise beim PostgreSQL mit einem Datenanbieter herstellen, die hier nicht aufgeführt ist, finden Sie unter [PostgreSQL-Verbindungszeichenfolgen](https://www.connectionstrings.com/postgresql/). Diese Drittanbieter-Website enthält auch Informationen über die Datenanbieter und die Verbindungsparameter, die auf dieser Seite beschriebenen.

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


