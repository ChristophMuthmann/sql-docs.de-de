---
title: MSSQLSERVER_3437 | Microsoft-Dokumentation
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
- 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fd30098161f7bdcad7c32496e1d8d6f51f889c94
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver3437"></a>MSSQLSERVER_3437
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3437|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|NODTC|  
|Meldungstext|Fehler beim Wiederherstellen der '%.*ls'-Datenbank. Es konnte keine Verbindung mit Microsoft Distributed Transaction Coordinator (MS DTC) hergestellt werden, um den Beendigungsstatus von Transaktion %S_XID zu überprüfen. Korrigieren Sie MS DTC, und führen Sie die Wiederherstellung erneut aus.|  
  
## <a name="explanation"></a>Erklärung  
Eine oder mehrere verteilte Transaktionen, für die MS DTC ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) verwendet wurde, waren nicht abgeschlossen, als die Datenbank beendet wurde. Bei der Wiederherstellung dieser Datenbank sind Fehler aufgetreten, da in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Verbindung mit MS DTC hergestellt werden kann, um die Transaktionen abzuschließen oder einen Rollback für die Transaktionen auszuführen.  
  
## <a name="user-action"></a>Benutzeraktion  
Zum Wiederherstellen dieser Datenbank müssen Sie zunächst das Problem mit MS DTC lösen. Weitere Informationen zu diesem Problem mit MS DTC finden Sie in den Windows-Ereignisprotokollen. Wenn das Problem mit MS DTC nicht gelöst und die Datenbank nicht wiederhergestellt werden kann, führen Sie die Wiederherstellung einer Sicherungskopie der Datenbank aus.  
  
