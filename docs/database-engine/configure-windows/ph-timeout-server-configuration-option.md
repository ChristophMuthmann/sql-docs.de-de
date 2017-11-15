---
title: PH-Timeout (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: TSQL
helpviewer_keywords:
- time limit for protocol handler wait [SQL Server]
- timeout options [SQL Server], ph timeout option
- protocols [SQL Server], timing out
- ph timeout option
ms.assetid: ed19a07c-83fe-4582-9c9e-41b1ce571850
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 118ea83ca4d3268f55a6ec1e0c6db68958dad9f4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="ph-timeout-server-configuration-option"></a>PH-Timeout (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die Option „ph timeout“, um in Sekunden anzugeben, wie lange der Volltext-Protokollhandler auf eine Verbindung mit der Datenbank warten soll, bevor ein Timeout eintritt. Der Standardwert ist 60 Sekunden. Vergrößern Sie den Wert für ph timeout, wenn bei Verbindungsversuchen aufgrund von vorübergehenden Netzwerkproblemen Timeouts auftreten.  
  
 Der Volltext-Protokollhandler wird von dem Filterdämonhost gehostet und wird dazu verwendet, aus SQL Server die Daten zum Erstellen des Volltextindexes abzurufen. Weitere Informationen zu den Komponenten der Volltextsuche finden Sie unter [Volltextsuche](../../relational-databases/search/full-text-search.md).  
  
 Wenn der Protokollhandler zum Abrufen einer Datenzeile innerhalb der angegebenen Zeit keine Verbindung mit SQL Server herstellen kann, wird ein Timeoutfehler für diese Zeile gemeldet. Der Volltext-Gatherer versucht, diese Zeile zu einem späteren Zeitpunkt erneut abzurufen. Weitere Informationen zum Volltext-Gatherer finden Sie unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Volltextsuche](../../relational-databases/search/full-text-search.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
