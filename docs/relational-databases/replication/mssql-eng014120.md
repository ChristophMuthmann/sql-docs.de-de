---
title: MSSQL_ENG014120 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014120 error
ms.assetid: 6b169a3b-30da-4981-b998-b52d61811572
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10c1c6aa01f9cc45a7e80e81b69e0212bc13fe2f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqleng014120"></a>MSSQL_ENG014120
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|14120|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Die %1!s!-Verteilungsdatenbank konnte nicht gelöscht werden. Diese Verteilerdatenbank ist einem Verleger zugeordnet.|  
  
## <a name="explanation"></a>Erklärung  
 In der Verteilungsdatenbank werden Metadaten und Verlaufsdaten für alle Replikations- und Transaktionstypen für die Transaktionsreplikation gespeichert. Dieser Fehler tritt bei dem Versuch auf, eine Verteilungsdatenbank zu löschen, die einem oder mehreren Verleger(n) zugeordnet ist.  
  
## <a name="user-action"></a>Benutzeraktion  
 Um eine Verteilungsdatenbank löschen zu können, müssen Sie zuerst die Zuordnung zwischen dem Verteiler und dem Verleger löschen. Weitere Informationen finden Sie unter [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Verteilung konfigurieren](../../relational-databases/replication/configure-distribution.md)  
  
  
