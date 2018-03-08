---
title: Herstellen einer Verbindung mit einer Excel-Datenquelle (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
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
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 16ace15a73d9ef727612c59f8c9329a4d4437312
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer Excel-Datenquelle (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **Microsoft Excel**-Datenquelle über die Seiten **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen.

Der folgende Screenshot zeigt eine Beispielverbindung mit einer Microsoft Excel-Arbeitsmappe.

![Excel-Verbindung](../../integration-services/import-export-data/media/excel-connection.png) 

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
Wählen Sie die Excel-Version aus, die von der Quellarbeitsmappe verwendet wird.

> [!IMPORTANT]
> Sie müssen möglicherweise zusätzliche Dateien herunterladen und installieren, um eine Verbindung mit Excel-Dateien herzustellen. Weitere Informationen finden Sie im Abschnitt [Herunterladen von Dateien zum Herstellen einer Verbindung mit Excel](#officeDownloads) weiter unten auf dieser Seite.

**Erste Zeile enthält Spaltennamen**  
Geben Sie an, ob die erste Datenzeile Spaltennamen enthält.
-   Wenn die Daten keine Spaltennamen enthalten, Sie diese Option jedoch aktivieren, behandelt der Assistent die erste Zeile der Quelldaten wie Spaltennamen.
-   Wenn die Daten Spaltennamen enthalten, Sie diese Option jedoch deaktivieren, behandelt der Assistent die Zeile mit den Spaltennamen als erste Datenzeile.

Wenn Sie festlegen, dass die Daten keine Spaltennamen enthalten, verwendet der Assistent F1, F2 usw. als Spaltenüberschriften.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Excel wird in der Liste der Datenquellen nicht angezeigt
Wenn Excel nicht in der Liste der Datenquellen angezeigt wird, sollten Sie überprüfen, ob Sie die 64-Bit-Version des Assistenten verwenden. Die Anbieter für Excel und Access sind in der Regel 32-Bit-Versionen und werden in der 64-Bit-Version des Assistenten nicht angezeigt. Führen Sie stattdessen die 32-Bit-Version des Assistenten aus.

> [!NOTE]
> Sie müssen SQL Server installieren, um die 64-Bit-Version des SQL Server-Import/Export-Assistenten verwenden zu können. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen und installieren daher auch nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten.

## <a name="officeDownloads"></a>Herunterladen von Dateien zum Herstellen einer Verbindung mit Excel  
Sie müssen möglicherweise die Konnektivitätskomponenten für Microsoft Office-Datenquellen (einschließlich Excel und Access) herunterladen, wenn diese nicht bereits installiert sind. Die neueste Version der Konnektivitätskomponenten für Excel- und Access-Dateien steht unter [Microsoft Access Database Engine 2016 Redistributable (Microsoft Access Database Engine 2016 – Weitervertreibbare Komponente)](https://www.microsoft.com/download/details.aspx?id=54920) zum Download bereit.
  
Die aktuelle Version der Komponenten dient zum Öffnen von Dateien, die in früheren Versionen von Excel erstellt wurden.

Wenn der Computer über eine 32-Bit-Version von Office verfügt, müssen Sie die 32-Bit-Version der Komponenten installieren. Sie müssen zudem sicherstellen, dass Sie das Paket im 32-Bit-Modus ausführen.

Wenn Sie über ein Office 365-Abonnement verfügen, stellen Sie sicher, dass Sie die weitervertreibbare Komponente von Access Database Engine 2016 und nicht Microsoft Access 2016 Runtime herunterladen. Wenn Sie das Installationsprogramm ausführen, wird möglicherweise eine Fehlermeldung angezeigt, dass Sie den Download nicht parallel mit Klick-und-Los-Komponenten von Office installieren können. Führen Sie die Installation zur Umgehung dieser Fehlermeldung im stillen Modus durch, indem Sie ein Eingabeaufforderungsfenster öffnen und die EXE-Datei, die Sie heruntergeladen haben, mit der Befehlszeilenoption `/quiet` ausführen. Zum Beispiel:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>Siehe auch
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

