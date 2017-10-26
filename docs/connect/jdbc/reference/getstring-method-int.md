---
title: GetString-Methode (Int) | Microsoft Docs
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
- SQLServerCallableStatement.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3fce8bf-8d6e-476f-aa6d-992daa79b899
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 638768b0806fd032a984a4279076e5e225a9ab54
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getstring-method-int"></a>getString-Methode (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert des angegebenen Parameters als eine **Zeichenfolge** in der Berücksichtigung des parameterindexes Programmiersprache Java ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getString(int index)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Index*  
  
 Ein **Int** , der die Indexnummer des Parameters angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** Wert.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetString-Methode wird von der GetString-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
 Alle Spalten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] als Zeichenfolge zurückgegeben werden kann. Es können also eine Zeichenfolgendarstellung aller zahlen- und zeichenfolgenbasierten Typen und eine hexadezimale Zeichenfolgendarstellung binärer Spalten wie "binary", "varbinary", "varbinary(max)", "image", "timestamp" oder "uniqueidentifier" zurückgegeben werden.  
  
 Speicherort sicherheitskritische Typen wie z. B. Money, Smallmoney, Datetime, Smalldatetime, Float, real, decimal und numeric werden für den zugrunde liegenden Wert des Typs das kanonische ToString()-Format zurück.  
  
 Benutzerdefinierte Typen werden als hexadezimale Zeichenfolgenwerte zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [GetString-Methode &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

