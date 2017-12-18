---
title: Herstellen einer Verbindung mit einer PostgreSQL-Datenquelle (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 58d8e69ae49c56716d8d0f5393fad329bd924b21
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer PostgreSQL-Datenquelle (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **PostgreSQL**-Datenquelle über die Seiten **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen. 

> [!IMPORTANT]
> Die detaillierten Anforderungen und Voraussetzungen für das Herstellen einer Verbindung mit einer PostgreSQL-Datenbank sind nicht Gegenstand dieses Microsoft-Artikels. In diesem Artikel wird davon ausgegangen, dass Sie die PostgreSQL-Clientsoftware bereits installiert und erfolgreich eine Verbindung mit der PostgreSQL-Zieldatenbank hergestellt haben. Rufen Sie für weitere Informationen die PostgreSQL-Dokumentation auf, oder wenden Sie sich an Ihren PostgreSQL-Datenbankadministrator.

## <a name="get-the-postgresql-odbc-driver"></a>Installieren des ODBC-Treibers für PostgreSQL

### <a name="install-the-odbc-driver-with-stack-builder"></a>Installieren des ODBC-Treibers mit Stack Builder
Führen Sie Stack Builder aus, um den ODBC-Treiber für PostgreSQL (psqlODBC) zu Ihrer Installation von PostgreSQL hinzuzufügen.

![Installieren von PostgreSQL ODBC mit Stack Builder](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>Herunterladen des aktuellen ODBC-Treibers
Laden Sie alternativ Windows Installer für die aktuelle Version des PostgreSQL ODBC-Treibers (psqlODBC) direkt von der FTP-Website [https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/) herunter. Extrahieren Sie die Dateien aus der ZIP-Datei, und führen Sie die MSI-Datei aus.

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>Herstellen einer Verbindung mit PostgreSQL mithilfe des ODBC-Treibers für PostgreSQL (psqlODBC)
ODBC-Treiber werden in der Dropdownliste der Datenquellen nicht aufgeführt. Wählen Sie zunächst **.NET Framework-Datenanbieter für ODBC** auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** als Datenquelle aus, um eine Verbindung mit einem ODBC-Treiber herzustellen. Dieser Anbieter dient als Wrapper für den ODBC-Treiber.

In der folgenden Abbildung wird die generische Anzeige dargestellt, die Ihnen unmittelbar angezeigt wird, nachdem Sie „.NET Framework-Datenanbieter für ODBC“ ausgewählt haben.

![Herstellen einer Verbindung mit PostgreSQL mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>Anzugebende Optionen (ODBC-Treiber für PostgreSQL)

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter und den ODBC-Treiber bleiben stets unverändert – egal, ob PostgreSQL die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

Assemblieren Sie eine Verbindungszeichenfolge, die folgende Einstellungen und deren Werte enthält, um eine Verbindung mit PostgreSQL mithilfe des ODBC-Treibers für PostgreSQL herzustellen. Das Format einer vollständigen Verbindungszeichenfolge wird direkt nach der Liste der Einstellungen angezeigt.

> [!TIP]
> Erhalten Sie Hilfe beim Assemblieren einer richtigen Verbindungszeichenfolge. Stellen Sie alternativ einen vorhandenen DSN (Datenquellennamen, Data Source Name) bereit, oder erstellen Sie einen neuen, statt eine Verbindungszeichenfolge anzugeben. Weitere Informationen zu diesen Optionen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Treiber**  
Der Name des ODBC-Treibers: **PostgreSQL ODBC Driver (UNICODE)** oder **PostgreSQL ODBC Driver (ANSI)**.

**Server**  
Der Name des PostgreSQL-Servers. 

**Port**  
Der Port, der verwendet wird, um eine Verbindung mit dem PostgreSQL-Server herzustellen.

**Datenbank**  
Der Name der PostgreSQL-Datenbank.

**UID** und **PWD**   
Die **UID** (Benutzer-ID) und das **PWD** (Kennwort) für das Herstellen einer Verbindung.

### <a name="connection-string-format"></a>Format der Verbindungszeichenfolge
Im Folgenden finden Sie das Format einer typischen Verbindungszeichenfolge. 

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>Eingeben der Verbindungszeichenfolge
Geben Sie die Verbindungszeichenfolge in das Feld **ConnectionString** ein, oder geben Sie den DSN-Namen in das Feld **Dsn** auf der Seite **Datenquelle auswählen** oder **Ziel auswählen** ein. Nach der Eingabe der Verbindungszeichenfolge analysiert der Assistent die Zeichenfolge und zeigt die einzelnen Eigenschaften und deren Werte in der Liste an.

Im folgenden Beispiel wird diese Verbindungszeichenfolge verwendet.

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
    ```

In der folgenden Abbildung wird die Ansicht dargestellt, die Ihnen angezeigt wird, nachdem Sie die Verbindungszeichenfolge eingegeben haben.

![Herstellen einer Verbindung mit PostgreSQL mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Andere Datenanbieter und weitere Informationen
Weitere Informationen zum Herstellen einer Verbindung mit PostgreSQL mithilfe eines nicht hier aufgeführten Datenanbieters finden Sie unter [PostgreSQL connection strings (PostgreSQL-Verbindungszeichenfolgen)](https://www.connectionstrings.com/postgresql/). Diese Drittanbieterseite enthält Informationen über die Datenanbieter und die auf dieser Seite beschriebenen Verbindungsparameter.

## <a name="see-also"></a>Siehe auch
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

