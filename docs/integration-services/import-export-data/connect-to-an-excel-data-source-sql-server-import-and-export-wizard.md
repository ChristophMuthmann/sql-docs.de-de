---
title: Herstellen einer Verbindung mit einer Excel-Datenquelle (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 42af9f992c293f9872080a69cf6a7a4890ff205f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer Excel-Datenquelle (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **Microsoft Excel**-Datenquelle über die Seiten **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen.

Der folgende Screenshot zeigt eine Beispielverbindung mit einer Microsoft Excel-Arbeitsmappe.

![Excel-Verbindung](../../integration-services/import-export-data/media/excel-connection.png) 

Sie müssen möglicherweise zusätzliche Dateien herunterladen und installieren, um eine Verbindung mit Excel-Dateien herzustellen. Weitere Informationen finden Sie unter [Get the files you need to connect to Excel (Herunterladen von Dateien zum Herstellen einer Verbindung mit Excel)](../load-data-to-from-excel-with-ssis.md#get-the-files-you-need-to-connect-to-excel).

> [!IMPORTANT]
> Ausführliche Informationen über das Herstellen einer Verbindung mit Excel-Dateien sowie Einschränkungen und bekannte Probleme beim Laden von Daten aus oder in Excel-Dateien finden Sie unter [Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md).

## <a name="options-to-specify"></a>Anzugebende Optionen

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter bleiben stets unverändert – egal, ob Excel die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

**Excel-Dateipfad**  
 Geben Sie den Pfad und den Dateinamen für die Excel-Datei an. Zum Beispiel:
-   Für eine Datei auf dem lokalen Computer können Sie beispielsweise **C:\\MeineDaten.xlsx** festlegen.
-   Für eine Datei auf einer Netzwerkfreigabe können Sie beispielsweise **\\\\Verkauf\\Datenbank\\Northwind.xlsx** festlegen.

Oder klicken Sie auf **Durchsuchen**.  
  
 **Durchsuchen**  
 Suchen Sie die Kalkulationstabelle mithilfe des Dialogfelds **Öffnen**.  

> [!NOTE]
> Der Assistent kann keine kennwortgeschützte Excel-Datei öffnen.

 **Excel-Version**  
Wählen Sie die Version von Excel aus, die von der Quelle oder Zielarbeitsmappe verwendet wird.

**Erste Zeile enthält Spaltennamen**  
Geben Sie an, ob die erste Datenzeile Spaltennamen enthält.
-   Wenn die Daten keine Spaltennamen enthalten, Sie diese Option jedoch aktivieren, behandelt der Assistent die erste Zeile der Quelldaten wie Spaltennamen.
-   Wenn die Daten Spaltennamen enthalten, Sie diese Option jedoch deaktivieren, behandelt der Assistent die Zeile mit den Spaltennamen als erste Datenzeile.

Wenn Sie festlegen, dass die Daten keine Spaltennamen enthalten, verwendet der Assistent F1, F2 usw. als Spaltenüberschriften.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Excel wird in der Liste der Datenquellen nicht angezeigt
Wenn Excel nicht in der Liste der Datenquellen angezeigt wird, sollten Sie überprüfen, ob Sie die 64-Bit-Version des Assistenten verwenden. Die Anbieter für Excel und Access sind in der Regel 32-Bit-Versionen und werden in der 64-Bit-Version des Assistenten nicht angezeigt. Führen Sie stattdessen die 32-Bit-Version des Assistenten aus.

> [!NOTE]
> Sie müssen SQL Server installieren, um die 64-Bit-Version des SQL Server-Import/Export-Assistenten verwenden zu können. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen und installieren daher auch nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten.

## <a name="see-also"></a>Siehe auch
[Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md)  
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

