---
title: UpdateNCharacterStream-Methode (Int, java.io.Reader) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc746413-bdbf-4109-aee0-385a1270c847
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 03460e0fc6529ac01fff341c0082ab886bd11e16
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updatencharacterstream-method-int-javaioreader"></a>updateNCharacterStream-Methode (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Zeichendatenstromwert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateNCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnIndex*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
 *x*  
  
 Ein Readerobjekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateNCharacterStream-Methode wird von der UpdateNCharacterStream-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode transferiert Unicode-Zeichen aus einem Reader-Objekt an ausgewählte **Nchar**, **nvarchar(max)**, **Ntext** und **Xml** Spalten. Bei Verwendung dieser Methode für andere Datentypspalten wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateNCharacterStream-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

