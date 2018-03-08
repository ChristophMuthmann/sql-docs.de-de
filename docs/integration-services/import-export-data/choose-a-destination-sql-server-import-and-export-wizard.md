---
title: "Ziel auswählen (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
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
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 192e3acf3aae6f26a1c67188b022c45fea08b238
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Ziel auswählen (SQL Server-Import/Export-Assistent)
 Nachdem Sie Informationen zur Quelle Ihrer Daten bereitgestellt haben und darüber, wie Sie eine Verbindung mit ihnen herstellen, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent **Ziel auswählen**an. Auf dieser Seite geben Sie Informationen zum Ziel für Ihre Daten an und dazu, wie Sie eine Verbindung damit herstellen.
  
Weitere Informationen zu Datenzielen, die Sie verwenden können, finden Sie unter [Welche Datenquellen und Ziele kann ich verwenden?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources). 

## <a name="screen-shot-of-the-destination-page"></a>Screenshot der Zielseite
Der folgende Screenshot zeigt den ersten Teil der Seite **Ziel auswählen** des Assistenten an. Auf den restlichen Seiten finden Sie verschiedene Optionen, die von dem Ziel abhängig sind, das Sie hier auswählen.

![Ziel auswählen](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>Ziel auswählen
 **Ziel**  
 Geben Sie das Ziel durch Auswählen eines Datenanbieters an, der Daten in das Ziel importieren kann.
 
-   **In der Regel können Sie anhand des jeweiligen Namens erkennen, welchen Datenanbieter Sie benötigen**, da der Name des Anbieters für gewöhnlich den Namen des Ziels enthält, z.B. *Flatfile*-Ziel, Microsoft *Excel*, Microsoft *Access*, .NET Framework-Datenanbieter für *SQL Server* und .NET Framework-Datenanbieter für *Oracle*.

-   **Wenn Sie beispielsweise über einen ODBC-Treiber für Ihr Ziel verfügen**, wählen Sie den .NET Framework-Datenanbieter für ODBC aus. Geben Sie dann die für den Treiber spezifischen Informationen ein. ODBC-Treiber werden in der Dropdownliste der Ziele nicht aufgeführt. Der .NET Framework-Datenanbieter für ODBC fungiert als Wrapper für den ODBC-Treiber. Weitere Informationen finden Sie unter [Connect to an ODBC Data Source (SQL Server Import and Export Wizard)](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit einer ODBC-Datenquelle [SQL Server-Import/Export-Assistent]).

-   **Möglicherweise sind für das Ziel mehrere Anbieter verfügbar.** In der Regel können Sie alle Anbieter auswählen, die für Ihr Ziel verwendet werden können. Sie können z.B. den .NET Framework-Datenanbieter für SQL Server oder den SQL Server-ODBC-Treiber verwenden, um eine Verbindung mit Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herzustellen. (Andere Anbieter werden zwar noch in der Liste aufgeführt, aber nicht mehr unterstützt.) 

## <a name="my-destination-isnt-in-the-list"></a>Mein Ziel ist nicht in der Liste.
-   **Sie müssen möglicherweise den Datenanbieter** von Microsoft oder einem Drittanbieter herunterladen. Die Liste der verfügbaren Anbieter in der Liste **Ziel** beinhaltet nur die auf Ihrem Computer installierten Anbieter. Weitere Informationen zu Datenzielen, die Sie verwenden können, finden Sie unter [What data sources and destinations can I use?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources) (Welche Datenquellen und -ziele kann ich verwenden?).

-   **Ist ein ODBC-Treiber für das Ziel installiert?** ODBC-Treiber werden in der Dropdownliste der Ziele nicht aufgeführt. Wenn Sie beispielsweise über einen ODBC-Treiber für Ihr Ziel verfügen, wählen Sie den .NET Framework-Datenanbieter für ODBC aus. Geben Sie dann die für den Treiber spezifischen Informationen ein. Der .NET Framework-Datenanbieter für ODBC fungiert als Wrapper für den ODBC-Treiber. Weitere Informationen finden Sie unter [Connect to an ODBC Data Source (SQL Server Import and Export Wizard)](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit einer ODBC-Datenquelle [SQL Server-Import/Export-Assistent]).

-   **64-Bit- und 32-Bit-Anbieter.** Wenn Sie den 64-Bit-Assistenten ausführen, werden Ihnen keine Ziele angezeigt, für die nur ein 32-Bit-Anbieter installiert ist (und umgekehrt).

> [!NOTE]
> Sie müssen SQL Server installieren, um die 64-Bit-Version des SQL Server-Import/Export-Assistenten verwenden zu können. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen und installieren daher auch nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten.

## <a name="after-you-choose-a-destination"></a>Nachdem Sie ein Ziel ausgewählt haben
Nach der Auswahl eines Ziels stehen Ihnen auf der Seite **Ziel auswählen** verschiedene Optionen zur Verfügung, die vom Datenanbieter abhängig sind, den Sie auswählen.

Sehen Sie sich eine der folgenden Seiten an, um eine Verbindung mit einem häufig verwendeten Ziel herzustellen.
-   [Connect to SQL Server (Herstellen einer Verbindung mit SQL Server)](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Connect to flat files (text files)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit Flatfiles [Textdateien])
-   [Connect to Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit Excel)
-   [Connect to Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit Access)
-   [Connect with ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit ODBC)
-   [Connect to Azure Blob Storage](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit Azure Blob Storage)
-   [Connect to PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit PostgreSQL)
-   [Connect to MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit MySQL)

Weitere Informationen zum Herstellen einer Verbindung mit einem Ziel, das hier nicht aufgeführt ist, finden Sie unter [The Connection Strings Reference](https://www.connectionstrings.com/) (Referenz für Verbindungszeichenfolgen). Auf dieser Website eines Drittanbieters sind Beispielverbindungszeichenfolgen aufgelistet, und es werden Angaben zu Datenanbietern und den erforderlichen Verbindungsinformationen bereitgestellt.

## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie Informationen zum Ziel Ihrer Daten und darüber, wie Sie eine Verbindung mit ihnen herstellen, bereitgestellt haben, rufen Sie die Seite **Tabelle kopieren oder Datenbank abfragen (SQL Server-Import/Export-Assistent)**auf. Auf dieser Seite geben Sie an, ob eine gesamte Tabelle oder nur bestimmte Zeilen kopiert werden sollen. Weitere Informationen finden Sie unter [Tabelle kopieren oder Datenbank abfragen (SQL Server-Import/Export-Assistent)](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Siehe auch
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


