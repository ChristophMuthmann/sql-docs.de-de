---
title: MSSQLSERVER_7915 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: b0b8d1752a64451824195426c241d19472483570
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|7915|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|Meldungstext|Reparaturvorgang: Die IAM-Kette für Objekt-ID O_ID, Index-ID I_ID, Partitions-ID PN_ID, Zuordnungseinheits-ID A_ID (Typ TYPE), wurde vor Seite P_ID abgeschnitten und wird neu erstellt.|  
  
## <a name="explanation"></a>Erklärung  
Dies ist eine Informationsmeldung, die von REPAIR gesendet wurde und anzeigt, dass die angegebene IAM-Kette (Index Allocation Map) gepatcht wurde, damit sie neu erstellt werden konnte. Für diesen Patch war möglicherweise die Zuordnung eines neuen Kopfteils der IAM-Kette oder die Entfernung von fehlerhaften Seiten aus der Kette erforderlich.  
  
## <a name="user-action"></a>Benutzeraktion  
Keine  
  
