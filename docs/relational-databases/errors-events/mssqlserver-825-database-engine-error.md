---
title: MSSQLSERVER_825 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 825 (Database Engine error)
ms.assetid: f69f8214-5af1-4769-878b-117ad6eaff52
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: edd994bcc2b288f27917db402e0422c29b4548d1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver825"></a>MSSQLSERVER_825
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|825|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|B_RETRYWORKED|  
|Meldungstext|Ein Lesevorgang für die Datei '%ls' und den Offset %#016I64x war nach %d fehlerhaften Versuchen mit dem Fehler %ls erfolgreich. Weitere Informationen finden Sie möglicherweise in zusätzlichen Meldungen im SQL Server-Fehlerprotokoll und im Systemereignisprotokoll. Dieser Fehler bedroht die Datenbankintegrität und muss behoben werden. Führen Sie eine vollständige Datenbankkonsistenzprüfung (DBCC CHECKDB) aus. Dieser Fehler kann viele Ursachen haben. Weitere Informationen finden Sie in der SQL Server-Onlinedokumentation.|  
  
## <a name="explanation"></a>Erklärung  
Mit dieser Meldung wird angegeben, dass der Lesevorgang mindestens ein Mal wiederholt werden musste. Zudem wird hiermit auf ein größeres Problem mit der Datenträgerhardware hingewiesen. Diese Meldung deutet aktuell nicht auf ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Problem hin, durch das Datenträgerproblem werden möglicherweise Datenverluste oder Beschädigungen der Datenbank verursacht, wenn es nicht behoben wird. Das Systemereignisprotokoll enthält möglicherweise ähnliche Ereignisse, anhand derer eine Problemdiagnose vorgenommen werden kann. Weitere Informationen zu E/A-Fehlern finden Sie unter [Microsoft SQL Server I/O Basics, Chapter 2 (Microsoft SQL Server - Grundlagen zur E/A, Kapitel 2)](http://go.microsoft.com/fwlink/?LinkId=69370).  
  
## <a name="user-action"></a>Benutzeraktion  
Mit den folgenden Aktionen können Sie das zugrunde liegende Problem möglicherweise identifizieren und lösen:  
  
-   Beachten Sie das Fehlerprotokoll und den jeweiligen Text in dieser Meldung, um Informationen zu den Ursachen für das Problem zu erfahren.  
  
-   Prüfen Sie Ihr Datenträgersystem. Das Problem ist möglicherweise auf die Datenträger, Datenträgercontroller, Arraykarten oder Datenträgertreiber zurückzuführen.  
  
-   Die neuesten Hilfsprogramme zum Überprüfen des Status Ihres Datenträgersystems erhalten Sie beim Hersteller des Datenträgers.  
  
-   Wenden Sie sich an den Hersteller des Datenträgers, um die neuesten Treiberupdates zu erhalten.  
  
