---
title: GUID-Escapesequenzen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5edd631171acf78fd4c0ada857f72e4e50fd5ebe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="guid-escape-sequences"></a>GUID-Escapesequenzen
Verwendung von ODBC Escapesequenzen für GUID-Literale. Die Syntax für diese Escapesequenz lautet wie folgt:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Hinweise  
 In BNF-Schreibweise ist die Syntax folgendermaßen:  
  
 *ODBC-Guid-Escape* :: =  
     *Initiator der ODBC-esc Guid* "*Guid-Wert*" *ODBC-esc-Abschlusszeichen*  
  
 *Initiator der ODBC-esc* :: = {}  
  
 *ODBC-esc-Terminator* :: =}  
  
 *GUID-Wert* :: = *Uhr-Low-Guid-Trennzeichen Uhr-mittleren-Guid-Trennzeichen Uhr-hochwertige Guid-Trennzeichen Uhr-Seq-Guid-Trennzeichen Knotenwert*  
  
 *GUID-Trennzeichen* :: = -  
  
 *Uhr-geringwertige* :: = *Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit*  
  
 *Uhr-mittleren-Value* :: = *Hex_digit Hex_digit Hex_digit Hex_digit*  
  
 *Uhr-hochwertige* :: = *Hex_digit Hex_digit Hex_digit Hex_digit*  
  
 *Seq-Uhrzeit* :: = *Hex_digit Hex_digit Hex_digit Hex_digit*  
  
 *Uhr Knotenwert* :: = *Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit Hex_digit*  
  
 *Hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; ein &#124; B &#124; C &#124; D &#124; E &#124; F  
  
 Die GUID-literal-Escapesequenz wird unterstützt, wenn der GUID-Datentyp von der Datenquelle unterstützt wird. Eine Anwendung sollte Aufrufen **SQLGetTypeInfo** um zu bestimmen, ob dieser Datentyp unterstützt wird.
