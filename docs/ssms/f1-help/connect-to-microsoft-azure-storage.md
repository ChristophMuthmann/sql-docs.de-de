---
title: Mit Microsoft Azure Storage verbinden | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: 
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: ea0fbb6f0297dfdbe94974de472c7a48ce8ce831
ms.openlocfilehash: b673559a735d3b28d6055a1440183861b3db692a
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="connect-to-microsoft-azure-storage"></a>Mit Microsoft Azure Storage verbinden
Verwenden Sie das Dialogfeld **Windows Azure Storage-Verbindung** , um ein Speicherkonto anzugeben und die Verbindung mit Windows Azure zu überprüfen.  
  
## <a name="options"></a>enthalten  
Geben Sie die folgenden Informationen zum Windows Azure-Konto an, und klicken Sie dann auf **Weiter** , um fortzufahren.  
  
1.  **Speicherkonto** – Geben Sie den Speicherkontonamen an.

   >[!NOTE]
   > Sie können nur Verbindungen zu [allgemeinen Speicherkonten](https://docs.microsoft.com/en-us/azure/storage/storage-introduction#introducing-the-azure-storage-services) herstellen. Die Verbindungserstellung zu anderen Arten von Speicherkonten kann zu einem Fehler wie dem folgenden führen:
   >
   >  The value for one of the HTTP headers is not in the correct format. (Das Format von einem der Werte des HTTP-Headers ist nicht korrekt.) (Microsoft.SqlServer.StorageClient).
   >
   >  The remote server returned an error: (400) Bad Request. (Der Remoteserver hat einen Fehler zurückgegeben: (400) Ungültige Anforderung.) (System)

2.  **Kontoschlüssel** – Geben Sie den Kontoschlüssel für das angegebene Speicherkonto an.  
  
3.  **Sichere Endpunkte verwenden (HTTPS)** – Bei Aktivierung dieser Option wird die Kommunikation verschlüsselt, und für Netzwerkwebserver wird eine sichere Identifikation verwendet.  
  
4.  **Kontoschlüssel speichern** – Bei Aktivierung dieser Option wird das Kennwort in einer verschlüsselten Datei gespeichert.  
  

