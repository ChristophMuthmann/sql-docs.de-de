---
title: Herstellen einer Verbindung mit einer SQL Server-Datenquelle (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
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
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 79a1f98f64096d11faf25a75e681518546bbd21e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer SQL Server-Datenquelle (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **Microsoft SQL Server**-Datenquelle über die Seiten **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen. Es gibt mehrere Datenanbieter, die Sie verwenden können, um eine Verbindung mit SQL Server herzustellen.

> [!TIP]
> Wenn ein Netzwerk mehrere Server enthält, kann es einfacher sein, den Servernamen einzugeben, statt die Dropdownliste der Server zu erweitern. Wenn Sie auf die Dropdownliste klicken, kann es einige Zeit dauern, das Netzwerk nach allen verfügbaren Servern abzufragen, und die Ergebnisse enthalten den gewünschten Server möglicherweise nicht.

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Herstellen einer Verbindung mit SQL Server mithilfe des .NET Framework-Datenanbieters für SQL Server 
Nachdem Sie **.NET Framework-Datenanbieter für SQL Server** auf der Seite **Datenquelle auswählen** oder **Ziel auswählen** des Assistenten ausgewählt haben, zeigt die Seite Ihnen eine gruppierte Liste von Optionen für den Anbieter an. Darunter befinden sich viele ungeeignete Namen und ungewöhnliche Einstellungen. Damit Sie eine Verbindung mit einer Unternehmensdatenbank herstellen können, benötigen Sie in der Regel nur wenige Informationen. Die Standardwerte für die anderen Einstellungen können Sie ignorieren.

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter bleiben stets unverändert – egal, ob SQL Server die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

|Erforderliche Informationen|Eigenschaft „.NET Framework-Datenanbieter für SQL Server“|
|---|---|
|Servername|**Datenquelle**|
|Authentifizierungsinformationen (Anmeldung)|**Integrierte Sicherheit** oder **Benutzer-ID** und **Kennwort**<br/>Wenn eine Dropdownliste mit den Datenbanken auf dem Server angezeigt werden soll, müssen Sie zunächst gültige Anmeldeinformationen eingeben.|
|Datenbankname|**Anfangskatalog**|

![Herstellen einer Verbindung mit SQL mithilfe des .NET-Anbieters](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>Anzugebende Optionen (.NET Framework-Datenanbieter für SQL Server)

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter bleiben stets unverändert – egal, ob SQL Server die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

**Datenquelle**  
 Geben Sie den Namen oder die IP-Adresse des Quell- oder Zielservers ein, oder wählen Sie einen Server aus der Dropdownliste aus.  
 
 Geben Sie ein Komma nach dem Servernamen oder der IP-Adresse und dann die Portnummer ein, um einen nicht dem Standard entsprechenden TCP-Port einzurichten.
 
 **Anfangskatalog**  
 Geben Sie den Namen der Quell- oder Zieldatenbank ein, oder wählen Sie eine Datenbank aus der Dropdownliste aus.  
  
 **Integrierte Sicherheit**  
 Geben Sie **TRUE** an, um eine Verbindung mit der integrierten Windows-Authentifizierung herzustellen (empfohlen), oder **FALSE**, um eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung herzustellen. Wenn Sie **FALSE** angeben, müssen Sie eine Benutzer-ID und ein Kennwort eingeben. Der Standardwert ist **False**.  
  
 **Benutzer-ID**  
 Geben Sie einen Benutzernamen ein, wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwenden.  
  
 **Kennwort**  
 Geben Sie das Kennwort ein, wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwenden.  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>Herstellen einer Verbindung mit SQL Server mithilfe des ODBC-Treibers für SQL Server 
ODBC-Treiber werden in der Dropdownliste der Datenquellen nicht aufgeführt. Wählen Sie zunächst **.NET Framework-Datenanbieter für ODBC** als Datenquelle aus, um eine Verbindung mit einem ODBC-Treiber herzustellen. Dieser Anbieter dient als Wrapper für den ODBC-Treiber.

> [!TIP]
> **Laden Sie den neuesten Treiber herunter**. Laden Sie [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339) herunter.

In der folgenden Abbildung wird die generische Anzeige dargestellt, die Ihnen unmittelbar angezeigt wird, nachdem Sie „.NET Framework-Datenanbieter für ODBC“ ausgewählt haben.

![Herstellen einer Verbindung mit SQL mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>Anzugebende Optionen (ODBC-Treiber für SQL Server)

> [!NOTE]
> Die Verbindungsoptionen für den ODBC-Treiber bleiben stets unverändert – egal, ob SQL Server die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

Assemblieren Sie eine Verbindungszeichenfolge, die folgende Einstellungen und deren Werte enthält, um eine Verbindung mit SQL Server mithilfe des aktuellen ODBC-Treibers herzustellen. Das Format einer vollständigen Verbindungszeichenfolge wird direkt nach der Liste der Einstellungen angezeigt.

> [!TIP]
> Erhalten Sie Hilfe beim Assemblieren einer richtigen Verbindungszeichenfolge. Stellen Sie alternativ einen vorhandenen DSN (Datenquellennamen, Data Source Name) bereit, oder erstellen Sie einen neuen, statt eine Verbindungszeichenfolge anzugeben. Weitere Informationen zu diesen Optionen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Treiber**  
Der Name des ODBC-Treibers. Der Name unterscheidet sich bei unterschiedlichen Versionen des Treibers.

**Server**  
Der Name des SQL-Servers.

**Datenbank**  
Der Name der Datenbank.  

**Trusted_Connection** oder **UID** und **PWD**.  
Geben Sie **Trusted_Connection=Yes** an, um eine Verbindung mit der integrierten Windows-Authentifizierung herzustellen, oder **UID** (Benutzer-ID) und **PWD** (Kennwort), um eine Verbindung mit der SQL Server-Authentifizierung herzustellen.

### <a name="connection-string-format"></a>Format der Verbindungszeichenfolge
Im Folgenden finden Sie das Format einer Verbindungszeichenfolge, die die integrierte Windows-Authentifizierung verwendet.

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

Im Folgenden finden Sie das Format einer Verbindungszeichenfolge, die die SQL Server-Authentifizierung statt der integrierten Windows-Authentifizierung verwendet.

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>Eingeben der Verbindungszeichenfolge
Geben Sie die Verbindungszeichenfolge in das Feld **ConnectionString** ein, oder geben Sie den DSN-Namen in das Feld **Dsn** auf der Seite **Datenquelle auswählen** oder **Ziel auswählen** ein. Nach der Eingabe der Verbindungszeichenfolge analysiert der Assistent die Zeichenfolge und zeigt die einzelnen Eigenschaften und deren Werte in der Liste an.

Im folgenden Beispiel wird diese Verbindungszeichenfolge verwendet.

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

In der folgenden Abbildung wird die Ansicht dargestellt, die Ihnen angezeigt wird, nachdem Sie die Verbindungszeichenfolge eingegeben haben.

![Herstellen einer Verbindung mit SQL mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>Herstellen einer Verbindung mit dem Microsoft OLEDB-Anbieter für SQL Server oder SQL Server Native Client

> [!IMPORTANT]
> Der Microsoft OLEDB-Anbieter für SQL Server und SQL Server Native Client wird in Versionen nach SQL Server 2012 nicht unterstützt. Verwenden Sie stattdessen den ODBC-Treiber. Weitere Informationen zum Wechsel zum ODBC-Treiber finden Sie in den folgenden Blogbeiträgen.
>   -   [Microsoft is Aligning with ODBC for Native Relational Data Access (Microsoft richtet ODBC auf den nativen relationalen Datenzugriff aus)](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [Introducing the new Microsoft ODBC Drivers for SQL Server (Einführung des neuen Microsoft ODBC-Treibers für SQL Server)](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>Andere Datenanbieter und weitere Informationen
Weitere Informationen zum Herstellen einer Verbindung mit SQL Server mithilfe eines nicht hier aufgeführten Datenanbieters finden Sie unter [SQL Server connection strings (SQL Server-Verbindungszeichenfolgen)](https://www.connectionstrings.com/sql-server/). Diese Drittanbieterseite enthält Informationen über die Datenanbieter und die auf dieser Seite beschriebenen Verbindungsparameter.

## <a name="see-also"></a>Siehe auch
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

