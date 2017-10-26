---
title: GetString-Methode (Int) (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa493c4-fe07-449b-b4d0-384e1a1fce48
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2851090b2f22faac3f050ad535ec9f36ac3efae6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getstring-method-int-sqlserverresultset"></a>GetString-Methode (Int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Spaltenindexes in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **Zeichenfolge** in der Programmiersprache Java ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getString(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnIndex*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetString-Methode wird von der GetString-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Alle Spalten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] als Zeichenfolge zurückgegeben werden kann. Dies bedeutet, dass eine **Zeichenfolge** Darstellung aller Zahlen- und zeichenfolgenbasierten Typen und eine Hex-Zeichenfolgendarstellung binärer Spalten wie Binary, Varbinary, varbinary(max), Image, Timestamp und "Uniqueidentifier" werden können zurückgegeben.  
  
 Speicherort sicherheitskritische Typen wie z. B. Money, Smallmoney, Datetime, Smalldatetime, Float, real, decimal und numeric werden für den zugrunde liegenden Wert des Typs das kanonische ToString()-Format zurück.  
  
 Benutzerdefinierte Typen werden zurückgegeben, als eine Hexadezimalzeichenfolge **Zeichenfolge** Werte.  
  
## <a name="see-also"></a>Siehe auch  
 [GetString-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

