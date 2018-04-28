---
title: GetColumns-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f173fa5d-e114-4a37-a5c4-2baad9ff3af1
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d6b0df43a82b288f475c1325c66670cf6290933
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="getcolumns-method-sqlserverdatabasemetadata"></a>getColumns-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der Tabellenspalten ab, die im angegebenen Katalog verfügbar sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getColumns(java.lang.String catalog,  
                                     java.lang.String schema,  
                                     java.lang.String table,  
                                     java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parameter  
 *catalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
 *schema*  
  
 Ein **Zeichenfolge** , die dem schemanamenmuster enthält.  
  
 *table*  
  
 Ein **Zeichenfolge** , der dem Namensmuster für die Tabelle enthält.  
  
 *Spalten-Nr*  
  
 Ein **Zeichenfolge** , der dem Namensmuster für die Spalte enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetColumns-Methode wird von der GetColumns-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 GetColumns-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Der Katalogname.|  
|TABLE_SCHEM|**String**|Der Tabellenschemaname.|  
|table_name|**String**|Der Tabellenname.|  
|COLUMN_NAME|**String**|Der Spaltenname.|  
|DATA_TYPE|**smallint**|Der SQL-Datentyp aus "java.sql.Types".|  
|TYPE_NAME|**String**|Der Name des Datentyps.|  
|COLUMN_SIZE|**int**|Die Genauigkeit der Spalte.|  
|BUFFER_LENGTH|**smallint**|Die Übertragungsgröße der Daten.|  
|DECIMAL_DIGITS|**smallint**|Die Dezimalstellen der Spalte.|  
|NUM_PREC_RADIX|**smallint**|Die Basis der Spalte.|  
|NULLABLE|**smallint**|Gibt an, ob die Spalte NULL-Werte zulässt. Mögliche Werte:<br /><br /> columnNoNulls (0)<br /><br /> columnNullable (1)|  
|REMARKS|**String**|Die der Spalte zugeordneten Kommentare.<br /><br /> **Hinweis:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] gibt immer null für diese Spalte zurück.|  
|COLUMN_DEF|**String**|Der Standardwert der Spalte.|  
|SQL_DATA_TYPE|**smallint**|Der Wert des SQL-Datentyps, wie er im TYPE-Feld des Deskriptors angezeigt wird. Diese Spalte entspricht der DATA_TYPE-Spalte mit Ausnahme des datetime-Datentyps und des SQL-92-Datentyps interval. Diese Spalte gibt immer einen Wert zurück.|  
|SQL_DATETIME_SUB|**smallint**|Untertypcode für den datetime-Datentyp und den SQL-92-Datentyp interval. Bei allen anderen Datentypen gibt diese Spalte NULL zurück.|  
|CHAR_OCTET_LENGTH|**int**|Die maximale Anzahl von Bytes in der Spalte.|  
|ORDINAL_POSITION|**int**|Der Index der Spalte innerhalb der Tabelle.|  
|IS_NULLABLE|**String**|Gibt an, ob in der Spalte NULL-Werte zulässig sind.|  
|SS_IS_SPARSE|**smallint**|Wenn die Spalte eine Spalte mit geringer Dichte ist, hat dies den Wert 1; andernfalls 0. <sup>1</sup>|  
|SS_IS_COLUMN_SET|**smallint**|Besitzt den Wert 1, wenn die Spalte die column_set-Sparsespalte ist, andernfalls 0. <sup>1</sup>|  
|SS_IS_COMPUTED|**smallint**|Zeigt an, ob eine TABLE_TYPE-Spalte eine berechnete Spalte ist. <sup>1</sup>|  
|IS_AUTOINCREMENT|**String**|"YES", wenn die Spalte automatisch inkrementiert wird. "NO", wenn die Spalte nicht automatisch inkrementiert wird. "" (leere Zeichenfolge), wenn vom Treiber nicht ermittelt werden kann, ob die Spalte automatisch inkrementiert wird. <sup>1</sup>|  
|SS_UDT_CATALOG_NAME|**String**|Der Name des Katalogs, der den benutzerdefinierten Typ (UDT) enthält. <sup>1</sup>|  
|SS_UDT_SCHEMA_NAME|**String**|Der Name des Schemas, der den benutzerdefinierten Typ (UDT) enthält. <sup>1</sup>|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|Der benutzerdefinierte Typ (UDT) für den vollqualifizierten Namen. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|Der Name des Katalogs, in dem ein XML-schemaauflistungsname definiert ist. Wenn der Katalogname nicht gefunden werden kann, enthält diese Variable eine leere Zeichenfolge. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|Der Name des Schemas, in dem eine XML-Schemaauflistung definiert ist. Wenn der Schemaname nicht gefunden werden kann, handelt es sich dabei um eine leere Zeichenfolge. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|Name der XML-Schemaauflistung. Wenn der Name nicht gefunden werden kann, ist dies eine leere Zeichenfolge. <sup>1</sup>|  
|SS_DATA_TYPE|**tinyint**|Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -Datentyp, mit der erweiterten gespeicherten Prozeduren.<br /><br /> **Hinweis** für Weitere Informationen zu den Datentypen zurückgegebenes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], finden Sie unter "Datentypen (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.|  
  
 (1) diese Spalte wird nicht vorhanden sein, wenn Sie Herstellen einer Verbindung mit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)].  
  
