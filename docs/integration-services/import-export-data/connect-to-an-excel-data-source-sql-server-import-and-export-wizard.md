---
title: Herstellen einer Verbindung mit einer Excel-Datenquelle (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: b4411fdd2337d93f15b149febf845fb7b0762c40
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer Excel-Datenquelle (SQL Server-Import / Export-Assistent)
Dieses Thema veranschaulicht das Herstellen von Verbindungen ein **Microsoft Excel** Datenquelle aus der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf der Seite der SQL Server-Import / Export-Assistenten.

Der folgende Screenshot zeigt eine Beispielverbindung mit einer Microsoft Excel-Arbeitsmappe.

![Excel-Verbindung](../../integration-services/import-export-data/media/excel-connection.png) 

## <a name="options-to-specify"></a>Optionen zum Festlegen

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter sind identisch, ob Excel Ihrer Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

**Excel-Dateipfad**  
 Geben Sie den Pfad und Namen für die Excel-Datei. Beispiel:
-   Für eine Datei auf dem lokalen Computer **"c:"\\MyData.xlsx**.
-   Für eine Datei auf einer Netzwerkfreigabe  **\\ \\Sales\\Datenbank\\Northwind.xlsx**.

Oder klicken Sie auf **Durchsuchen**.  
  
 **Durchsuchen**  
 Suchen Sie die Kalkulationstabelle mithilfe des Dialogfelds **Öffnen**.  

> [!NOTE]
> Der Assistent kann keine kennwortgeschützte Excel-Datei öffnen.

 **Excel-Version**  
Wählen Sie die Excel-Version aus, die von der Quellarbeitsmappe verwendet wird.

> [!IMPORTANT]
> Sie müssen möglicherweise zusätzliche Dateien zur Verbindung mit Excel-Dateien herunterladen und installieren. Finden Sie unter [erhalten Sie die Dateien müssen Sie die Verbindung mit Excel](#officeDownloads) auf dieser Seite finden Sie weitere Informationen.

**Erste Zeile enthält Spaltennamen**  
Geben Sie an, ob die erste Zeile der Daten Spaltennamen enthält.
-   Wenn die Daten keine Spaltennamen enthalten, aber Sie diese Option aktivieren, behandelt der Assistent die erste Zeile der Quelldaten wie die Spaltennamen an.
-   Wenn die Daten Spaltennamen enthält, aber Sie diese Option deaktivieren, behandelt der Assistent die Datenzeile Spaltennamen als erste Zeile der Daten.

Wenn Sie angeben, dass die Daten Spaltennamen aufweist, verwendet der Assistent F1, F2 usw., als Spaltenüberschriften.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Ich nicht Excel in der Liste der Datenquellen angezeigt.
Wenn Excel nicht in der Liste der Datenquellen angezeigt wird, werden Sie auf die 64-Bit-Assistent ausgeführt? Die Anbieter für Excel und Access sind in der Regel 32-Bit- und nicht in der 64-Bit-Assistent angezeigt. Führen Sie stattdessen den 32-Bit-Assistenten.

> [!NOTE]
> Um die 64-Bit-Version von den SQL Server-Import / Export-Assistenten verwenden zu können, müssen Sie SQL Server installieren. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen, und nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten installieren.

## <a name="officeDownloads"></a>Erhalten Sie die Verbindung mit Excel benötigten Dateien  
Sie müssen möglicherweise herunterladen die Konnektivitätskomponenten für Microsoft Office-Datenquellen, einschließlich Excel- und Access, sofern diese nicht bereits installiert sind. Die neueste Version der datenkonnektivitätskomponenten für Excel- und Access-Dateien hier herunterladen: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
Die neueste Version der Komponenten kann von früheren Versionen von Excel erstellte Dateien öffnen.

Verfügt der Computer eine 32-Bit-Version von Office, dann müssen Sie die 32-Bit-Version der Komponenten zu installieren, und außerdem müssen Sie sicherstellen, dass Sie das Paket im 32-Bit-Modus ausführen.

Wenn Sie ein Office 365-Abonnement verfügen, stellen Sie sicher, dass Sie Access-Datenbank-Engine 2016 Redistributable und nicht die Microsoft Access 2016 Runtime herunterladen. Wenn Sie das Installationsprogramm ausführen, sehen Sie eine Fehlermeldung angezeigt, dass Sie die Download-Seite-an-Seite mit den Office-Klick-und-Los-Komponenten installieren können. Um diese Fehlermeldung umgehen, führen Sie die Installation im stillen Modus, indem Sie ein Eingabeaufforderungsfenster öffnen und Ausführen der. EXE-Datei, die Sie heruntergeladen, mit der `/quiet` wechseln. Beispiel:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


