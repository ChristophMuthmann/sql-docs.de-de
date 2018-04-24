---
title: MSSQLSERVER_1462 | Microsoft-Dokumentation
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
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3158e2c9314c2aee59ebaf711e5cd5b4eaa65e55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1462"></a>MSSQLSERVER_1462
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1462|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|Meldungstext|Die Datenbankspiegelung wird aufgrund eines Fehlers beim Wiederholungsvorgang deaktiviert. Der Vorgang kann nicht fortgesetzt werden.|  
  
## <a name="explanation"></a>Erklärung  
Bei der Datenbankspiegelung ist beim Wiederholungsvorgang für einen Protokolldatensatz für den Spiegel ein Fehler aufgetreten.  
  
### <a name="possible-causes"></a>Mögliche Ursachen  
Die wahrscheinlichste Ursache besteht darin, dass ein Vorgang zum Hinzufügen einer Datei für die Prinzipaldatenbank abgeschlossen wurde, bei diesem Vorgang auf der Spiegeldatenbank jedoch ein Fehler aufgetreten ist, da sich Dateinamen oder Verzeichnisstrukturen auf dem Prinzipalserver und dem Spiegelserver unterscheiden.  
  
## <a name="user-action"></a>Benutzeraktion  
Suchen Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll nach der Fehlerursache. Versuchen Sie, die Fehlerursache zu beheben, und setzen Sie anschließend die Datenbankspiegelung fort.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Problembehandlung für die Datenbankspiegelungskonfiguration &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
