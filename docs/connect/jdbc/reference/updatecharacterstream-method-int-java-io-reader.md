---
title: UpdateCharacterStream-Methode (Int, java.io.Reader) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4dddf885-0482-4776-8e9a-69f6c6270931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74898560434c44891a92e38940b521785cb3a5e5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="updatecharacterstream-method-int-javaioreader"></a>updateCharacterStream-Methode (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte mit einem Zeichendatenstromwert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateCharacterStream(int columnIndex,  
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
 Diese UpdateCharacterStream-Methode wird von der UpdateCharacterStream-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode wird Unicode-Zeichen aus einem Readerobjekt an ausgewählte Text- und Binärspalten übergeben. Dies schließt alle Textspalten und **binäre**, **Varbinary**, **varbinary(max)**, **Image**, und **Xml**Spalten, aber nicht **Udt** Spalten.  
  
 Mit dieser Methode für die **Image**, **Text**, und **Ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentypen können die Leistung beeinträchtigen.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateCharacterStream-Methode &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
