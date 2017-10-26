---
title: UpdateAsciiStream-Methode (java.io.InputStream) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 747b0308-1ce6-4eba-bdfc-af29c21c18cf
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7885895db612ffd4fd6801cea64242ad9347859
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updateasciistream-method-javalangstring-javaioinputstream"></a>updateAsciiStream-Methode (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem ASCII-Datenstromwert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateAsciiStream(java.lang.String columnLabel,  
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
 Diese UpdateAsciiStream-Methode wird von der UpdateAsciiStream-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode wird von ASCII-Zeichen (Bytes) von einem Objekt InputStream an konvertierbare Zeichenspalten, die den ASCII-Bereich [0 x 00 – 0x7F] von Unicode und 874, 932, 936, 949, 950 und 1250 bis 1258-Codepages. Von dieser Methode wird eine Konvertierung zur Zielsortierseite vorgenommen. Beim Versuch, eine nicht konvertierbare Zielspalte zu aktualisieren, wird eine Ausnahme ausgelöst. Für Binärspalten werden Rohbytes übergeben.  
  
 Mit dieser Methode für die **Image**, **Text**, und **Ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentypen können die Leistung beeinträchtigen.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateAsciiStream-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

