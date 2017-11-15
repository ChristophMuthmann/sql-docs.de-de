---
title: MSSQLSERVER_3437 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 92bb3d6a8ed547f0e5e3c185db78fcb55f1e12ea
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3437"></a>MSSQLSERVER_3437
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3437|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|NODTC|  
|Meldungstext|Fehler beim Wiederherstellen der '%.*ls'-Datenbank. Es konnte keine Verbindung mit Microsoft Distributed Transaction Coordinator (MS DTC) hergestellt werden, um den Beendigungsstatus von Transaktion %S_XID zu überprüfen. Korrigieren Sie MS DTC, und führen Sie die Wiederherstellung erneut aus.|  
  
## <a name="explanation"></a>Erklärung  
Eine oder mehrere verteilte Transaktionen, für die MS DTC ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator) verwendet wurde, waren nicht abgeschlossen, als die Datenbank beendet wurde. Bei der Wiederherstellung dieser Datenbank sind Fehler aufgetreten, da in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keine Verbindung mit MS DTC hergestellt werden kann, um die Transaktionen abzuschließen oder einen Rollback für die Transaktionen auszuführen.  
  
## <a name="user-action"></a>Benutzeraktion  
Zum Wiederherstellen dieser Datenbank müssen Sie zunächst das Problem mit MS DTC lösen. Weitere Informationen zu diesem Problem mit MS DTC finden Sie in den Windows-Ereignisprotokollen. Wenn das Problem mit MS DTC nicht gelöst und die Datenbank nicht wiederhergestellt werden kann, führen Sie die Wiederherstellung einer Sicherungskopie der Datenbank aus.  
  
