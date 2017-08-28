---
title: "Wählen Sie eine Datenquelle (SQL Server-Import / Export-Assistent) | Microsoft Docs"
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
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
caps.latest.revision: 124
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 80d35cb294fd900611c73ca37bba2a66baef0767
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>Datenquelle auswählen (SQL Server-Import/Export-Assistent)
  Nach der Begrüßungsseite zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent die Seite **Datenquelle auswählen**an. Auf dieser Seite geben Sie Informationen zur Quelle für Ihre Daten an und darüber, wie Sie eine Verbindung mit dieser herstellen.
  
Weitere Informationen zu Datenquellen, die Sie verwenden können, finden Sie unter [Welche Datenquellen und -ziele kann ich verwenden?](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>Screenshot der Seite „Datenquelle auswählen“ 
Der folgende Screenshot zeigt den oberen Teil der Seite **Datenquelle auswählen** im Assistenten, der sich nicht ändert. Der Rest der Seite verfügt über eine Variable Anzahl von Optionen, die von der Datenquelle abhängig sind, die Sie hier auswählen.

![Quelle auswählen](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>Datenquelle auswählen
 **Datenquelle**  
Geben Sie die Datenquelle an, indem Sie einen Datenanbieter auswählen, der eine Verbindung mit der Quelle herstellen kann.

-   **Der Datenanbieter, die Sie benötigen ist in der Regel aus dem Namen offensichtlich**, da der Name des Anbieters in der Regel der Name der Datenquelle - z. B. enthält *Flatfile* Quellen, Microsoft *Excel*, Microsoft *Zugriff*, .net Framework-Datenanbieter für *SqlServer*, .net Framework-Datenanbieter für *Oracle*.

-   **Wenn Sie einen ODBC-Treiber für die Datenquelle haben**, wählen Sie die .net Framework-Datenanbieter für ODBC. Geben Sie dann die treiberspezifische Informationen. ODBC-Treiber sind nicht in der Dropdown-Liste der Datenquellen aufgeführt. .Net fungiert Framework-Datenanbieter für ODBC als Wrapper um die ODBC-Treiber. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Möglicherweise sind für die Datenquelle mehrere Anbieter verfügbar.** In der Regel können Sie alle Anbieter auswählen, die für Ihre Quelle verwendet werden können. Angenommen, für die Verbindung an Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], können Sie die .NET Framework-Datenanbieter für SQL Server oder SQL Server-ODBC-Treiber verwenden. (Anderer Anbieter werden auch weiterhin in der Liste aber werden nicht mehr unterstützt.) 

## <a name="my-data-source-isnt-in-the-list"></a>Der Datenquelle nicht in der Liste
-   **Möglicherweise müssen Sie den Datenanbieter herunterladen** von Microsoft oder von einem Drittanbieter. Die Liste der verfügbaren Datenanbieter in der **Datenquelle** Liste enthält nur die Anbieter, die auf Ihrem Computer installiert. Weitere Informationen zu Datenquellen, die Sie verwenden können, finden Sie unter [Welche Datenquellen und -ziele kann ich verwenden?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **Haben Sie einen ODBC-Treiber für Ihre Datenquelle?** ODBC-Treiber sind nicht in der Dropdown-Liste der Datenquellen aufgeführt. Wenn Sie einen ODBC-Treiber für die Datenquelle haben, wählen Sie die .net Framework-Datenanbieter für ODBC. Geben Sie dann die treiberspezifische Informationen. .Net fungiert Framework-Datenanbieter für ODBC als Wrapper um die ODBC-Treiber. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit einer ODBC-Datenquelle](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **64-Bit- und 32-Bit-Anbieter.** Wenn Sie die 64-Bit-Assistenten ausführen, werden Sie nicht angezeigt Datenquellen für den nur ein 32-Bit-Anbieter installiert ist (und umgekehrt).

> [!NOTE]
> Um die 64-Bit-Version von den SQL Server-Import / Export-Assistenten verwenden zu können, müssen Sie SQL Server installieren. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen, und nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten installieren.

## <a name="after-you-choose-a-data-source"></a>Nach dem Auswählen der Datenquelle
Nach dem Auswählen einer Datenquelle, die restliche der **wählen Sie eine Datenquelle** weist auf eine Variable Anzahl von Optionen, die von den Datenanbieter abhängen, die Sie auswählen.

Zur Verbindung mit einer häufig verwendeten Datenquelle finden Sie in den folgenden Seiten.
-   [Herstellen einer Verbindung mit SQLServer](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Flatfile-Dateien (Textdateien)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit Azure-Blob-Speicher](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Herstellen einer Verbindung mit MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Informationen zum Herstellen einer Verbindung mit einer Datenquelle, die hier nicht aufgeführt ist, finden Sie unter [der Zeichenfolgen-Verbindungsverweis](https://www.connectionstrings.com/). Diese Site eines Drittanbieters enthält Beispiele für Verbindungszeichenfolgen und Weitere Informationen zu Datenanbietern und die Verbindungsinformationen, die sie benötigen.

## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie Informationen zur Quelle Ihrer Daten bereitgestellt haben und darüber, wie Sie eine Verbindung mit ihnen herstellen, wird als nächste Seite **Ziel auswählen**angezeigt. Auf dieser Seite geben Sie Informationen zum Ziel für Ihre Daten an und dazu, wie Sie eine Verbindung damit herstellen. Weitere Informationen finden Sie unter [Ziel auswählen](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).
 
## <a name="see-also"></a>Siehe auch
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



