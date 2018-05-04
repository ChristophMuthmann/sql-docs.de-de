---
title: 64-Bit-Ganzzahl-Strukturen | Microsoft Docs
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
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9f397923b652bf889dae70e14c39e2f3a8865c7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="64-bit-integer-structures"></a>64-Bit-Ganzzahl-Strukturen
Der C-Typ für die SQL_C_SBIGINT und SQL_C_UBIGINT-Datentypbezeichner auf Microsoft C-Compiler ist _int64. Wenn ein Compiler als ein Microsoft® C-Compiler verwendet wird, kann die C-Typ unterscheiden. Wenn der Compiler die 64-Bit-Ganzzahlen systemeigene Unterstützung bietet, sollten den Treiber oder die Anwendung ODBCINT64 werden von den systemeigenen 64-Bit-Ganzzahl-Typ definieren. Wenn der Compiler 64-Bit-Ganzzahlen nicht systemintern unterstützt wird, kann eine Anwendung oder Treiber definieren die folgenden Strukturen aus, um sicherzustellen, dass sie Zugriff auf diese Daten hat:  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 Diese Strukturen sollten eine 8-Byte-Grenze ausgerichtet sein, da eine 64-Bit-Ganzzahl, die 8-Byte-Grenze ausgerichtet ist.
