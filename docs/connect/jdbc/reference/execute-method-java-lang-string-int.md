---
title: Execute-Methode (java.lang.String, int[]) | Microsoft Docs
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.execute (javal.lang.String.int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc73d1c3-e756-43af-b1fc-ac438cbd0965
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 50cb9686b883ac0a4d682e7ea28f1dba40257c7e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="execute-method-javalangstring-int"></a>execute-Methode (java.lang.String, int[])

  Führt die angegebene SQL-Anweisung, der mehrere Ergebnisse, und signalisiert zurückgegeben werden können [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion-md.md)] , dass die automatisch generierten Schlüssel, die im angegebenen Array angegeben sind zum Abrufen verfügbar gemacht werden.

## <a name="syntax"></a>Syntax

```Java
public final boolean execute(
    java.lang.String sql,
    int[] columnIndexes)
```

#### <a name="parameters"></a>Parameter
*SQL*

Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.

*columnIndexes*

Ein Array von **Int**s, der die Spaltenindizes der automatisch generierten Schlüssel angibt, die verfügbar gemacht werden sollen.

## <a name="return-value"></a>Rückgabewert
**"true"** , wenn das erste Ergebnis ein Resultset handelt. Andernfalls lautet der Wert **false**.
  
## <a name="exceptions"></a>Ausnahmen
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Hinweise
Diese Execute-Methode wird von der Execute-Methode in der java.sql.Statement-Schnittstelle angegeben.

## <a name="see-also"></a>Siehe auch

[Execute-Methode &#40; SQLServerStatement &#41;](./execute-method-sqlserverstatement.md)

[SQLServerStatement-Elemente](./sqlserverstatement-members.md)

[SQLServerStatement-Klasse](./sqlserverstatement-class.md)

