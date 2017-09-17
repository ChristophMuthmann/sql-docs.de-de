---
title: GetBestRowIdentifier-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getBestRowIdentifier
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c19e9ca6-2a53-4a0c-91ab-80090c3f7229
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 09dee13a9a71b606aa630aac1716d43f6d38a1f2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getbestrowidentifier-method-sqlserverdatabasemetadata"></a>getBestRowIdentifier-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der optimalen Gruppe von Spalten einer Tabelle ab, durch die eine Zeile eindeutig identifiziert wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getBestRowIdentifier(java.lang.String catalog,  
                                               java.lang.String schema,  
                                               java.lang.String table,  
                                               int scope,  
                                               boolean nullable)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Katalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
 *Schema*  
  
 Ein **Zeichenfolge** , die den Schemanamen enthält.  
  
 *table*  
  
 Ein **Zeichenfolge** , die den Tabellennamen enthält.  
  
 *Bereich*  
  
 Ein **Int** , des relevanten Bereichs angibt. Die Werte können Folgendes enthalten:  
  
 bestRowTemporary (0)  
  
 bestRowTransaction (1)  
  
 bestRowSession (2)  
  
 *NULL-Werte zulässt*  
  
 **"true"** einbinden Spalten NULL-Werte zulässt. Andernfalls lautet der Wert **false**.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetBestRowIdentifier-Methode wird von der GetBestRowIdentifier-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Durch die GetBestRowIdentifier-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|SCOPE|short|Der Bereich der zurückgegebenen Ergebnisse. Mögliche Werte:<br /><br /> bestRowTemporary (0)<br /><br /> bestRowTransaction (1)<br /><br /> bestRowSession (2)|  
|COLUMN_NAME|String|Name der Spalte.|  
|DATA_TYPE|short|Der SQL-Datentyp aus "java.sql.Types".|  
|TYPE_NAME|String|Der Name des Datentyps.|  
|COLUMN_SIZE|int|Die Genauigkeit der Spalte.|  
|BUFFER_LENGTH|int|Die Pufferlänge.|  
|DECIMAL_DIGITS|short|Die Dezimalstellen der Spalte.|  
|PSEUDO_COLUMN|short|Gibt an, ob die Spalte eine Pseudospalte ist. Mögliche Werte:<br /><br /> bestRowUnknown (0)<br /><br /> bestRowNotPseudo (1)<br /><br /> bestRowPseudo (2)|  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetBestRowIdentifier-Methode zum Zurückgeben von Informationen zum geeignetsten Zeilenidentifizierer für die Tabelle "Person.Contact" in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank.  
  
```  
public static void executeGetBestRowIdentifier(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getBestRowIdentifier(null, "Person", "Contact", 0, true);  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }  
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
