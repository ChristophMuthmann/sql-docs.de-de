---
title: MSSQLSERVER_9790 | Microsoft-Dokumentation
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
helpviewer_keywords: 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f38c88f7dc009d9af03d720873a6de89caec41f0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|9790|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|Meldungstext|Die eingehende Nachricht kann nicht geroutet werden. Die MSDB-Systemdatenbank, die Routinginformationen enthält, befindet sich im Einzelbenutzermodus.|  
  
## <a name="explanation"></a>Erklärung  
Beim Klassifizieren einer empfangenen Nachricht ist ein Fehler aufgetreten, da die MSDB-Datenbank im SINGLE USER-Modus war.  
  
## <a name="user-action"></a>Benutzeraktion  
Ändern Sie die MSDB-Datenbank mit dem Befehl ALTER DATABASE auf den MULTI USER-Modus.  
  
