---
title: ExecuteUpdate-Methode (java.lang.String, Int) | Microsoft Docs
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
apiname: SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3226c9c4ae102a80708fb5a020f9e9a9a32cdf5e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate-Methode (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Führt die angegebene SQL-Anweisung und signalisiert dem [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] mit dem angegebenen Flag gibt an, ob automatisch generierte-Schlüssel werden von diesem erzeugt [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt zum Abrufen verfügbar gemacht werden sollen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int flag)  
```  
  
#### <a name="parameters"></a>Parameter  
 *SQL*  
  
 Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.  
  
 *Kennzeichen*  
  
 Ein **Int** Wert, der angibt, ob der automatisch generierten Schlüssel verfügbar gemacht werden sollen. Dabei muss es sich um eine der folgenden Konstanten handeln:  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Int** , der die Anzahl der betroffenen Zeilen, oder 0 bei Verwendung einer DDL-Anweisung angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese ExecuteUpdate-Methode wird von der ExecuteUpdate-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
 Wenn eine updatezählung eine gespeicherte Prozedur auszuführen führt, die größer als 1 ist, oder, generiert mehr als ein Resultset, verwenden, die [ausführen](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) Methode zum Ausführen der gespeicherten Prozedur.  
  
## <a name="see-also"></a>Siehe auch  
 [ExecuteUpdate-Methode &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
