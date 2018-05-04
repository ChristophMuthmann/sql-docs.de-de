---
title: ExecuteUpdate-Methode (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91ecb1cd-001d-4ac9-9ae8-5db05c3c2959
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb1b5e42d05508ea83b37985356c4eb0da6c68d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="executeupdate-method-javalangstring"></a>executeUpdate-Methode (java.lang.String)

Führt die angegebene SQL-Anweisung aus. Hierbei kann es sich um eine Anweisung vom Typ "INSERT", "UPDATE", "MERGE" oder "DELETE" oder um eine SQL-Anweisung handeln, von der nichts zurückgegeben wird (beispielsweise eine SQL-DDL-Anweisung).

## <a name="syntax"></a>Syntax

```
public final int executeUpdate(java.lang.String sql)
```

#### <a name="parameters"></a>Parameter
*sql*

Ein **Zeichenfolge** , die die SQL-Anweisung enthält.

## <a name="return-value"></a>Rückgabewert
Ein **Int** , der die Anzahl der betroffenen Zeilen, oder 0 bei Verwendung einer DDL-Anweisung angibt.

## <a name="exceptions"></a>Ausnahmen
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Hinweise
Diese ExecuteUpdate-Methode wird von der ExecuteUpdate-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.

Beim Aufrufen dieser Methode führt eine Ausnahme ausgelöst, da die SQL-Anweisung für die SQLServerPreparedStatement-Objekt angegeben wird, wenn das Objekt erstellt wird.

## <a name="see-also"></a>Siehe auch

[ExecuteUpdate-Methode &#40;sqlserverpreparedstatement-Klasse&#41;](./executeupdate-method-sqlserverpreparedstatement.md)

[SQLServerPreparedStatement-Elemente](./sqlserverpreparedstatement-members.md)

[SQLServerPreparedStatement-Klasse](./sqlserverpreparedstatement-class.md)
