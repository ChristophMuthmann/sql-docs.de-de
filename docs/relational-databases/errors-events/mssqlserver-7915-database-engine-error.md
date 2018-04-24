---
title: MSSQLSERVER_7915 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5fb0a4415f7645bfb1d1bd93f525b9582738079e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|7915|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|Meldungstext|Reparaturvorgang: Die IAM-Kette für Objekt-ID O_ID, Index-ID I_ID, Partitions-ID PN_ID, Zuordnungseinheits-ID A_ID (Typ TYPE), wurde vor Seite P_ID abgeschnitten und wird neu erstellt.|  
  
## <a name="explanation"></a>Erklärung  
Dies ist eine Informationsmeldung, die von REPAIR gesendet wurde und anzeigt, dass die angegebene IAM-Kette (Index Allocation Map) gepatcht wurde, damit sie neu erstellt werden konnte. Für diesen Patch war möglicherweise die Zuordnung eines neuen Kopfteils der IAM-Kette oder die Entfernung von fehlerhaften Seiten aus der Kette erforderlich.  
  
## <a name="user-action"></a>Benutzeraktion  
InclusionThresholdSetting  
  