> [!NOTE]  
>  Weitere Informationen zu den Daten, die von der GetColumns-Methode zurückgegebene finden Sie unter "Sp_columns (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
 In der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 sehen, da Sie das folgende Verhalten ändert sich von früheren Versionen des JDBC-Treibers:  
  
 Die DATA_TYPE-Spalte wurde folgendermaßen geändert:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp|Rückgabetyp in JDBC Driver 2.0 (oder, wenn es sich bei einer Verbindung mit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]) und zugeordnete numerische Konstante|Rückgabetyp in JDBC Driver 3.0 beim Verbinden mit [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] oder höher|  
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|  
|benutzerdefinierter, 8 KB überschreitender Typ|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geography|LONGVARBINARY (-4)|VARBINARY (-3)|  
|Geometrie|LONGVARBINARY (-4)|VARBINARY (-3)|  
|varbinary(max)|LONGVARBINARY (-4)|VARBINARY (-3)|  
|nvarchar(max)|LONGVARCHAR (-1) oder LONGNVARCHAR (JDBC 4) (-16)|VARCHAR (12) oder NVARCHAR (JDBC 4) (-9)|  
|varchar(max)|LONGVARCHAR (-1)|VARCHAR (12)|  
|Uhrzeit|VARCHAR (12) oder NVARCHAR (JDBC 4) (-9)|TIME (-154)|  
|Datum|VARCHAR (12) oder NVARCHAR (JDBC 4) (-9)|DATE (91)|  
|datetime2|VARCHAR (12) oder NVARCHAR (JDBC 4) (-9)|TIMESTAMP (93)|  
|datetimeoffset|VARCHAR (12) oder NVARCHAR (JDBC 4) (-9)|microsoft.sql.Types.DATETIMEOFFSET (-155)|  
  
 Die COLUMN_SIZE-Spalte wurde folgendermaßen geändert:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp|Rückgabetyp in JDBC Driver 2.0|Rückgabetyp in JDBC Driver 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|nvarchar(max)|1073741823|2147483647 (Datenbankmetadaten)|  
|xml|1073741823|2147483647 (Datenbankmetadaten)|  
|benutzerdefinierter Typ mit weniger oder genau 8 KB|8 KB (Resultset- und Parametermetadaten)|Die tatsächliche von der gespeicherten Prozedur zurückgegebene Größe|  
|Uhrzeit||Die Länge (in Zeichen) der Zeichenfolgendarstellung des Typs, wobei die maximal zulässige Genauigkeit der Komponente für Sekundenbruchteile vorausgesetzt wird.|  
|Datum||entspricht "time"|  
|datetime2||entspricht "time"|  
|datetimeoffset||entspricht "time"|  
  
 Die BUFFER_LENGTH-Spalte wurde folgendermaßen geändert:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp|Rückgabetyp in JDBC Driver 2.0|Rückgabetyp in JDBC Driver 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|benutzerdefinierter, 8 KB überschreitender Typ||2147483647|  
  
 Die TYPE_NAME-Spalte wurde folgendermaßen geändert:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp|Rückgabetyp in JDBC Driver 2.0|Rückgabetyp in JDBC Driver 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|varchar(max)|text|varchar|  
|varbinary(max)|image|varbinary|  
  
 Die DECIMAL_DIGITS-Spalte wurde folgendermaßen geändert:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-Typ|JDBC Driver 2.0|JDBC Driver 3.0|  
|--------------------------------------------------------------|---------------------|---------------------|  
|Uhrzeit|NULL|7 (oder – falls angegeben – kleiner)|  
|Datum|NULL|NULL|  
|datetime2|NULL|7 (oder – falls angegeben – kleiner)|  
|datetimeoffset|NULL|7 (oder – falls angegeben – kleiner)|  
  
 Die SQL_DATA_TYPE-Spalte wurde folgendermaßen geändert:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 2008-Datenwert in JDBC Driver 2.0|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 2008-Datenwert in JDBC Driver 3.0|  
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|varchar(max)|-10|-9|  
|nvarchar(max)|-1|-9|  
|xml|-10|-152|  
|benutzerdefinierter Typ mit weniger oder genau 8 KB|-3|-151|  
|benutzerdefinierter, 8 KB überschreitender Typ|Nicht verfügbar in JDBC Driver 2.0|-151|  
|geography|-4|-151|  
|Geometrie|-4|-151|  
|hierarchyid|-4|-151|  
|Uhrzeit|-9|92|  
|Datum|-9|91|  
|datetime2|-9|93|  
|datetimeoffset|-9|-155|  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetColumns-Methode zum Zurückgeben von Informationen für die Tabelle "Person.Contact" in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank.  
  
```  
import java.sql.*;  
public class c1 {  
   public static void main(String[] args) {  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedsecurity=true";  
  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         DatabaseMetaData dbmd = con.getMetaData();  
         rs = dbmd.getColumns("AdventureWorks", "Person", "Contact", "FirstName");  
  
         ResultSet r = dbmd.getColumns(null, null, "Contact", null);  
         ResultSetMetaData rm = r.getMetaData();   
         int noofcols = rm.getColumnCount();  
  
         if (r.next())  
            for (int i = 0 ; i < noofcols ; i++ )  
            System.out.println(rm.getColumnName( i + 1 ) + ": \t\t" + r.getString( i + 1 ));  
      }  
  
      catch (Exception e) {}  
      finally {}  
   }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Methoden](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
