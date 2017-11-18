---
title: GetNClob-Methode (Int) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 10dfa251-9408-469e-ae2a-1acf3917cf47
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d708887958eb78b625dce47914433761f434ed4a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getnclob-method-int"></a>getNClob-Methode (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen JDBC **NCLOB** Parameter als NClob-Objekt in der Programmiersprache Java ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.NClob getNClob(int parameterIndex)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterIndex*  
  
 Ein **Int** , der die Indexnummer des Parameters angibt.  
  
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
  
  

