---
title: MSSQLSERVER_3619 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f487685e727f9f5ccf3862ac62cf0f1e21fb78ea
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3619"></a>MSSQLSERVER_3619
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3619|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SYS_NOLOG|  
|Meldungstext|In die Datenbank mit der ID %d konnte kein Prüfpunktdatensatz geschrieben werden, da für das Protokoll kein Speicherplatz mehr zur Verfügung steht. Bitten Sie den Datenbankadministrator, das Protokoll abzuschneiden oder den Datenbankprotokolldateien mehr Speicherplatz zuzuordnen.|  
  
## <a name="explanation"></a>Erklärung  
Für das Transaktionsprotokoll steht kein Speicherplatz mehr zur Verfügung.  
  
## <a name="user-action"></a>Benutzeraktion  
Schneiden Sie das Protokoll ab, um Speicherplatz freizugeben, oder ordnen Sie dem Protokoll mehr Speicherplatz zu. Weitere Informationen finden Sie unter "Problembehandlung bei vollen Transaktionsprotokollen (Fehler 9002)" in der SQL Server-Onlinedokumentation.  
  

