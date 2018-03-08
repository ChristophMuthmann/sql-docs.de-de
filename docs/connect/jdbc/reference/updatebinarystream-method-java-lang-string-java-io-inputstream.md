---
title: UpdateBinaryStream-Methode (java.io.InputStream) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 56883144-26a0-4f45-ad36-4f616369af3e
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f91ce9be6ff4f05585b751e506462100cb09f078
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream"></a>updateBinaryStream-Methode (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Binärdatenstromwert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnLabel*  
  
 Ein **Zeichenfolge** , die die Bezeichnung der Spalte enthält.  
  
 *x*  
  
 Ein InputStream-Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateBinaryStream-Methode wird von der UpdateBinaryStream-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Mit dieser Methode für die **Image**, **Text**, und **Ntext** SQL Server-Datentypen können die Leistung beeinträchtigen.  
  
 Diese Methode transferiert Bytes aus einem Objekt InputStream ausgewählt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] binärer Spalten wie Binary, Varbinary, varbinary(max), Image, Xml und Udt. Das Aktualisieren von Zeichenspalten wird für diese Methode nicht unterstützt. Verwenden Sie zum Aktualisieren von Zeichenspalten mit InputStream der [UpdateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) Methode.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateBinaryStream-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
