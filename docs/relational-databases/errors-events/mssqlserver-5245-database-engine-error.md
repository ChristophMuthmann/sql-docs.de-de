---
title: MSSQLSERVER_5245 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: d1ee9b94e955cd560db165e774d623dbf2796aeb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|5245|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|Meldungstext|Objekt-ID O_ID ('NAME'-Objekt): DBCC konnte keine Sperre für dieses Objekt erhalten, da das Timeout für die Sperranforderung überschritten wurde. Das Objekt wurde ausgelassen und wird nicht verarbeitet.|  
  
## <a name="explanation"></a>Erklärung  
Ein Sperrtimeout ist aufgetreten, während DBCC auf eine Tabellensperre für das angegebene Objekt gewartet hat.  
  
## <a name="user-action"></a>Benutzeraktion  
Führen Sie den DBCC-Befehl erneut aus.  
  
