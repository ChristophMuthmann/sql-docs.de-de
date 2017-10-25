---
title: GetFunctions-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0482197b706ac4e604fe6e4402bebbe1bc793fc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getfunctions-method-sqlserverdatabasemetadata"></a>getFunctions-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der System- und Benutzerfunktionen ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public ResultSet getFunctions(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Katalog*  
  
 Der Name eines Katalogs in der Datenbank. Bei einer leeren Zeichenfolge ("") enthält das Ergebnis die Funktionen ohne einen Katalog. Ist er **null**, der Name des Katalogs wird nicht für die Suche verwendet.  
  
 *schemaPattern*  
  
 Der Name eines Schemas. Bei einer leeren Zeichenfolge ("") enthält das Ergebnis die Funktionen ohne ein Schema. Ist er **null**, der Schemaname wird nicht für die Suche verwendet.  
  
 *functionNamePattern*  
  
 Der Name einer Funktion.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetFunctions-Methode wird von der GetFunctions-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Von dieser Methode werden nur die System- und Benutzerfunktionen zurückgegeben, die dem angegebenen Schema- und Funktionsnamen entsprechen.  
  
> [!IMPORTANT]  
>  Das zurückgegebene Resultset kann Funktionen enthalten, zu deren Ausführung der aufrufende Benutzer nicht berechtigt ist.  
  
 Jede Funktionsbeschreibung umfasst die folgenden Spalten:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|Der Name der Datenbank, in der die Funktion gespeichert ist.|  
|FUNCTION_SCHEM|**String**|Der Name des Schemas, in dem die Funktion gespeichert ist.|  
|FUNCTION_NAME|**String**|Der Name der Funktion.|  
|NUM_INPUT_PARAMS|**int**|Reserviert für zukünftige Verwendung. Gibt derzeit den Wert "-1" zurück.|  
|NUM_OUTPUT_PARAMS|**int**|Reserviert für zukünftige Verwendung. Gibt derzeit den Wert "-1" zurück.|  
|NUM_RESULT_SETS|**int**|Reserviert für zukünftige Verwendung. Gibt derzeit den Wert "-1" zurück.|  
|REMARKS|**String**|Kommentare zur Funktion.|  
|FUNCTION_TYPE|**kurze**|Der Typ der Funktion. Mögliche Werte:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
 Alle Beschreibungen im zurückgegebenen Resultset sind nach "FUNCTION_CAT", "FUNCTION_SCHEM", "FUNCTION_NAME" und "SPECIFIC_NAME" sortiert.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

