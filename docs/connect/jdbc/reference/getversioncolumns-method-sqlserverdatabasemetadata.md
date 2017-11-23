---
title: GetVersionColumns-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
apiname: SQLServerDatabaseMetaData.getVersionColumns
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 6dd275d3-d9b2-4db7-938a-d4406c940a7a
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6adf8973efd40728df1604dcef9b4a87736be72c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getversioncolumns-method-sqlserverdatabasemetadata"></a>getVersionColumns-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der Spalten einer Tabelle ab, die automatisch aktualisiert wird, wenn ein Wert in einer Zeile aktualisiert wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getVersionColumns(java.lang.String catalog,  
                                            java.lang.String schema,  
                                            java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Katalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
 *Schema*  
  
 Ein **Zeichenfolge** , die dem schemanamenmuster enthält.  
  
 *table*  
  
 Ein **Zeichenfolge** , die den Tabellennamen enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetVersionColumns-Methode wird von der GetVersionColumns-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Durch die GetVersionColumns-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|SCOPE|**kurze**|Wird vom JDBC-Treiber nicht unterstützt.|  
|COLUMN_NAME|**String**|Der Spaltenname.|  
|DATA_TYPE|**kurze**|Der SQL-Datentyp aus "java.sql.Types".|  
|TYPE_NAME|**String**|Der Name des Datentyps.|  
|COLUMN_SIZE|**int**|Die Genauigkeit der Spalte.|  
|BUFFER_LENGTH|**int**|Die Länge der Spalten in Bytes.|  
|DECIMAL_DIGITS|**kurze**|Die Dezimalstellen der Spalte.|  
|PSEUDO_COLUMN|**kurze**|Gibt an, ob die Spalte eine Pseudospalte ist. Mögliche Werte:<br /><br /> versionColumnUnknown (0)<br /><br /> versionColumnNotPseudo (1)<br /><br /> versionColumnPseudo (2)|  
  
> [!NOTE]  
>  Weitere Informationen zu den Daten, die von der GetVersionColumns-Methode zurückgegebene finden Sie unter "Sp_datatype_info (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetVersionColumns-Methode zum Zurückgeben von Informationen zu den Spalten, die automatisch aktualisiert werden in der Person.Contact-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank.  
  
```  
public static void executeGetVersionColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getVersionColumns("AdventureWorks", "Person", "Contact");  
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
  
  
