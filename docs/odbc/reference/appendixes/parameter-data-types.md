---
title: Parameterdatentypen | Microsoft Docs
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
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a43fdab2fd7ffeaf409bde41c06386fad23d3c3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-data-types"></a>Parameterdatentypen
Obwohl jedes Parameters angegeben **SQLBindParameter** ist definierten mithilfe eines SQL-Datentyps, die Parameter in einer SQL­Anweisung keine systeminterne-Datentyp aufweisen. Parametermarkierungen können daher in einer SQL­Anweisung aufgenommen werden, nur dann, wenn ihre Datentypen aus einem anderen Operanden in der Anweisung abgeleitet werden können. Beispielsweise ist in einem arithmetischen Ausdruck, z. B.? + Der Datentyp der benannten Spalte COLUMN1 dargestellte können COLUMN1, den Datentyp des Parameters abgeleitet werden. Eine Anwendung kann keine parametermarkierung verwenden, wenn der Datentyp bestimmt werden kann.  
  
 In der folgenden Tabelle wird beschrieben, wie ein Datentyp für mehrere Typen von Parametern in Übereinstimmung mit SQL-92 bestimmt wird. Eine umfassendere Spezifikation auf den Parametertyp ableiten, wenn andere SQL-Klauseln verwendet werden finden Sie in der SQL-92-Spezifikation.  
  
|Speicherort des Parameters|Davon ausgegangen, dass-Datentyp|  
|---------------------------|-----------------------|  
|Ein Operand eines binären Operators von arithmetischen oder Vergleichsoperation|Identisch mit der andere operand|  
|Der erste Operand in einem **BETWEEN** Klausel|Identisch mit der zweite operand|  
|Der zweite oder dritte Operand in einem **BETWEEN** Klausel|Identisch mit den ersten Operanden|  
|Ein Ausdruck für die **IN**|Identisch mit den ersten Wert oder der Ergebnisspalte der Unterabfrage|  
|Ein Wert, der mit verwendet **IN**|Identisch mit dem Ausdruck oder den ersten Wert, wenn eine parametermarkierung im Ausdruck vorliegt.|  
|Einen Musterwert mit verwendet **wie**|VARCHAR|  
|Eine Updatewert, der verwendet wird, mit **aktualisieren**|Der Update-Spalte|
