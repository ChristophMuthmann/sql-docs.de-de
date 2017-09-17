---
title: ExecuteUpdate-Methode (java.lang.String) | Microsoft Docs
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
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 264ccb901e544eb0990f39ed53d112c7f8e9220f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring"></a>executeUpdate-Methode (java.lang.String)

Führt die angegebene SQL-Anweisung aus. Hierbei kann es sich um eine Anweisung vom Typ "INSERT", "UPDATE", "MERGE" oder "DELETE" oder um eine SQL-Anweisung handeln, von der nichts zurückgegeben wird (beispielsweise eine SQL-DDL-Anweisung).

## <a name="syntax"></a>Syntax

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>Parameter
*SQL*

Ein **Zeichenfolge** , die die SQL-Anweisung enthält.

## <a name="return-value"></a>Rückgabewert
Ein **Int** , der die Anzahl der betroffenen Zeilen, oder 0 bei Verwendung einer DDL-Anweisung angibt.

## <a name="exceptions"></a>Ausnahmen
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Hinweise
Diese ExecuteUpdate-Methode wird von der ExecuteUpdate-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.

Beim Aufrufen dieser Methode führt eine Ausnahme ausgelöst, da die SQL-Anweisung für die SQLServerPreparedStatement-Objekt angegeben wird, wenn das Objekt erstellt wird.

## <a name="see-also"></a>Siehe auch

[ExecuteUpdate-Methode &#40; SQLServerPreparedStatement &#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[SQLServerPreparedStatement-Elemente](./sqlserverpreparedstatement-members.md)

[SQLServerPreparedStatement-Klasse](./sqlserverpreparedstatement-class.md)

