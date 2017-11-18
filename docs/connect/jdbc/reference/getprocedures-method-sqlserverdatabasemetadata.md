---
title: GetProcedures-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3b1fb6671ac6f223b4e3dcc620f5f7144432abe8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getprocedures-method-sqlserverdatabasemetadata"></a>getProcedures-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der gespeicherten Prozeduren ab, die im angegebenen Katalog, Schema oder Namensmuster für gespeicherte Prozeduren verfügbar sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getProcedures(java.lang.String sCatalog,  
                                        java.lang.String sSchema,  
                                        java.lang.String proc)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sCatalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs. Durch Festlegen dieses Parameters auf NULL wird angegeben, dass der Katalogname nicht verwendet werden muss.  
  
 *%sder*  
  
 Ein **Zeichenfolge** , die dem schemanamenmuster enthält. Durch Festlegen dieses Parameters auf NULL wird angegeben, dass der Schemaname nicht verwendet werden muss.  
  
 *proc*  
  
 Ein **Zeichenfolge** , die dem prozedurnamenmuster enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetProcedures-Methode wird von der GetProcedures-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Die von der GetProcedures-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|Der Name der Datenbank, in der sich die angegebene gespeicherte Prozedur befindet.|  
|PROCEDURE_SCHEM|**String**|Das Schema für die gespeicherte Prozedur.|  
|PROCEDURE_NAME|**String**|Der Name der gespeicherten Prozedur.|  
|NUM_INPUT_PARAMS|**int**|Reserviert für zukünftige Verwendung. Gibt derzeit den Wert "-1" zurück.|  
|NUM_OUTPUT_PARAMS|**int**|Reserviert für zukünftige Verwendung. Gibt derzeit den Wert "-1" zurück.|  
|NUM_RESULT_SETS|**int**|Reserviert für zukünftige Verwendung. Gibt derzeit den Wert "-1" zurück.|  
|REMARKS|**String**|Die Beschreibung der Prozedurspalte.<br /><br /> <br /><br /> **Hinweis:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] keinen Wert für diese Spalte zurückgibt.  |  
|PROCEDURE_TYPE|**smallint**|Der Typ der gespeicherten Prozedur. Mögliche Werte:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
> [!NOTE]  
>  Weitere Informationen zu den Daten, die von der GetProcedures-Methode zurückgegebene finden Sie unter "Sp_stored_procedures (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetProcedures-Methode zum Zurückgeben von Informationen über die gespeicherte Prozedur UspGetBillOfMaterials in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank.  
  
```  
public static void executeGetProcedures(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedures(null, null, "uspGetBillOfMaterials");  
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
  
  

