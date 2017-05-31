---
title: MSSQLSERVER_12329 | Microsoft-Dokumentation
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
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
caps.latest.revision: 4
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 47b2380fdb3bf5fbde95bfbd984c3ed6095dcd1f
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver12329"></a>MSSQLSERVER_12329
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|12329|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|HK_UNSUPPORTED_NON_LATIN_CODEPAGE|  
|Meldungstext|Die Datentypen char(n) und varchar(n), die Sortierungen mit einer anderen Codepage als 1252 verwenden, werden bei *construct* nicht unterstützt.|  
  
## <a name="explanation"></a>Erklärung  
Verwenden Sie die Datentypen char(n) und varchar(n) nicht mit Sortierungen, die eine andere Codepage als 1252 verwenden.  
  
## <a name="user-action"></a>Benutzeraktion  
Die folgende unerwartete Situation kann zu diesem Fehler führen:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'us_english')  
```  
  
Verwenden Sie stattdessen:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
```  
  

