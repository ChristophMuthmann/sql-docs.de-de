---
title: "ZWISCHEN Prädikat | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1738aa33f371a2e64ea0362cefcf59a759fdfee7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="between-predicate"></a>ZWISCHEN Prädikat
Die Syntax lautet:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Gibt "true" nur, wenn *expression1* ist größer als oder gleich *expression2* und *expression1* ist kleiner als oder gleich *expression3*.  
  
 Die Semantik dieser Syntax unterscheiden sich für die Desktop-Datenbank-Treiber und der Microsoft Jet-Datenbankmodul. In der Microsoft Jet-SQL *expression2* kann größer sein als *expression3* , damit die Anweisung "true" zurückgibt, wenn nur *expression1* ist größer als oder gleich *expression3*, und *expression1* ist kleiner als oder gleich *expression2*.
