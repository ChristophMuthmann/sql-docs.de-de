---
title: GetTypeInfo-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getTypeInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 23208f01-c1bf-4235-b29c-9051d3df59a3
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 032ddf6a5f266fa68c6a735dd7f59cf4df02c68e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="gettypeinfo-method-sqlserverdatabasemetadata"></a>getTypeInfo-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung aller standardmäßigen SQL-Typen ab, die von der aktuellen Datenbank unterstützt werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getTypeInfo()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetTypeInfo-Methode wird vom GetTypeInfo-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Die vom GetTypeInfo-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|TYPE_NAME|**String**|Der Name des Datentyps.|  
|DATA_TYPE|**short**|Der SQL-Datentyp aus "java.sql.Types".|  
|PRECISION|**int**|Die Gesamtanzahl von signifikanten Stellen.|  
|LITERAL_PREFIX|**String**|Die Zeichen, die einer Konstante vorangestellt werden.|  
|LITERAL_SUFFIX|**String**|Die Zeichen, die eine Konstante beenden.|  
|CREATE_PARAMS|**String**|Die Beschreibung der Erstellungsparameter für den Datentyp.|  
|NULLABLE|**short**|Gibt an, ob die Spalte einen NULL-Wert enthalten kann. Mögliche Werte:<br /><br /> typeNoNulls (0)<br /><br /> typeNullable (1)<br /><br /> typeNullableUnknown (2)|  
|CASE_SENSITIVE|**boolean**|Gibt an, ob bei dem Datentyp die Groß-/Kleinschreibung berücksichtigt wird. "**" true "**"Wenn der Typ ist die Groß-/Kleinschreibung beachtet, andernfalls"**" false "**".|  
|SEARCHABLE|**short**|Gibt an, ob die Spalte in einer SQL-Klausel vom Typ "WHERE" verwendet werden kann. Mögliche Werte:<br /><br /> typePredNone (0)<br /><br /> typePredChar (1)<br /><br /> typePredBasic (2)<br /><br /> typeSeachable (3)|  
|UNSIGNED_ATTRIBUTE|**boolean**|Gibt das Vorzeichen des Datentyps an. "**" true "**"Wenn der Typ ohne Vorzeichen ist, andernfalls"**" false "**".|  
|FIXED_PREC_SCALE|**boolean**|Gibt an, dass es sich bei dem Datentyp um eine Währung handeln kann. "**" true "**" ist der Datentyp Währung handelt; andernfalls "**" false "**".|  
|AUTO_INCREMENT|**boolean**|Gibt an, dass der Datentyp automatisch inkrementiert werden kann. "**" true "**"Wenn "der Typ kann werden für automatisch inkrementiert wurde, andernfalls"**"false"**".|  
|LOCAL_TYPE_NAME|**String**|Der lokalisierte Name des Datentyps.|  
|MINIMUM_SCALE|**short**|Die maximale Anzahl von Stellen rechts des Dezimalzeichens.|  
|MAXIMUM_SCALE|**short**|Die Mindestanzahl von Stellen rechts des Dezimalzeichens.|  
|SQL_DATA_TYPE|**int**|Wird vom JDBC-Treiber nicht unterstützt.|  
|SQL_DATETIME_SUB|**int**|Wird vom JDBC-Treiber nicht unterstützt.|  
|NUM_PREC_RADIX|**int**|Die Anzahl von Bits oder Stellen zum Berechnen der höchsten Zahl, die eine Spalte enthalten kann.|  
|INTERVAL_PRECISION|**smallint**|Die Genauigkeit für anführenden Intervallwert.|  
|USERTYPE|**smallint**|Die **Usertype** Wert aus der **Systypes** Tabelle. Weitere Informationen finden Sie in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-Onlinedokumentation.|  
  
> [!NOTE]  
>  Weitere Informationen zu den Daten, die vom GetTypeInfo-Methode zurückgegeben, finden Sie unter "Sp_datatype_info (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetTypeInfo-Methode zum Zurückgeben von Informationen zu den Datentypen in verwendet eine [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)] (oder höher) Datenbank.  
  
```  
public static void executeGetTypeInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTypeInfo();  
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
  
  
