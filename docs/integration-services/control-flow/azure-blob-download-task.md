---
title: Azure-BLOB-Download-Task | Microsoft Docs
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
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 95ea7de4600551cc994e82dd3408cb4ea608685c
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-download-task"></a>Azure Blob-Download-Task
Der Azure Blob-Download-Task ermöglicht einem SSIS-Paket das Herunterladen von Dateien aus einem Azure-Blob-Speicher.

Um einen **Azure Blob-Download-Task**hinzuzufügen, legen Sie ihn mittels Drag &amp; Drop auf dem SSIS-Designer ab, und doppelklicken Sie darauf, oder klicken Sie mit der rechten Maustaste, und klicken Sie dann auf **Bearbeiten** , um das folgende Dialogfeld **Azure Blob-Download-Task-Editor** anzuzeigen.  
  
 Die **Azure Blob-Download-Task** ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
 Die folgende Tabelle enthält Beschreibungen für die Felder in diesem Dialogfeld.  
  
|||  
|-|-|  
|**Feld**|**Description**|  
|AzureStorageConnection|Geben Sie einen vorhandenen Azure Storage-Verbindungs-Manager an, oder erstellen Sie einen neuen, der sich auf ein Azure-Speicherkonto bezieht, das auf den Speicherort der Blob-Dateien verweist.|  
|BlobContainer|Gibt den Namen des Blob-Containers an, der die herunterzuladenden Blob-Dateien enthält.|  
|BlobDirectory|Gibt das Blob-Verzeichnis an, das die herunterzuladenden Blob-Dateien enthält. Das Blob-Verzeichnis ist eine virtuelle hierarchische Struktur.|  
|LocalDirectory|Gibt das lokale Verzeichnis, in dem die heruntergeladenen Blob-Dateien gespeichert sind.|  
|FileName|Legt einen Namensfilter an, um Dateien mit dem angegebenen Namensmuster auszuwählen. Beispielsweise `MySheet*.xls\*` enthält Dateien, wie z. B. `MySheet001.xls` und `MySheetABC.xlsx`.|  
|TimeRangeFrom/TimeRangeTo|Legt einen Filter für den Zeitbereich fest. Dateien nach der geänderte **TimeRangeFrom** und vor dem **TimeRangeTo** enthalten sind.|  
  
  

