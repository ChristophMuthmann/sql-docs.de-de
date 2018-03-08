---
title: GetPrimaryKeys-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
apiname: SQLServerDatabaseMetaData.getPrimaryKeys
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: ebfe236a-dc02-493e-a3ab-5353d3769e36
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4dad2aa3d1f423b623970b7bb21673d27fb6616c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getprimarykeys-method-sqlserverdatabasemetadata"></a>getPrimaryKeys-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der Primärschlüsselspalten der angegebenen Tabelle ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getPrimaryKeys(java.lang.String cat,  
                                         java.lang.String schema,  
                                         java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parameter  
 *CAT*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
 *Schema*  
  
 Ein **Zeichenfolge** , die den Schemanamen enthält.  
  
 *table*  
  
 Ein **Zeichenfolge** , die den Tabellennamen enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetPrimaryKeys-Methode wird von der GetPrimaryKeys-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Durch die GetPrimaryKeys-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|String|Der Name der Datenbank, in der die angegebene Tabelle befindet.|  
|TABLE_SCHEM|String|Das Schema der Tabelle.|  
|TABLE_NAME|String|Der Name der Tabelle.|  
|COLUMN_NAME|String|Name der Spalte.|  
|KEY_SEQ|short|Die Sequenznummer der Spalte bei einem Primärschlüssel, der durch mehrere Spalten definiert wird.|  
|PK_NAME|String|Der Name des Primärschlüssels.|  
  
> [!NOTE]  
>  Weitere Informationen zu den Daten, die von der GetPrimaryKeys-Methode zurückgegebene finden Sie unter "Sp_pkeys (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetPrimaryKeys-Methode zum Zurückgeben von Informationen zu den Primärschlüsseln der Tabelle Person.Contact in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank.  
  
```  
public static void executeGetPrimaryKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getPrimaryKeys("AdventureWorks", "Person", "Contact");  
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
  
  
