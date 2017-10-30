---
title: "Wählen Sie ein Ziel (SQL Server-Import / Export-Assistent) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 4ff3c7c8413bd6b535e1c5f95e2a7b06b397c053
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Ziel auswählen (SQL Server-Import/Export-Assistent)
 Nachdem Sie Informationen zur Quelle Ihrer Daten bereitgestellt haben und darüber, wie Sie eine Verbindung mit ihnen herstellen, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent **Ziel auswählen**an. Auf dieser Seite geben Sie Informationen zum Ziel für Ihre Daten an und dazu, wie Sie eine Verbindung damit herstellen.
  
Weitere Informationen zu Datenzielen, die Sie verwenden können, finden Sie unter [Welche Datenquellen und Ziele kann ich verwenden?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources). 

## <a name="screen-shot-of-the-destination-page"></a>Screenshot der Zielseite
Der folgende Screenshot zeigt den ersten Teil der Seite **Ziel auswählen** des Assistenten an. Der Rest der Seite verfügt über eine Variable Anzahl von Optionen, die das Ziel abhängig, die Sie hier auswählen.

![Ziel auswählen](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>Ziel auswählen
 **Ziel**  
 Geben Sie das Ziel durch Auswählen eines Datenanbieters an, der Daten in das Ziel importieren kann.
 
-   **Der Datenanbieter, die Sie benötigen ist in der Regel aus dem Namen offensichtlich**, da der Name des Anbieters in der Regel der Name des Ziel - z. B. enthält *Flatfile* Ziel, Microsoft *Excel*, Microsoft *Zugriff*, .net Framework-Datenanbieter für *SqlServer*, .net Framework-Datenanbieter für *Oracle*.

-   **Wenn Sie einen ODBC-Treiber für Ihr Ziel haben**, wählen Sie die .net Framework-Datenanbieter für ODBC. Geben Sie dann die treiberspezifische Informationen. ODBC-Treiber sind nicht in der Dropdown-Liste der Ziele aufgeführt. .Net fungiert Framework-Datenanbieter für ODBC als Wrapper um die ODBC-Treiber. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Möglicherweise sind für das Ziel mehrere Anbieter verfügbar.** In der Regel können Sie alle Anbieter auswählen, die für Ihr Ziel verwendet werden können. Angenommen, für die Verbindung an Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], können Sie die .NET Framework-Datenanbieter für SQL Server oder SQL Server-ODBC-Treiber verwenden. (Anderer Anbieter werden auch weiterhin in der Liste aber werden nicht mehr unterstützt.) 

## <a name="my-destination-isnt-in-the-list"></a>Mein Ziel nicht in der Liste
-   **Möglicherweise müssen Sie den Datenanbieter herunterladen** von Microsoft oder von einem Drittanbieter. Die Liste der verfügbaren Datenanbieter in der **Ziel** Liste enthält nur die Anbieter, die auf Ihrem Computer installiert. Weitere Informationen über die Ziele, die Sie verwenden können, finden Sie unter [welche Datenquellen und Ziele kann ich verwenden?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **Haben Sie einen ODBC-Treiber für Ihr Ziel?** ODBC-Treiber sind nicht in der Dropdown-Liste der Ziele aufgeführt. Wenn Sie einen ODBC-Treiber für Ihr Ziel haben, wählen Sie die .net Framework-Datenanbieter für ODBC. Geben Sie dann die treiberspezifische Informationen. .Net fungiert Framework-Datenanbieter für ODBC als Wrapper um die ODBC-Treiber. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **64-Bit- und 32-Bit-Anbieter.** Wenn Sie die 64-Bit-Assistenten ausführen, werden Sie nicht angezeigt Ziele für den nur ein 32-Bit-Anbieter installiert ist (und umgekehrt).

> [!NOTE]
> Um die 64-Bit-Version von den SQL Server-Import / Export-Assistenten verwenden zu können, müssen Sie SQL Server installieren. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen, und nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten installieren.

## <a name="after-you-choose-a-destination"></a>Nachdem Sie ein Ziel ausgewählt haben
Nachdem Sie ein Ziel, das restliche ausgewählt der **wählen Sie ein Ziel** weist auf eine Variable Anzahl von Optionen, die von den Datenanbieter abhängen, die Sie auswählen.

Zur Verbindung mit einer häufig verwendeten Ziel finden Sie in den folgenden Seiten.
-   [Herstellen einer Verbindung mit SQLServer](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Flatfile-Dateien (Textdateien)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Azure-Blob-Speicher](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Weitere Informationen dazu, wie Sie mit einem Ziel verbinden, die hier nicht aufgeführt ist, finden Sie unter [der Zeichenfolgen-Verbindungsverweis](https://www.connectionstrings.com/). Diese Site eines Drittanbieters enthält Beispiele für Verbindungszeichenfolgen und Weitere Informationen zu Datenanbietern und die Verbindungsinformationen, die sie benötigen.

## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie Informationen zum Ziel Ihrer Daten und darüber, wie Sie eine Verbindung mit ihnen herstellen, bereitgestellt haben, rufen Sie die Seite **Tabelle kopieren oder Datenbank abfragen (SQL Server-Import/Export-Assistent)**auf. Auf dieser Seite geben Sie an, ob eine gesamte Tabelle oder nur bestimmte Zeilen kopiert werden sollen. Weitere Informationen finden Sie unter [Tabelle kopieren oder Datenbank abfragen (SQL Server-Import/Export-Assistent)](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Siehe auch
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



