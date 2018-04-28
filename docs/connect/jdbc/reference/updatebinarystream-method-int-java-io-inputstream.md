---
title: UpdateBinaryStream-Methode (Int, java.io.InputStream) | Microsoft Docs
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
ms.topic: article
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f124760dfcd86342b083c5aa4b88c749e79771d3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="updatebinarystream-method-int-javaioinputstream"></a>updateBinaryStream-Methode (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Binärdatenstromwert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateBinaryStream(int columnIndex,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnIndex*  
  
 Ein **Int** , der den Spaltenindex angibt.  
  
 *x*  
  
 Ein InputStream-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateBinaryStream-Methode wird von der UpdateBinaryStream-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Mit dieser Methode für die **Image**, **Text**, und **Ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentypen können die Leistung beeinträchtigen.  
  
 Diese Methode transferiert Bytes aus einem Objekt InputStream ausgewählt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] binärer Spalten wie Binary, Varbinary, varbinary(max), Image, Xml und Udt. Das Aktualisieren von Zeichenspalten wird für diese Methode nicht unterstützt. Verwenden Sie zum Aktualisieren von Zeichenspalten mit InputStream der [UpdateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) Methode.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateBinaryStream-Methode &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
