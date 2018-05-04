---
title: PrepareStatement-Methode (java.lang.String) | Microsoft Docs
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
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afd095efadf10a6838fb5ba8f6abec6a6f9e0bb5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="preparestatement-method-javalangstring"></a>prepareStatement-Methode (java.lang.String)

Erstellt eine [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) Objekt zum Senden parametrisierter SQL-Anweisungen in der Datenbank.

## <a name="syntax"></a>Syntax

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>Parameter
*sql*

Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.

## <a name="return-value"></a>Rückgabewert
Ein PreparedStatement-Objekt.

## <a name="exceptions"></a>Ausnahmen  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Hinweise
Diese PrepareStatement-Methode wird von der PrepareStatement-Methode in der java.sql.Connection-Schnittstelle angegeben.

## <a name="see-also"></a>Siehe auch

[PrepareStatement-Methode &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[SQLServerConnection-Elemente](./sqlserverconnection-members.md)

[SQLServerConnection-Klasse](./sqlserverconnection-class.md)
