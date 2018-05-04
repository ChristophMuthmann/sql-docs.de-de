---
title: GetTablePrivileges-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43bd46b81a6df2193181e4384b3b19d8d32c2929
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="gettableprivileges-method-sqlserverdatabasemetadata"></a>getTablePrivileges-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der Zugriffsrechte für die einzelnen Tabellen ab, die im angegebenen Katalog, Schema oder Tabellennamenmuster verfügbar sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getTablePrivileges(java.lang.String catalog,  
                                             java.lang.String schema,  
                                             java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parameter  
 *catalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs. Durch Festlegen dieses Parameters auf NULL wird angegeben, dass der Katalogname nicht verwendet werden muss.  
  
 *schema*  
  
 Ein **Zeichenfolge** , die dem schemanamenmuster enthält. Durch Festlegen dieses Parameters auf NULL wird angegeben, dass der Schemaname nicht verwendet werden muss.  
  
 *table*  
  
 Ein **Zeichenfolge** , der dem Namensmuster für die Tabelle enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetTablePrivileges-Methode wird von der GetTablePrivileges-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Durch die GetTablePrivileges-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Der Katalogname.|  
|TABLE_SCHEM|**String**|Der Tabellenschemaname.|  
|table_name|**String**|Der Tabellenname.|  
|GRANTOR|**String**|Das Objekt, von dem der Zugriff gewährt wird.|  
|GRANTEE|**String**|Das Objekt, von dem der Zugriff empfangen wird.|  
|PRIVILEGE|**String**|Der Typ des gewährten Zugriffs.|  
|IS_GRANTABLE|**String**|Gibt an, ob der Empfänger seinerseits anderen Benutzern Zugriff gewähren darf.|  
  
> [!NOTE]  
>  Weitere Informationen zu den Daten, die von der GetTablePrivileges-Methode zurückgegebene finden Sie unter "Sp_table_privileges (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetTablePrivileges-Methode zurückzugebenden die Zugriffsrechte für die Tabelle "Person.Contact" in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank.  
  
```  
public static void executeGetTablePrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTablePrivileges("AdventureWorks", "Person", "Contact");  
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
  
  
