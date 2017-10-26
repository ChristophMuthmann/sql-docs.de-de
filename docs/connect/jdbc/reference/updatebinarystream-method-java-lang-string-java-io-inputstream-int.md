---
title: UpdateBinaryStream-Methode (java.io.InputStream, Int) | Microsoft Docs
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
- SQLServerResultSet.updateBinaryStream (java.lang.String, java.io.InputStream, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9be246a7-85fa-49fc-ad79-aabe97f5b280
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e1199bdd667e4b24c39f987a37f48f841176ae05
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream-int"></a>updateBinaryStream-Methode (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Binärdatenstromwert mit der angegebenen Anzahl von Bytes.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x,  
                               int length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnLabel*  
  
 AStringthat enthält die Bezeichnung der Spalte.  
  
 *x*  
  
 Ein InputStream-Objekt.  
  
 *length*  
  
 Ein **Int** , der die Länge des Streams angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateBinaryStream-Methode wird von der UpdateBinaryStream-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode transferiert Bytes aus einem Objekt InputStream ausgewählt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] binärer Spalten wie Binary, Varbinary, varbinary(max), Image, Xml und Udt. Das Aktualisieren von Zeichenspalten wird für diese Methode nicht unterstützt. Verwenden Sie zum Aktualisieren von Zeichenspalten mit InputStream der [UpdateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) Methode.  
  
 Wenn die Länge des Datenstroms, angegeben unterscheidet die *Länge* Parameter, der JDBC-Treiber löst eine Ausnahme aus, wenn die Zeile aktualisiert oder eingefügt wird.  
  
 Wenn die Länge des Datenstroms unbekannt ist, ist die *Länge* Parameter kann auf-1 festgelegt werden, um anzugeben, dass der Treiber den Datenstrom unabhängig von seiner Länge akzeptiert werden sollen. Bei "sqljdbc4.jar", empfehlen wir, dass Sie die JDBC 4.0-Methode verwenden [UpdateBinaryStream-Methode &#40;java.lang.String, java.io.InputStream &#41;](../../../connect/jdbc/reference/updatebinarystream-method-java-lang-string-java-io-inputstream.md) Wenn die Anwendung die Spalte aus einem Datenstrom Länge zu aktualisieren möchte unbekannt.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateBinaryStream-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

