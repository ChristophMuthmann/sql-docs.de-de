---
title: ZWISCHEN Prädikat | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9909930941c7dfd6a180ca3e33b7e89c7d9c4825
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="between-predicate"></a>ZWISCHEN Prädikat
Die Syntax lautet:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Gibt "true" nur, wenn *expression1* ist größer als oder gleich *expression2* und *expression1* ist kleiner als oder gleich *expression3*.  
  
 Die Semantik dieser Syntax unterscheiden sich für die Desktop-Datenbank-Treiber und der Microsoft Jet-Datenbankmodul. In der Microsoft Jet-SQL *expression2* kann größer sein als *expression3* , damit die Anweisung "true" zurückgibt, wenn nur *expression1* ist größer als oder gleich *expression3*, und *expression1* ist kleiner als oder gleich *expression2*.
