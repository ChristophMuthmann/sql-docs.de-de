---
title: GetProcedureColumns-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
apiname: SQLServerDatabaseMetaData.getProcedureColumns
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d8fa1fbb84392dba636c8aa5649f45cd54e397d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="getprocedurecolumns-method-sqlserverdatabasemetadata"></a>getProcedureColumns-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der Parameter gespeicherter Prozeduren und Ergebnisspalten ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getProcedureColumns(java.lang.String sCatalog,  
                                              java.lang.String sSchema,  
                                              java.lang.String proc,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parameter  
 *sCatalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs. Durch Festlegen dieses Parameters auf NULL wird angegeben, dass der Katalogname nicht verwendet werden muss.  
  
 *%sder*  
  
 Ein **Zeichenfolge** , die dem schemanamenmuster enthält. Durch Festlegen dieses Parameters auf NULL wird angegeben, dass der Schemaname nicht verwendet werden muss.  
  
 *proc*  
  
 Ein **Zeichenfolge** , die dem prozedurnamenmuster enthält.  
  
 *Spalten-Nr*  
  
 Ein **Zeichenfolge** , der dem Namensmuster für die Spalte enthält. Wird für diesen Parameter NULL angegeben, wird für jede Spalte eine Zeile zurückgegeben.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetProcedureColumns-Methode wird von der GetProcedureColumns-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Durch die GetProcedureColumns-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|Der Name der Datenbank, in der sich die angegebene gespeicherte Prozedur befindet.|  
|PROCEDURE_SCHEM|**String**|Das Schema für die gespeicherte Prozedur.|  
|PROCEDURE_NAME|**String**|Der Name der gespeicherten Prozedur.|  
|COLUMN_NAME|**String**|Name der Spalte.|  
|COLUMN_TYPE|**kurze**|Der Typ der Spalte. Mögliche Werte:<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|Der SQL-Datentyp aus "java.sql.Types".|  
|TYPE_NAME|**String**|Der Name des Datentyps.|  
|PRECISION|**int**|Die Gesamtanzahl von signifikanten Stellen.|  
|LENGTH|**int**|Die Länge der Daten in Bytes.|  
|SCALE|**kurze**|Die Anzahl der Ziffern rechts vom Dezimaltrennzeichen.|  
|RADIX|**kurze**|Die Basis für numerische Typen.|  
|NULLABLE|**kurze**|Gibt an, ob die Spalte einen NULL-Wert enthalten kann. Mögliche Werte:<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|REMARKS|**String**|Die Beschreibung der Prozedurspalte.<br /><br /> <br /><br /> **Hinweis:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] keinen Wert für diese Spalte zurückgibt.|  
|COLUMN_DEF|**String**|Der Standardwert der Spalte.|  
|SQL_DATA_TYPE|**smallint**|Diese Spalte ist identisch mit der **DATA_TYPE** Spalte, mit Ausnahme der **"DateTime"** und ISO **Intervall** Datentypen.|  
|SQL_DATETIME_SUB|**smallint**|Die **"DateTime"** ISO **Intervall** subcode, wenn der Wert der **SQL_DATA_TYPE** ist **SQL_DATETIME** oder **SQL_INTERVAL**. Bei allen Datentypen außer **"DateTime"** und ISO **Intervall**, ist diese Spalte NULL.|  
|CHAR_OCTET_LENGTH|**int**|Die maximale Anzahl von Bytes in der Spalte.|  
|ORDINAL_POSITION|**int**|Der Index der Spalte innerhalb der Tabelle.|  
|IS_NULLABLE|**String**|Gibt an, ob in der Spalte NULL-Werte zulässig sind.|  
|SS_TYPE_CATALOG_NAME|**String**|Der Name des Katalogs, der den benutzerdefinierten Typ (UDT) enthält.|  
|SS_TYPE_SCHEMA_NAME|**String**|Der Name des Schemas, der den benutzerdefinierten Typ (UDT) enthält.|  
|SS_UDT_CATALOG_NAME|**String**|Der benutzerdefinierte Typ (UDT) für den vollqualifizierten Namen.|  
|SS_UDT_SCHEMA_NAME|**String**|Der Name des Katalogs, in dem ein XML-schemaauflistungsname definiert ist. Wenn der Katalogname nicht gefunden werden kann, enthält diese Variable eine leere Zeichenfolge.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|Der Name des Schemas, in dem eine XML-Schemaauflistung definiert ist. Wenn der Schemaname nicht gefunden werden kann, handelt es sich dabei um eine leere Zeichenfolge.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|Name der XML-Schemaauflistung. Wenn der Name nicht gefunden werden kann, ist dies eine leere Zeichenfolge.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|Der Name des Katalogs, der den benutzerdefinierten Typ (UDT) enthält.|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|Der Name des Schemas, der den benutzerdefinierten Typ (UDT) enthält.|  
|SS_DATA_TYPE|**tinyint**|Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -Datentyp, mit der erweiterten gespeicherten Prozeduren.<br /><br /> <br /><br /> **Hinweis:** für Weitere Informationen zu den Datentypen zurückgegebenes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], finden Sie unter "Datentypen (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.|  
  
> [!NOTE]  
>  Weitere Informationen zu den Daten, die von der GetProcedureColumns-Methode zurückgegebene finden Sie unter "Sp_sproc_columns (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetProcedureColumns-Methode zum Zurückgeben von Informationen über die gespeicherte Prozedur UspGetBillOfMaterials in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank.  
  
```  
public static void executeGetProcedureColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedureColumns(null, null, "uspGetBillOfMaterials", null);  
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
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
