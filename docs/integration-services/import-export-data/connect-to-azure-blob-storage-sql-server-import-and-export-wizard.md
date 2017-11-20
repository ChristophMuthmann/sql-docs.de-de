---
title: Herstellen einer Verbindung mit Azure-Blob-Speicher (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 02/17/2017
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
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 36b992b5141799d4e168b2e990643e6a515a8d69
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit Azure-Blob-Speicher (SQL Server-Import / Export-Assistent)
Dieses Thema veranschaulicht das Herstellen von Verbindungen ein **Azure Blob-Speicher** Datenquelle aus der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf der Seite der SQL Server-Import / Export-Assistenten.

>   [!NOTE]
> Um die Azure-Blob-Quelle oder das Ziel zu verwenden, müssen Sie das Azure Feature Pack für SQL Server Integration Services zu installieren.
> - Um das Feature Pack herunterladen zu können, finden Sie unter [Microsoft SQL Server 2016 Integration Services Feature Pack für Azure](https://www.microsoft.com/download/details.aspx?id=49492).
>
> - Weitere Informationen finden Sie unter [Azure Feature Pack für Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Der folgende Screenshot zeigt die Optionen für eine Verbindung mit Azure-Blob-Speicher konfigurieren.

![Azure Blob Storage-Verbindung](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>Optionen zum Festlegen

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter werden die gleichen Azure-Blob-Speicher Ihrer Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

 **Azure-Konto verwenden**  
 Geben Sie an, ob ein Onlinekonto verwendet werden soll.
  
 **Speicherkontoname**  
 Geben Sie den Namen des Azure Storage-Kontos ein.  
  
**Kontoschlüssel**  
Geben Sie den Schlüssel für das Azure-Speicherkonto an.  
  
 **HTTPS verwenden**  
 Geben Sie an, ob die Verbindung mit dem Speicherkonto über HTTP oder HTTPS hergestellt werden soll.  
  
 **Lokales Entwicklerkonto verwenden**  
 Geben Sie an, ob der Speicheremulator auf dem lokalen Computer verwendet werden soll.  
  
 **Blob-Containername**  
 Treffen Sie eine Auswahl aus der Liste der im angegebenen Speicherkonto verfügbaren Speichercontainer.  
  
 **Blob-Dateiformat**  
 Wählen Sie das Dateiformat „Text“ oder „Avro“ aus.  
  
 **Spaltentrennzeichen**  
 Wenn Sie Text-Format ausgewählt haben, geben Sie das Spaltentrennzeichen.  
  
 **Erste Zeile als Spaltennamen verwenden**  
 Geben Sie an, ob die erste Zeile der Daten Spaltennamen enthält.  

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


