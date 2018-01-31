---
title: Herstellen einer Verbindung mit einer MySQL-Datenquelle (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d011a5b39f6aded3bc305c922b5d2788026559e2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer MySQL-Datenquelle (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **MySQL**-Datenquelle über die Seiten **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen. Es gibt mehrere Datenanbieter, die Sie verwenden können, um eine Verbindung mit MySQL herzustellen.

> [!IMPORTANT]
> Die detaillierten Anforderungen und Voraussetzungen für das Herstellen einer Verbindung mit einer MySQL-Datenbank sind nicht Gegenstand dieses Microsoft-Artikels. In diesem Artikel wird davon ausgegangen, dass Sie die MySQL-Clientsoftware bereits installiert und erfolgreich eine Verbindung mit der MySQL-Zieldatenbank hergestellt haben. Rufen Sie für weitere Informationen die MySQL-Dokumentation auf, oder wenden Sie sich an Ihren MySQL-Datenbankadministrator.

## <a name="get-the-mysql-connectors"></a>Herunterladen der MySQL-Connectors
Laden Sie die Anbieter und Treiber, die in diesem Artikel beschrieben werden, von der Seite [MySQL-Connectors](https://dev.mysql.com/downloads/connector/) herunter.

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>Herstellen einer Verbindung mit MySQL mithilfe des .NET Framework-Datenanbieters für MySQL
Nachdem Sie **.NET Framework-Datenanbieter für MySQL** auf der Seite **Datenquelle auswählen** oder **Ziel auswählen** des Assistenten ausgewählt haben, zeigt die Seite Ihnen eine gruppierte Liste von Optionen für den Anbieter an. Darunter befinden sich viele ungeeignete Namen und ungewöhnliche Einstellungen. Sie müssen jedoch nur wenige Informationen angeben. Die Standardwerte für die anderen Einstellungen können Sie ignorieren.

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter bleiben stets unverändert – egal, ob MySQL die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

|Erforderliche Informationen|Eigenschaft des .NET Framework-Datenanbieters für MySQL|
|---|---|
|Servername|**Server**|
|Datenbankname|**Datenbank**|
|Authentifizierungsinformationen (Anmeldung)|**Benutzer-ID** und **Kennwort**|

Sie müssen die Verbindungszeichenfolge nicht im Feld **ConnectionString** in der Liste eintragen. Nachdem Sie einzelne Werte für den MySQL-Servernamen (**Server**) und die Anmeldedaten eingegeben haben, assembliert der Assistent die Verbindungszeichenfolge aus den einzelnen Eigenschaften und deren Werten. 

![Herstellen einer Verbindung mit MySQL mithilfe des .NET-Anbieters, 1 von 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![Herstellen einer Verbindung mit MySQL mithilfe des .NET-Anbieters, 2 von 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>Herstellen einer Verbindung mit MySQL mithilfe des ODBC-Treibers für MySQL
ODBC-Treiber werden in der Dropdownliste der Datenquellen nicht aufgeführt. Wählen Sie zunächst **.NET Framework-Datenanbieter für ODBC** auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** als Datenquelle aus, um eine Verbindung mit einem ODBC-Treiber herzustellen. Dieser Anbieter dient als Wrapper für den ODBC-Treiber.

In der folgenden Abbildung wird die generische Anzeige dargestellt, die Ihnen unmittelbar angezeigt wird, nachdem Sie „.NET Framework-Datenanbieter für ODBC“ ausgewählt haben.

![Herstellen einer Verbindung mit SQL mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>Anzugebende Optionen (ODBC-Treiber für MySQL)

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter und den ODBC-Treiber bleiben stets unverändert – egal, ob MySQL die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

Assemblieren Sie eine Verbindungszeichenfolge, die folgende Einstellungen und deren Werte enthält, um eine Verbindung mit MySQL mithilfe des ODBC-Treibers für MySQL herzustellen. Das Format einer vollständigen Verbindungszeichenfolge wird direkt nach der Liste der Einstellungen angezeigt.

> [!TIP]
> Erhalten Sie Hilfe beim Assemblieren einer passenden Verbindungszeichenfolge. Stellen Sie alternativ einen vorhandenen DSN (Datenquellennamen, Data Source Name) bereit, oder erstellen Sie einen neuen, statt eine Verbindungszeichenfolge anzugeben. Weitere Informationen zu diesen Optionen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Treiber**  
Der Name des ODBC-Treibers.

**Server**  
Der Name des MySQL-Servers. 

**Datenbank**  
Der Name der MySQL-Datenbank.

**UID** und **PWD**   
Die Benutzer-ID und das Kennwort für die Verbindung.

### <a name="connection-string-format"></a>Format der Verbindungszeichenfolge
Im Folgenden finden Sie das Format einer typischen Verbindungszeichenfolge.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>Eingeben der Verbindungszeichenfolge
Geben Sie die Verbindungszeichenfolge in das Feld **ConnectionString** ein, oder geben Sie den DSN-Namen in das Feld **Dsn** auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** ein. Nach der Eingabe der Verbindungszeichenfolge analysiert der Assistent die Zeichenfolge und zeigt die einzelnen Eigenschaften und deren Werte in der Liste an.

Im folgenden Beispiel wird diese Verbindungszeichenfolge verwendet.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
    ```

In der folgenden Abbildung wird die Ansicht dargestellt, die Ihnen angezeigt wird, nachdem Sie die Verbindungszeichenfolge eingegeben haben.

![Herstellen einer Verbindung mit MySQL mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Andere Datenanbieter und weitere Informationen
Weitere Informationen zum Herstellen einer Verbindung mit MySQL mithilfe eines nicht hier aufgeführten Datenanbieters finden Sie unter [MySQL connection strings (MySQL-Verbindungszeichenfolgen)](https://www.connectionstrings.com/mysql/). Diese Drittanbieterseite enthält Informationen über die Datenanbieter und die auf dieser Seite beschriebenen Verbindungsparameter.

## <a name="see-also"></a>Siehe auch
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

