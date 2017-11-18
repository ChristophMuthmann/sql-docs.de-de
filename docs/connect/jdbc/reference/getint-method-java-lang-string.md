---
title: GetInt-Methode (java.lang.String) | Microsoft Docs
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
apiname:
- SQLServerCallableStatement.getInt (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1705812f-1f04-4e84-b6c8-d164dded47b3
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 589ceac845495d5f3242aed6d04dbde1c2cd68c0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getint-method-javalangstring"></a>getInt-Methode (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Parameters als ein **Int** in der Programmiersprache Java ab Berücksichtigung des Parameternamens.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getInt(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sCol*  
  
 Ein **Zeichenfolge** , die den Namen des Parameters enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetInt-Methode wird von der GetInt-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
 Diese Methode wird nur unterstützt unter [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentypen, die einen Ganzzahlwert wie Int, Smallint, Tinyint und Bit sicher zurückgeben. Bei Verwendung dieser Methode für andere Datentypen wird eine Ausnahme ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [GetInt-Methode &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getint-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

