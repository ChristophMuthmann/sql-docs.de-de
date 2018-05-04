---
title: Länge des Datentyps Interval | Microsoft Docs
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
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e611326930b099496db893d4d46d36bbd04116ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="interval-data-type-length"></a>Datentyplänge Intervall
Die folgenden Regeln werden verwendet, um zu bestimmen, die Länge eines Intervalls-Datentyps in Zeichen. Länge wird in Anzahl von Zeichen angegeben. Die Anzahl der Bytes, hängt von den Zeichensatz ab. Die Länge der umfasst die folgenden Werte, die zusammengefügt wurden:  
  
-   Zwei Zeichen für jedes Feld in das Intervall, das nicht das führende Feld ist.  
  
-   Führende Feld die Anzahl der Zeichen, die die ausdrückliche oder implizite führende Genauigkeit ist. Wenn die führende Genauigkeit nicht angegeben wird, ist der Standardwert 2.  
  
-   Ein Zeichen für das Trennzeichen zwischen den Feldern.  
  
-   1 plus die ausdrückliche oder konkludente Sekunden Genauigkeit. Wenn die Genauigkeit Sekunden nicht angegeben wird, ist der Standardwert 6.  
  
 Bestimmte Länge Spaltenwerte für jeden Datentyp Intervall in enthaltenen [Spaltengröße](../../../odbc/reference/appendixes/column-size.md).
