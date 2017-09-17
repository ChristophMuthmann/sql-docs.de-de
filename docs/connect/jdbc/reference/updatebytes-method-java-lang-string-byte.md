---
title: UpdateBytes-Methode (java.lang.String, Byte) | Microsoft Docs
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
- SQLServerResultSet.updateBytes (java.lang.String, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4fb9de2b-61bc-4c96-89a5-c07cd7ee201a
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 995ae6ccb99dcf1b982d4675697ca7e4953487a0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updatebytes-method-javalangstring-byte"></a>UpdateBytes-Methode (java.lang.String, Byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Array von **Byte** Werte Berücksichtigung des Spaltennamens.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateBytes(java.lang.String columnName,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnName*  
  
 Ein **Zeichenfolge** , die den Namen der Spalte enthält.  
  
 *x*  
  
 Ein Array von **Byte** Werte.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateBytes-Methode wird von der UpdateBytes-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 In einer früheren Version von [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], Sie mithilfe von "sqlserverresultset.updateBytes" Werte zwischen Bytearrays konvertieren und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp **Datum**, **Zeit**, ** datetime2**, oder **"DateTimeOffset"**. Nun wird durch Verwendung der Methode mit diesen Datentypen eine Ausnahme ausgelöst, die angibt, dass die Konvertierung nicht unterstützt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateBytes-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
