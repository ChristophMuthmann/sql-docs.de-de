---
title: UpdateNClob-Methode (java.lang.String, java.io.Reader, long) | Microsoft Docs
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
ms.assetid: ad5c8d9b-f8c8-4ddf-85c8-23420bba54ee
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51100f0358f85b3e8347328f84d6265c43c1d1b3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="updatenclob-method-javalangstring-javaioreader-long"></a>updateNClob-Methode (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Aktualisiert die angegebene Spalte unter Verwendung des angegebenen **Reader** Objekt, das die angegebene Anzahl von Zeichen lang ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void updateNClob(java.lang.String columnLabel,  
                        java.io.Reader reader,  
                        long length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *columnLabel*  
  
 Ein **Zeichenfolge** , der die Bezeichnung der Spalte angibt.  
  
 *Reader*  
  
 Ein Readerobjekt.  
  
 *length*  
  
 Die Anzahl von Zeichen in den Parameterdaten.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese UpdateNClob-Methode wird von der UpdateNClob-Methode in der java.sql.ResultSet-Schnittstelle angegeben.  
  
 Diese Methode wird nur unterstützt unter **nvarchar(max)**, **Ntext**, und **Xml** Spalten. Bei Verwendung dieser Methode für andere Datentypen wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateNClob-Methode &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
