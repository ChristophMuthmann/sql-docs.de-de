---
title: MSSQLSERVER_5515 | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 5515 (Database Engine error)
ms.assetid: ccd793bc-ba5d-4782-8d72-731fd01fc177
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: 78b87a2dea7dabd07f8a9c542c3e808511f7118b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver5515"></a>MSSQLSERVER_5515
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|MSSQLSERVER|  
|Ereignis-ID|5515|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|FS_OPEN_CONTAINER_FAILED|  
|Meldungstext|Das Containerverzeichnis ''%.*ls'' der FILESTREAM-Datei kann nicht geöffnet werden. Das Betriebssystem hat den Windows-Statuscode 0x%x zurückgegeben.|  
  
## <a name="explanation"></a>Erklärung  
Das angegebene Containerverzeichnis der FILESTREAM-Datei kann nicht geöffnet werden.  
  
## <a name="user-action"></a>Benutzeraktion  
Die Ursache des Fehlers finden Sie im angegebenen Windows-Statuscode.  
  
