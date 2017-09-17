---
title: GetNClob-Methode (java.lang.String) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be01ce56-8f13-437b-8de6-246cda5f7830
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd11b3bc0f6a43ffcc504b99b117e3eab5170749
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getnclob-method-javalangstring"></a>getNClob-Methode (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des einem JDBC **NCLOB** Parameter als NClob-Objekt in der Programmiersprache Java ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.NClob getNClob(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterName*  
  
 Ein **Zeichenfolge** , die den Namen des Parameters enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 ANClobobject.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetNClob-Methode wird von der GetNClob-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
 Diese Methode unterstützt nur das Abrufen **NCHAR**, **NVARCHAR**, **NTEXT**, und **XML** Parameter. Werden diese Methoden für andere Datentypparameter aufgerufen, wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [GetNClob-Methode &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
