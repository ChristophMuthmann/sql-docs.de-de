---
title: LOCALDB_ERROR_INSTANCE_BUSY | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 0ed9d0f8-3297-4e31-a3e9-4a827f381789
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9f94d5323f3b942baccc024fd951783b540dcd80
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="localdberrorinstancebusy"></a>LOCALDB_ERROR_INSTANCE_BUSY
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|274|  
|Ereignisquelle|Lokale SQL Server-Datenbanklaufzeit 12.0|  
|Komponente|Laufzeit-API der lokalen Datenbank|  
|Meldungstext|Der angeforderte Vorgang für die lokale Datenbankinstanz kann nicht ausgeführt werden, weil die angegebene Instanz gerade verwendet wird. Beenden Sie die Instanz, und wiederholen Sie den Vorgang.|  
  
## <a name="explanation"></a>Erklärung  
 Die angegebene Instanz wird ausgeführt.  
  
## <a name="user-action"></a>Benutzeraktion  
 Stoppen Sie die angegebene Laufzeitinstanz der lokalen Datenbank, und versuchen Sie es erneut.  
  
  
