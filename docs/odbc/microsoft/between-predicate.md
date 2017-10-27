---
title: "ZWISCHEN Prädikat | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8daaa0e1c26f00acbff2e6f7788eab8ee5ac8ce
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="between-predicate"></a>ZWISCHEN Prädikat
Die Syntax lautet:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Gibt "true" nur, wenn *expression1* ist größer als oder gleich *expression2* und *expression1* ist kleiner als oder gleich *expression3*.  
  
 Die Semantik dieser Syntax unterscheiden sich für die Desktop-Datenbank-Treiber und der Microsoft Jet-Datenbankmodul. In der Microsoft Jet-SQL *expression2* kann größer sein als *expression3* , damit die Anweisung "true" zurückgibt, wenn nur *expression1* ist größer als oder gleich *expression3*, und *expression1* ist kleiner als oder gleich *expression2*.

