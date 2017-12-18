---
title: Herstellen einer Verbindung mit einer Oracle-Datenquelle (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
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
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f2a93e5d4c038db3620e78a4141ca8235d703263
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>Verbinden mit einer Oracle-Datenquelle (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **Oracle**-Datenquelle von den Seiten **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen. Es gibt mehrere Datenanbieter, die Sie verwenden können, um eine Verbindung mit Oracle herzustellen.

> [!IMPORTANT]
> Die detaillierten Anforderungen und Voraussetzungen für das Herstellen einer Verbindung mit einer Oracle-Datenbank sind nicht Gegenstand dieses Microsoft-Artikels. In diesem Artikel wird davon ausgegangen, dass Sie die Oracle-Clientsoftware bereits installiert und erfolgreich eine Verbindung mit der Oracle-Zieldatenbank hergestellt haben. Rufen Sie für weitere Informationen die Oracle-Dokumentation auf, oder wenden Sie sich an Ihren Oracle-Datenbankadministrator.

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>Herstellen einer Verbindung mit Oracle mithilfe des .NET Framework-Datenanbieters für Oracle
Nachdem Sie **.NET Framework-Datenanbieter für Oracle** auf der Seite **Datenquelle auswählen** oder **Ziel auswählen** des Assistenten ausgewählt haben, zeigt die Seite Ihnen eine gruppierte Liste von Optionen für den Anbieter an. Darunter befinden sich viele ungeeignete Namen und ungewöhnliche Einstellungen. Sie müssen jedoch nur zwei bis drei Informationen angeben. Die Standardwerte für die anderen Einstellungen können Sie ignorieren.

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter bleiben stets unverändert – egal, ob Oracle die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

|Erforderliche Informationen|.NET Framework-Datenanbieter für die Oracle-Eigenschaft|
|---|---|
|Servername|**Datenquelle**|
|Authentifizierungsinformationen (Anmeldung)|**Benutzer-ID** und **Kennwort**, oder **Integrierte Sicherheit**|

Sie müssen die Verbindungszeichenfolge nicht im Feld **ConnectionString** in der Liste eintragen. Nachdem Sie einzelne Werte für den Oracle-Servernamen (**Datenquelle**) und die Anmeldedaten eingegeben haben, assembliert der Assistent die Verbindungszeichenfolge aus den einzelnen Eigenschaften und deren Werten. 

![Herstellen einer Verbindung mit Oracle mithilfe des .NET-Anbieters](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Herstellen einer Verbindung mit Oracle mithilfe des Microsoft ODBC-Treibers für Oracle
ODBC-Treiber werden in der Dropdownliste der Datenquellen nicht aufgeführt. Wählen Sie zunächst **.NET Framework-Datenanbieter für ODBC** auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** als Datenquelle aus, um eine Verbindung mit einem ODBC-Treiber herzustellen. Dieser Anbieter dient als Wrapper für den ODBC-Treiber.

In der folgenden Abbildung wird die generische Anzeige dargestellt, die Ihnen unmittelbar angezeigt wird, nachdem Sie „.NET Framework-Datenanbieter für ODBC“ ausgewählt haben.

![Herstellen einer Verbindung mit Oracle mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>Anzugebende Optionen (ODBC-Treiber für Oracle)

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter und den ODBC-Treiber bleiben stets unverändert – egal, ob Oracle die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

Assemblieren Sie eine Verbindungszeichenfolge, die folgende Einstellungen und deren Werte enthält, um eine Verbindung mit Oracle mithilfe des aktuellen ODBC-Treibers für Oracle herzustellen. Das Format einer vollständigen Verbindungszeichenfolge wird direkt nach der Liste der Einstellungen angezeigt.

> [!TIP]
> Erhalten Sie Hilfe beim Assemblieren einer passenden Verbindungszeichenfolge. Stellen Sie alternativ einen vorhandenen DSN (Datenquellennamen, Data Source Name) bereit, oder erstellen Sie einen neuen, anstatt eine Verbindungszeichenfolge anzugeben. Weitere Informationen zu diesen Optionen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Treiber**  
Der Name das ODBC-Treibers **Microsoft ODBC für Oracle**.

**Server**  
Der Name des Oracle-Servers. 

**UID** und **PWD**   
Die Benutzer-ID und das Kennwort für die Verbindung.

### <a name="connection-string-format"></a>Format der Verbindungszeichenfolge
Im Folgenden finden Sie das Format einer typischen Verbindungszeichenfolge.

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>Eingeben der Verbindungszeichenfolge
Geben Sie die Verbindungszeichenfolge in das Feld **ConnectionString** ein, oder geben Sie den DSN-Namen in das Feld **Dsn** auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** ein. Nach der Eingabe der Verbindungszeichenfolge analysiert der Assistent die Zeichenfolge und zeigt die einzelnen Eigenschaften und deren Werte in der Liste an.

In der folgenden Abbildung wird die Ansicht dargestellt, die Ihnen angezeigt wird, nachdem Sie die Verbindungszeichenfolge eingegeben haben.

![Herstellen einer Verbindung mit Oracle mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>Oracle-Servername
Führen Sie eine der folgenden Abfragen aus, um den Namen des Oracle-Servers abzurufen.

`SELECT host_name FROM v$instance`

oder

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>Andere Datenanbieter und weitere Informationen
Weitere Informationen zum Herstellen einer Verbindung mit Oracle mithilfe eines nicht hier aufgeführten Datenanbieters finden Sie unter [Oracle connection strings (Oracle-Verbindungszeichenfolgen)](https://www.connectionstrings.com/oracle/). Diese Drittanbieterseite enthält Informationen über die Datenanbieter und die auf dieser Seite beschriebenen Verbindungsparameter.

## <a name="see-also"></a>Siehe auch
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Ziel auswählen](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

