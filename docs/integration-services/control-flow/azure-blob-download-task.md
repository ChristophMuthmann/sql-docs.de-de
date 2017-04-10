---
title: "Azure Blob-Download-Task | Microsoft Docs"
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
  - "sql13.dts.designer.afpblobdltask.f1"
  - "sql14.dts.designer.afpblobdltask.f1"
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# Azure Blob-Download-Task
  Der Azure Blob-Download-Task ermöglicht einem SSIS-Paket das Herunterladen von Dateien aus einem Azure-Blob-Speicher.

>   [!NOTE] Um sicherzustellen, dass der Azure Storage-Verbindungs-Manager und die Komponenten, die ihn verwenden – Blobquelle, Blobziel, Blob-Upload- und Blob-Download-Task – sowohl Verbindungen mit allgemeinen Speicherkonten als auch Blobspeicherkonten herstellen können, stellen Sie sicher, dass Sie die neueste Version von Azure Feature Pack [hier](https://www.microsoft.com/download/details.aspx?id=49492) herunterladen. Weitere Informationen über diese beiden Typen von Speicherkonten finden Sie unter [Einführung in Microsoft Azure Storage](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts).
   
Um einen **Azure Blob-Download-Task** hinzuzufügen, legen Sie ihn mittels Drag & Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Bearbeiten**, um das folgende Dialogfeld **Azure Blob-Download-Task-Editor** anzuzeigen.  
  
 Der **Azure Blob-Download-Task** ist eine Komponente des SQL Server Integration Services (SSIS) Feature Pack für Azure für SQL Server 2016. Laden Sie das Feature Pack [hier](http://go.microsoft.com/fwlink/?LinkID=626967) herunter.  
  
 Die folgende Tabelle enthält Beschreibungen für die Felder in diesem Dialogfeld.  
  
|||  
|-|-|  
|**Feld**|**Description**|  
|AzureStorageConnection|Geben Sie einen vorhandenen Azure Storage-Verbindungs-Manager an, oder erstellen Sie einen neuen, der sich auf ein Azure-Speicherkonto bezieht, das auf den Speicherort der Blob-Dateien verweist.|  
|BlobContainer|Gibt den Namen des Blob-Containers an, der die herunterzuladenden Blob-Dateien enthält.|  
|BlobDirectory|Gibt das Blob-Verzeichnis an, das die herunterzuladenden Blob-Dateien enthält. Das Blob-Verzeichnis ist eine virtuelle hierarchische Struktur.|  
|LocalDirectory|Gibt das lokale Verzeichnis an, in dem die heruntergeladenen Blob-Dateien gespeichert werden sollen.|  
|FileName|Legt einen Namensfilter an, um Dateien mit dem angegebenen Namensmuster auszuwählen. Beispiel: „MeinArbeitsblatt*.xls\*“ schließt „MeinArbeitsblatt001.xls“ und „MeinArbeitsblattABC.xlsx“ ein.|  
|TimeRangeFrom/TimeRangeTo|Legt einen Filter für den Zeitbereich fest. Dateien, die nach **TimeRangeFrom** und vor **TimeRangeTo** geändert wurden, sind eingeschlossen.|  
  
  