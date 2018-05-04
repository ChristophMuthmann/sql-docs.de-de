---
title: GetImportedKeys-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getImportedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc8c1a5e-700e-4059-a5ed-5013bbb87fb6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de5ae39ff10c32737df637c9a6f29aab19d27574
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getimportedkeys-method-sqlserverdatabasemetadata"></a>getImportedKeys-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der Primärschlüsselspalten ab, auf die von den Fremdschlüsselspalten in einer Tabelle verwiesen wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.sql.ResultSet getImportedKeys(java.lang.String cat,  
                                          java.lang.String schema,  
                                          java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parameter  
 *CAT*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs.  
  
 *schema*  
  
 Ein **Zeichenfolge** , die den Schemanamen enthält.  
  
 *table*  
  
 Ein **Zeichenfolge** , die den Tabellennamen enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetImportedKeys-Methode wird von der GetImportedKeys-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Durch die GetImportedKeys-Methode zurückgegebene Resultset enthält die folgende Informationen:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**String**|Der Name des Katalogs, der die Primärschlüsseltabelle enthält.|  
|PKTABLE_SCHEM|**String**|Der Name des Schemas der Primärschlüsseltabelle.|  
|PKTABLE_NAME|**String**|Der Name der Primärschlüsseltabelle.|  
|PKCOLUMN_NAME|**String**|Der Spaltenname des Primärschlüssels.|  
|FKTABLE_CAT|**String**|Der Name des Katalogs, der die Fremdschlüsseltabelle enthält.|  
|FKTABLE_SCHEM|**String**|Der Name des Schemas der Fremdschlüsseltabelle.|  
|FKTABLE_NAME|**String**|Der Name der Fremdschlüsseltabelle.|  
|FKCOLUMN_NAME|**String**|Der Spaltenname des Fremdschlüssels.|  
|KEY_SEQ|**short**|Die Sequenznummer der Spalte bei einem Primärschlüssel, der durch mehrere Spalten definiert wird.|  
|UPDATE_RULE|**short**|Die auf den Fremdschlüssel angewendete Aktion, wenn es sich beim SQL-Vorgang um ein Update handelt. Mögliche Werte:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|Die auf den Fremdschlüssel angewendete Aktion, wenn es sich beim SQL-Vorgang um eine Löschung handelt. Mögliche Werte:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**String**|Der Name des Fremdschlüssels.|  
|PK_NAME|**String**|Der Name des Primärschlüssels.|  
|DEFERRABILITY|**short**|Zeigt an, ob die Auswertung der Fremdschlüsseleinschränkung bis zur Ausführung einer Commit-Aktion verzögert werden kann. Mögliche Werte:<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  Weitere Informationen zu den Daten, die von der GetImportedKeys-Methode zurückgegebene finden Sie unter "Sp_fkeys (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die GetImportedKeys-Methode verwenden, um Informationen zu allen Primärschlüsseln zurückgegeben, die die Fremdschlüssel der Person.Address-Tabelle in verweisen die [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] -Beispieldatenbank.  
  
```  
public static void executeGetImportedKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getImportedKeys("AdventureWorks", "Person", "Address");  
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
  
  
