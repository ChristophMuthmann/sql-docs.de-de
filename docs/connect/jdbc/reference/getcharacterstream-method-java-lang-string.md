---
title: GetCharacterStream-Methode (java.lang.String) | Microsoft Docs
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
- SQLServerResultSet.getCharacterStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cdddc572-05c1-480d-b3e5-28270001575c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a882e903e689f67db7adf9b8d71d34851affd5b4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getcharacterstream-method-javalangstring"></a>getCharacterStream-Methode (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Spaltennamens in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekts als java.io.Reader-Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.io.Reader getCharacterStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnName*  
  
 Ein **Zeichenfolge** , die den Namen der Spalte enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein Readerobjekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetCharacterStream-Methode wird von der GetCharacterStream-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode wird nur lesen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Unicodezeichen-Datentypen wie Nchar, Nvarchar, nvarchar(max) und Ntext. Alle anderen Datentypen, einschließlich der ASCII-Zeichentypen lösen eine Ausnahme aus. Verwenden Sie zum Lesen der ASCII-Datentypen die [GetAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md) Methode.  
  
## <a name="see-also"></a>Siehe auch  
 [GetCharacterStream-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
