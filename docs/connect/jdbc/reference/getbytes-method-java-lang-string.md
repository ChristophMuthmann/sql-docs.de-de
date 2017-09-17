---
title: GetBytes-Methode (java.lang.String) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d0dac7f-7f39-47a2-953e-80ab03688d82
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2d4a2eba7c1ec403d8079188c8cdc8a874bf7cdf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getbytes-method-javalangstring"></a>getBytes-Methode (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Parameters unter Berücksichtigung des Parameternamens als ein Array von Bytewerten ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public byte[] getBytes(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sCol*  
  
 Ein **Zeichenfolge** , die den Namen des Parameters enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Array von **Byte** Werte.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 In einer früheren Version von [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], Sie mithilfe von "sqlservercallablestatement.GetBytes" Werte zwischen Bytearrays konvertieren und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp **Datum**, **Zeit**, ** datetime2**, oder **"DateTimeOffset"**. Nun wird durch Verwendung der Methode mit diesen Datentypen eine Ausnahme ausgelöst, die angibt, dass die Konvertierung nicht unterstützt wird.  
  
 Diese GetBytes-Methode wird von der GetBytes-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [GetBytes-Methode &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
