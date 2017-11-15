---
title: MSSQLSERVER_15661 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: bba24fb998afb3713de138c1c77f7a15bf04d100
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|15661|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|SQLErrorNum15661|  
|Meldungstext|Die gespeicherte Prozedur sp_estimate_data_compression_savings kann nicht für temporäre Tabellen verwendet werden.|  
  
## <a name="explanation"></a>Erklärung  
Eine temporäre Tabelle wurde als Argument für die gespeicherte Prozedur sp_estimate_data_compression_savings verwendet. Obwohl die Komprimierung von temporären Tabellen unterstützt wird, können Sie sp_estimate_data_compression_savings nicht verwenden, um die Komprimierungseinsparungen zu schätzen.  
  
## <a name="user-action"></a>Benutzeraktion  
Entfernen Sie die temporäre Tabelle als Argument für sp_estimate_data_compression_savings.  
  
