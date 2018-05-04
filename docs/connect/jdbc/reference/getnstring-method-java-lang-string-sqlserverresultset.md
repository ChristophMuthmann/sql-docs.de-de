---
title: GetNString-Methode (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
ms.assetid: 546d77e2-723a-42ac-ba3f-fabf2395d376
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38e3391d16fed59fbb0de1efd8052e8eb9260f90
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getnstring-method-javalangstring-sqlserverresultset"></a>getNString-Methode (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert der angegebenen Spalte in der aktuellen Zeile ab der [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt als ein java.lang.String-Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getNString(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnLabel*  
  
 Eine Zeichenfolge, die die Bezeichnung der Spalte enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein String-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetNString-Methode wird von der GetNString-Methode in der java.sql.SQLServerResultSet-Schnittstelle angegeben.  
  
 Diese Methode kann verwendet werden, zum Abrufen des Werts von einer **Nvarchar**, **Nchar**, **nvarchar(max)**, **Ntext**, oder **Xml** Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt. Beim Versuch, mit dieser Methode Werte anderer Datentypen abzurufen, wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [GetNString-Methode &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
