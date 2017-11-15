---
title: MSSQLSERVER_1461 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 191de2402cca3e0e306a3dca2ede0a06ebcd755c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver1461"></a>MSSQLSERVER_1461
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1461|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBM_SAFETY_MISMATCH|  
|Meldungstext|Für die "%.*ls"-Datenbank wurden bei den Servern unterschiedliche Sicherheitsstufen für die Datenbankspiegelung gefunden. Die Sicherheitsstufe FULL wird verwendet.|  
  
## <a name="explanation"></a>Erklärung  
Die Spiegelungsverbindungen wurden unterbrochen, als die Sicherheitsstufe der Transaktion geändert wurde, da die Sicherheitseinstellungen der Transaktion für die Prinzipal- und Spiegeldatenbank inkonsistent waren. Es wird die Standardsicherheitseinstellung der Sicherheit für vollständige Transaktionen verwendet. Die Sitzung wird im Modus für hohe Sicherheit ausgeführt.  
  
## <a name="user-action"></a>Benutzeraktion  
Wenn Sie die Transaktionssicherheit initiieren möchten, führen Sie die ALTER DATABASE *Datenbank_Name* SET PARTNER SAFETY OFF-Anweisung für die Prinzipaldatenbank erneut aus.  
  
