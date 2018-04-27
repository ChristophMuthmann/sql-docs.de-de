---
title: Verbinden mit Azure Blob Storage (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7287d5d1342da6c2a43e7013eae60247cf4aabaf
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>Verbinden mit Azure Blob Storage (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **Azure Blob Storage**-Datenquelle über die Seiten **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen.

>   [!NOTE]
> Um Azure-Blobquelle oder -Blobziel zu verwenden, müssen Sie das Azure Feature Pack für SQL Server Integration Services installieren.
> - Wie Sie das Feature Pack herunterladen, erfahren Sie unter [Microsoft SQL Server 2016 Integration Services Feature Pack für Azure](https://www.microsoft.com/download/details.aspx?id=49492).
>
> - Weitere Informationen finden Sie unter [Azure Feature Pack für Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Der folgende Screenshot zeigt die Optionen für die Konfiguration einer Verbindung mit Azure Blob Storage.

![Azure Blob Storage-Verbindung](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>Anzugebende Optionen

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter bleiben unabhängig davon, ob Azure Blob Storage die Quelle oder das Ziel ist, stets unverändert. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

 **Azure-Konto verwenden**  
 Geben Sie an, ob ein Onlinekonto verwendet werden soll.
  
 **Speicherkontoname**  
 Geben Sie den Namen des Azure-Speicherkontos ein.  
  
**Kontoschlüssel**  
Geben Sie den Schlüssel für das Azure-Speicherkonto ein.  
  
 **HTTPS verwenden**  
 Geben Sie an, ob die Verbindung mit dem Speicherkonto über HTTP oder HTTPS hergestellt werden soll.  
  
 **Lokales Entwicklerkonto verwenden**  
 Geben Sie an, ob der Speicheremulator auf dem lokalen Computer verwendet werden soll.  
  
 **Blob-Containername**  
 Treffen Sie eine Auswahl aus der Liste der im angegebenen Speicherkonto verfügbaren Speichercontainer.  
  
 **Blob-Dateiformat**  
 Wählen Sie das Dateiformat „Text“ oder „Avro“ aus.  
  
 **Spaltentrennzeichen**  
 Wenn Sie das Format „Text“ ausgewählt haben, geben Sie das Spaltentrennzeichen ein.  
  
 **Erste Zeile als Spaltennamen verwenden**  
 Geben Sie an, ob die erste Zeile der Daten Spaltennamen enthält.  

## <a name="see-also"></a>Siehe auch
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

