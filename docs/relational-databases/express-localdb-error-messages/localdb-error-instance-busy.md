---
title: LOCALDB_ERROR_INSTANCE_BUSY | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0ed9d0f8-3297-4e31-a3e9-4a827f381789
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 62d17b4a24969a40b5fc9ecb142879cebf3a9e94
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
  
