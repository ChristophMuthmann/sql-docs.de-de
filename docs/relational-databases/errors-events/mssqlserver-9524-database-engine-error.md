---
title: MSSQLSERVER_9524 | Microsoft-Dokumentation
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
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ef38d6859183ffb4b47a7a7d1a46e9ed77152f8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver9524"></a>MSSQLSERVER_9524
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|9254|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|XMLERR_INVALID_COLUMNSET_XML|  
|Meldungstext|Der angegebene XML-Inhalt entspricht nicht dem erforderlichen XML-Format für Sparsespaltensätze.|  
  
## <a name="explanation"></a>Erklärung  
Es wurde versucht, einen Spaltensatz zu ändern. Der XML-Inhalt eines Spaltensatzes muss die Formateinschränkungen für Spaltensätze erfüllen. Das allgemeine Format eines Spaltensatzes sieht folgendermaßen aus:  
  
`<column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...`  
  
Weitere Informationen zu Spaltensätzen finden Sie im Thema "Verwenden von Spaltensätzen" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
## <a name="user-action"></a>Benutzeraktion  
Korrigieren Sie das XML-Format für den Spaltensatz in der Anweisung.  
  
