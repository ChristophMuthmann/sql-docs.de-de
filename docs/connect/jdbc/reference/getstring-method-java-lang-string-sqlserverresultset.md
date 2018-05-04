---
title: GetString-Methode (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getString (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a98c8a8-61d0-40c9-9335-25a87b732dc3
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f615ce3f4f9fcd883ccb9f8ebc380c5e71e1a4eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getstring-method-javalangstring-sqlserverresultset"></a>GetString-Methode (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Spaltennamens in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) -Objekt als eine **Zeichenfolge** in der Programmiersprache Java ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getString(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnName*  
  
 Ein **Zeichenfolge** , die den Namen der Spalte enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetString-Methode wird von der GetString-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Alle Spalten in SQL Server können als Zeichenfolge zurückgegeben werden. Dies bedeutet, dass eine **Zeichenfolge** Darstellung aller Zahlen- und zeichenfolgenbasierten Typen und eine Hex-Zeichenfolgendarstellung binärer Spalten wie Binary, Varbinary, varbinary(max), Image, Timestamp und "Uniqueidentifier" werden können zurückgegeben.  
  
 Den Speicherort berücksichtigende Typen wie "money", "smallmoney", "datetime", "smalldatetime", "float", "real", "decimal" oder "numeric" geben für den zugrundeliegenden Wert des Typs das kanonische toString()-Format zurück.  
  
 Benutzerdefinierte Typen werden zurückgegeben, als eine Hexadezimalzeichenfolge **Zeichenfolge** Werte.  
  
## <a name="see-also"></a>Siehe auch  
 [GetString-Methode &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
