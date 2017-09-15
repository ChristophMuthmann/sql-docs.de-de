---
title: GetIndexInfo-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 028937d023b6cf899eb5fa47354cb0c5d21545bc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>getIndexInfo-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der Indizes und der Statistik für die angegebene Tabelle ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getIndexInfo(java.lang.String cat,  
                                       java.lang.String schema,  
                                       java.lang.String table,  
                                       boolean unique,  
                                       boolean approximate)  
```  
  
#### <a name="parameters"></a>Parameter  
 *CAT*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
 *Schema*  
  
 Ein **Zeichenfolge** , die den Schemanamen enthält.  
  
 *table*  
  
 Ein **Zeichenfolge** , die den Tabellennamen enthält.  
  
 *eindeutige*  
  
 **"true"** Wenn nur Indizes für individuelle Werte zurückgegeben werden. **"false"** , wenn alle Indizes zurückgegeben werden.  
  
 *Ungefähre*  
  
 **"true"** , wenn die Ergebnisse ungefähre oder veraltete Werte wiedergeben. **"false"** , wenn die Ergebnisse korrekt sind.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetIndexInfo-Methode wird von der GetIndexInfo-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Durch die GetIndexInfo-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Der Name der Datenbank, in der die angegebene Tabelle befindet.|  
|TABLE_SCHEM|**String**|Das Schema der Tabelle.|  
|TABLE_NAME|**String**|Der Name der Tabelle.|  
|NON_UNIQUE|**boolean**|Gibt an, ob die Indexwerte nicht eindeutig sein können.|  
|INDEX_QUALIFIER|**String**|Der Name des Indexbesitzers. Wenn für TYPE das tableIndexStatistic-Objekt eingetragen wird, entspricht er NULL.|  
|INDEX_NAME|**String**|Der Name des Index.|  
|TYPE|**kurze**|Der Typ des Indexes. Mögliche Werte:<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**kurze**|Die Ordinalposition der Spalte innerhalb des Indexes. Die erste Spalte im Index hat den Wert 1.|  
|COLUMN_NAME|**String**|Name der Spalte.|  
|ASC_OR_DESC|**String**|Der in der Indexsortierung verwendete Befehl. Mögliche Werte:<br /><br /> A (aufsteigend)<br /><br /> D (absteigend)<br /><br /> NULL (nicht anwendbar)<br /><br /> **Hinweis:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] gibt immer "A" zurück.  |  
|CARDINALITY|**int**|Die Anzahl der Zeilen in der Tabelle oder der eindeutigen Werte im Index|  
|PAGES|**int**|Die Anzahl der Seiten, die zum Speichern des Indexes oder der Tabelle verwendet werden.|  
|FILTER_CONDITION|**String**|Die Filter-Bedingung.<br /><br /> **Hinweis:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] gibt immer null zurück.  |  
  
> [!NOTE]  
>  Weitere Informationen zu den Daten, die von der GetIndexInfo-Methode zurückgegebene finden Sie unter "Sp_indexes (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetIndexInfo-Methode zum Zurückgeben von Informationen zu den Indizes und Statistiken der Person.Contact-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank.  
  
```  
public static void executeGetIndexInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getIndexInfo("AdventureWorks", "Person", "Contact", false, true);  
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
  
  
