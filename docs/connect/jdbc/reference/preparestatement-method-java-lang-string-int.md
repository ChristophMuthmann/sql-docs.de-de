---
title: PrepareStatement-Methode (java.lang.String) | Microsoft Docs
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c2452837aba5b8c5a146c12de838a3259f65be38
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="preparestatement-method-javalangstring"></a>prepareStatement-Methode (java.lang.String)

Erstellt eine [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) Objekt zum Senden parametrisierter SQL-Anweisungen in der Datenbank.

## <a name="syntax"></a>Syntax

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>Parameter
*SQL*

Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.

## <a name="return-value"></a>Rückgabewert
Ein PreparedStatement-Objekt.

## <a name="exceptions"></a>Ausnahmen  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Hinweise
Diese PrepareStatement-Methode wird von der PrepareStatement-Methode in der java.sql.Connection-Schnittstelle angegeben.

## <a name="see-also"></a>Siehe auch

[PrepareStatement-Methode &#40; SQLServerConnection &#41;](./preparestatement-method-sqlserverconnection.md)

[SQLServerConnection-Elemente](./sqlserverconnection-members.md)

[SQLServerConnection-Klasse](./sqlserverconnection-class.md)

