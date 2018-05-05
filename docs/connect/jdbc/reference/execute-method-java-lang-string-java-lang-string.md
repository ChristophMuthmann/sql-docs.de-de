---
title: Execute-Methode (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (java.lang.String.java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9451c7c2-4c0d-4d1e-9b42-a26ff28e3f6a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4f566b1832ed88e933533f47b0b532fdc45bee1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="execute-method-javalangstring-javalangstring"></a>Execute-Methode (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Führt die angegebene SQL-Anweisung, der mehrere Ergebnisse, und signalisiert zurückgegeben werden können [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] , dass die automatisch generierten Schlüssel, die im angegebenen Array angegeben sind zum Abrufen verfügbar gemacht werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final boolean execute(java.lang.String sql,  
                             java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sql*  
  
 Ein **Zeichenfolge** , die eine SQL-Anweisung enthält.  
  
 *"ColumnNames"*  
  
 Ein Zeichenfolgenarray, mit dem angegeben wird, welche Spaltennamen der automatisch generierten Schlüssel verfügbar gemacht werden sollen.  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** , wenn das erste Ergebnis ein Resultset handelt. Andernfalls lautet der Wert **false**.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese Execute-Methode wird von der Execute-Methode in der java.sql.Statement-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Execute-Methode &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
