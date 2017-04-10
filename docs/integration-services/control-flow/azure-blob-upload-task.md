---
title: "Azure-Blob-Uploadtask | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpblobuptask.f1"
  - "sql14.dts.designer.afpblobuptask.f1"
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# Azure-Blob-Uploadtask
  Der **Azure-Blob-Uploadtask** ermöglicht einem SSIS-Paket das Hochladen von Dateien in einen Azure-Blobspeicher.
  
>   [!NOTE] Laden Sie [hier](https://www.microsoft.com/download/details.aspx?id=49492) unbedingt die neueste Version des Azure Feature Pack herunter, um sicherzustellen, dass der Azure Storage-Verbindungs-Manager und die Komponenten, die ihn verwenden (Blobquelle, Blobziel, Blob-Upload- und Blob-Download-Task) sowohl Verbindungen mit allgemeinen Speicherkonten als auch Blobspeicherkonten herstellen können. Weitere Informationen zu diesen beiden Typen von Speicherkonten finden Sie unter [Einführung in Microsoft Azure Storage](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts). 
    
Um einen **Azure-Blob-Uploadtask** hinzuzufügen, legen Sie ihn mittels Drag & Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie anschließend auf **Bearbeiten**, um das folgende Dialogfeld **Azure-Blob-Uploadtask-Editor** anzuzeigen.  
  
 Der **Azure-Blob-Uploadtask** ist eine Komponente des SQL Server Integration Services Feature Pack (SSIS) für Azure für SQL Server 2016. Laden Sie das Feature Pack [hier](http://go.microsoft.com/fwlink/?LinkID=626967) herunter.  
  
 Die folgende Tabelle enthält Beschreibungen für die Felder in diesem Dialogfeld.  
  
|||  
|-|-|  
|**Feld**|**Description**|  
|AzureStorageConnection|Geben Sie einen vorhandenen Azure Storage-Verbindungs-Manager an, oder erstellen Sie einen neuen, der sich auf ein Azure-Speicherkonto bezieht, das auf den Speicherort der Blob-Dateien verweist.|  
|BlobContainer|Gibt den Namen des Blobcontainers an, in dem die hochgeladenen Dateien als Blobs enthalten sein sollen.|  
|BlobDirectory|Gibt das Blobverzeichnis an, in dem die hochgeladene Datei als Blockblob gespeichert wird. Das Blob-Verzeichnis ist eine virtuelle hierarchische Struktur. Wenn das Blob bereits vorhanden ist, wird es ersetzt.|  
|LocalDirectory|Geben Sie das lokale Verzeichnis mit den Dateien an, die hochgeladen werden sollen.|  
|FileName|Legt einen Namensfilter an, um Dateien mit dem angegebenen Namensmuster auszuwählen. Beispiel: „MeinArbeitsblatt*.xls\*“ schließt „MeinArbeitsblatt001.xls“ und „MeinArbeitsblattABC.xlsx“ ein.|  
|TimeRangeFrom/TimeRangeTo|Legt einen Filter für den Zeitbereich fest. Dateien, die nach **TimeRangeFrom** und vor **TimeRangeTo** geändert wurden, sind eingeschlossen.|  
  
  