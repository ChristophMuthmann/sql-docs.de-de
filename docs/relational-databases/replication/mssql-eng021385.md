---
title: MSSQL_ENG021385 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG021385 error
ms.assetid: a2c0444f-d97b-4760-8905-3574791c2e26
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c99c72b377f10999f55ad48a23e2b522308d0a2a
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="mssqleng021385"></a>MSSQL_ENG021385
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21385|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Der Momentaufnahmevorgang konnte die %1!s!-Veröffentlichung nicht verarbeiten. Möglicherweise ist gerade eine Schemaänderungsaktivität aktiv, oder es werden neue Artikel hinzugefügt.|  
  
## <a name="explanation"></a>Erklärung  
 Dieser Fehler wird ausgelöst, wenn die Ausführung des Momentaufnahme-Agents beginnt, während gerade Änderungen an der Veröffentlichung vorgenommen werden, z. B. Hinzufügen oder Löschen von Artikeln oder das Ausführen von Schemaänderungen an veröffentlichten Objekten.  
  
## <a name="user-action"></a>Benutzeraktion  
 Starten Sie den Momentaufnahme-Agent erneut, nachdem die Änderungen an der Veröffentlichungsdatenbank abgeschlossen sind. Weitere Informationen finden Sie unter [Starten und Beenden eines Replikations-Agents &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) und [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
