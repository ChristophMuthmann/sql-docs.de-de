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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d744e84aa2b4ae0462a5d5a1e4453a9e86abb890
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

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
> Sie müssen möglicherweise zusätzliche Dateien herunterladen und installieren, um eine Verbindung mit der Excel-Version herzustellen, die Sie auswählen. Finden Sie unter [erhalten Sie die Dateien müssen Sie die Verbindung mit Excel](#officeDownloads) auf dieser Seite finden Sie weitere Informationen.

Wenn Sie ein Problem bei der Angabe einer Version haben, geben Sie eine andere Version, auch eine frühere Version. Beispielsweise können Sie nicht in der Lage, Office 2016-Datenanbieter installiert werden, da Sie ein Microsoft Office 365-Abonnement besitzen. Sie können den Datenanbieter für Excel 2016 und Zugriff 2016 nur mit einer desktop-Version von Microsoft Office installieren. In diesem Fall können Sie Excel 2013 anstatt Excel 2016 angeben. Die beiden Versionen des Anbieters sind funktional äquivalent. Diese Einschränkung von der Laufzeit Office 2016 gemäß [diesem Blogbeitrag](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/).

**Erste Zeile enthält Spaltennamen**  
Geben Sie an, ob die erste Zeile der Daten Spaltennamen enthält.
-   Wenn die Daten keine Spaltennamen enthalten, aber Sie diese Option aktivieren, behandelt der Assistent die erste Zeile der Quelldaten wie die Spaltennamen an.
-   Wenn die Daten Spaltennamen enthält, aber Sie diese Option deaktivieren, behandelt der Assistent die Datenzeile Spaltennamen als erste Zeile der Daten.

Wenn Sie angeben, dass die Daten Spaltennamen aufweist, verwendet der Assistent F1, F2 usw., als Spaltenüberschriften.

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>Ich nicht Excel in der Liste der Datenquellen angezeigt.
Wenn Excel nicht in der Liste der Datenquellen angezeigt wird, werden Sie auf die 64-Bit-Assistent ausgeführt? Die Anbieter für Excel und Access sind in der Regel 32-Bit- und nicht in der 64-Bit-Assistent angezeigt. Führen Sie stattdessen den 32-Bit-Assistenten.

## <a name="officeDownloads"></a>Erhalten Sie die Verbindung mit Excel benötigten Dateien  
Sie müssen möglicherweise herunterladen die Konnektivitätskomponenten für Microsoft Office-Datenquellen, einschließlich Excel- und Access, sofern diese nicht bereits installiert sind.

Spätere Versionen der Komponenten dienen zum Öffnen von Dateien, die in früheren Versionen der Programme erstellt wurden. Spätere Versionen der Komponenten dienen zum Öffnen von Dateien, die in früheren Versionen der Programme erstellt wurden. Z. B. Wenn Sie die Office 2016-Komponenten installieren können, verwenden Sie die Office 2013-Komponenten stattdessen. Die beiden Versionen des Anbieters sind funktional äquivalent. Diese Einschränkung von der Laufzeit Office 2016 gemäß [diesem Blogbeitrag](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/).

Wenn der Computer eine 32-Bit-Version von Office hat-dies normal, selbst auf 64-Bit-Computer ist – müssen Sie die 32-Bit-Version der Komponenten zu installieren. Sie müssen auch sicherstellen, dass Sie den 32-Bit-Assistenten ausführen, oder führen Sie das SQL Server Integration Services-Paket, das der Assistent im 32-Bit-Modus erstellt. 
 
|Microsoft Office-Version|Herunterladen|  
|------------------------------|--------------|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2007|[2007 Office System-Treiber: Datenkonnektivitätskomponenten](https://www.microsoft.com/download/details.aspx?id=23734)|  

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


