---
title: Azure Blob Upload-Task | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpblobuptask.f1
- sql14.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cec51398ac521abc0345e90b3c6ed156b542b5f1
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-upload-task"></a>Azure-Blob-Uploadtask
Der **Azure-Blob-Uploadtask** ermöglicht einem SSIS-Paket das Hochladen von Dateien in einen Azure-Blobspeicher.
    
Um einen **Azure-Blob-Uploadtask**hinzuzufügen, legen Sie ihn mittels Drag &amp; Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie anschließend auf **Bearbeiten** , um das folgende Dialogfeld **Azure-Blob-Uploadtask-Editor** anzuzeigen.  
  
 Die **Azure Blob-Uploadtask** ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 Die folgende Tabelle enthält Beschreibungen für die Felder in diesem Dialogfeld.  
  
|||  
|-|-|  
|**Feld**|**Description**|  
|AzureStorageConnection|Geben Sie einen vorhandenen Azure Storage-Verbindungs-Manager an, oder erstellen Sie einen neuen, der sich auf ein Azure-Speicherkonto bezieht, das auf den Speicherort der Blob-Dateien verweist.|  
|BlobContainer|Gibt den Namen des Blob-Containers, der hochgeladenen Dateien als Blobs enthält.|  
|BlobDirectory|Gibt das Blob-Verzeichnis, in dem die hochgeladene Datei als ein Block-Blob gespeichert wird. Das Blob-Verzeichnis ist eine virtuelle hierarchische Struktur. Wenn das Blob bereits vorhanden ist, wird es ersetzt.|  
|LocalDirectory|Geben Sie das lokale Verzeichnis mit den Dateien an, die hochgeladen werden sollen.|  
|FileName|Legt einen Namensfilter an, um Dateien mit dem angegebenen Namensmuster auszuwählen. Beispielsweise `MySheet*.xls\*` enthält Dateien, wie z. B. `MySheet001.xls` und `MySheetABC.xlsx`.|  
|TimeRangeFrom/TimeRangeTo|Legt einen Filter für den Zeitbereich fest. Dateien nach der geänderte **TimeRangeFrom** und vor dem **TimeRangeTo** enthalten sind.|  
  
  

