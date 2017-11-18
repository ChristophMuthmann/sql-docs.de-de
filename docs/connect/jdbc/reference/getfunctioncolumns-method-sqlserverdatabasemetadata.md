---
title: GetFunctionColumns-Methode (SQLServerDatabaseMetaData) | Microsoft Docs
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
ms.assetid: e2b0e0f7-717c-48e6-bcd2-a325d938a833
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1508d70610c47116a4aaf58063b0f4196459d3e4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getfunctioncolumns-method-sqlserverdatabasemetadata"></a>getFunctionColumns-Methode (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft eine Beschreibung der System- oder Benutzerfunktionsparameter des angegebenen Katalogs sowie den Rückgabetyp ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public ResultSet getFunctionColumns(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern  
                       java.lang.String columnNamePattern)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Katalog*  
  
 Ein **Zeichenfolge** , enthält der Name des Katalogs. Bei einer leeren Zeichenfolge ("") enthält das Ergebnis die Funktionen ohne einen Katalog. Ist er **null**, der Name des Katalogs wird nicht für die Suche verwendet.  
  
 *schemaPattern*  
  
 Ein **Zeichenfolge** , die dem schemanamenmuster enthält. Bei einer leeren Zeichenfolge ("") enthält das Ergebnis die Funktionen ohne ein Schema. Ist er **null**, der Schemaname wird nicht für die Suche verwendet.  
  
 *functionNamePattern*  
  
 Ein **Zeichenfolge** , die den Namen einer Funktion enthält.  
  
 *columnNamePattern*  
  
 Ein **Zeichenfolge** , die den Namen eines Parameters enthält.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Objekt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetFunctionColumns-Methode wird von der GetFunctionColumns-Methode in der java.sql.DatabaseMetaData-Schnittstelle angegeben.  
  
 Von dieser Methode werden nur die Funktionen und Parameter zurückgegeben, die dem angegebenen Schema, Funktions- und Parameternamen innerhalb des angegebenen Katalogs entsprechen.  
  
 Jede Zeile im Resultset enthält die folgenden Spalten für eine Parameterbeschreibung, eine Spaltenbeschreibung oder einen Rückgabetyp:  
  
|Name|Typ|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|Der Name der Datenbank, in der die Funktion gespeichert ist.|  
|FUNCTION_SCHEM|**String**|Das Schema für die Funktion.|  
|FUNCTION_NAME|**String**|Der Name der Funktion.|  
|COLUMN_NAME|**String**|Der Name eines Parameters oder einer Spalte.|  
|COLUMN_TYPE|**kurze**|**Der Typ der Spalte. Die folgenden Werte sind möglich:**<br /><br /> functionColumnUnknown (0): Unbekannter Typ<br /><br /> functionColumnIn (1): Eingabeparameter<br /><br /> functionColumnInOut (2): Eingabe-/Ausgabeparameter<br /><br /> functionColumnOut (3): Ausgabeparameter<br /><br /> functionReturn (4): Funktionsrückgabewert<br /><br /> functionColumnResult (5): Ein Parameter oder eine Spalte ist eine Spalte im Resultset.|  
|DATA_TYPE|**smallint**|Der SQL-Datentyp, Wert aus "java.SQL.Types".|  
|TYPE_NAME|**String**|Der Name des Datentyps.|  
|PRECISION|**int**|Die Gesamtanzahl von signifikanten Stellen.|  
|LENGTH|**int**|Die Länge der Daten in Bytes.|  
|SCALE|**kurze**|Die Anzahl der Ziffern rechts vom Dezimaltrennzeichen.|  
|RADIX|**kurze**|Die Basis für numerische Typen.|  
|NULLABLE|**kurze**|Gibt an, ob der Parameter oder Rückgabetyp Wert enthalten kann eine **null** Wert.<br /><br /> **Die folgenden Werte sind möglich:**<br /><br /> functionNoNulls (0): NULL-Wert ist nicht zulässig.<br /><br /> functionNullable (1): NULL-Wert ist zulässig.<br /><br /> functionNullableUnknown (2): Unbekannt|  
|REMARKS|**String**|Die Kommentare zu einer Spalte oder einem Parameter.|  
|COLUMN_DEF|**String**|Der Standardwert der Spalte.<br /><br /> **Hinweis:** diese Informationen sind verfügbar, mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] und JDBC-Treiber-spezifisch ist.|  
|SQL_DATA_TYPE|**smallint**|Diese Spalte ist identisch mit der **DATA_TYPE** Spalte, mit Ausnahme der **"DateTime"** und ISO **Intervall** Datentypen.<br /><br /> **Hinweis:** diese Informationen sind verfügbar, mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] und JDBC-Treiber-spezifisch ist.|  
|SQL_DATETIME_SUB|**smallint**|Die **"DateTime"** ISO **Intervall** subcode, wenn der Wert der **SQL_DATA_TYPE** ist **SQL_DATETIME** oder **SQL_INTERVAL**. Bei allen Datentypen außer **"DateTime"** und ISO **Intervall**, ist diese Spalte NULL.<br /><br /> **Hinweis:**diese Informationen sind verfügbar, mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] und JDBC-Treiber-spezifisch ist.|  
|CHAR_OCTET_LENGTH|**int**|Die maximale Länge von binären oder zeichenbasierten Parametern oder Spalten. Für andere Datentypen ist der Wert NULL.|  
|ORDINAL_POSITION|**int**|Stellt für Eingabe- und Ausgabeparameter die Position (beginnend mit "1") dar.<br /><br /> Für Resultsetspalten handelt es sich hierbei um die Position der Spalte im Resultset. Beginn ist der Wert "1".<br /><br /> Für den Rückgabewert ist der Wert "0".|  
|IS_NULLABLE|**String**|Bestimmt die NULL-Zulässigkeit eines Parameters oder einer Spalte.<br /><br /> Mögliche Werte:<br /><br /> **Ja**: der Parameter oder die Spalte kann NULL-Werte enthalten.<br /><br /> **NICHT**: der Parameter oder die Spalte kann keine NULL-Werte enthalten.<br /><br /> Leere Zeichenfolge (""): Unbekannt|  
|SS_TYPE_CATALOG_NAME|**String**|Der Name des Katalogs, der den benutzerdefinierten Typ (UDT) enthält.|  
|SS_TYPE_SCHEMA_NAME|**String**|Der Name des Schemas, der den benutzerdefinierten Typ (UDT) enthält.|  
|SS_UDT_CATALOG_NAME|**String**|Der benutzerdefinierte Typ (UDT) für den vollqualifizierten Namen.|  
|SS_UDT_SCHEMA_NAME|**String**|Der Name des Katalogs, in dem ein XML-schemaauflistungsname definiert ist. Wenn der Katalogname nicht gefunden werden kann, enthält diese Variable eine leere Zeichenfolge.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|Der Name des Schemas, in dem eine XML-Schemaauflistung definiert ist. Wenn der Schemaname nicht gefunden werden kann, handelt es sich dabei um eine leere Zeichenfolge.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|Name der XML-Schemaauflistung. Wenn der Name nicht gefunden werden kann, ist dies eine leere Zeichenfolge.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|Der Name des Katalogs, der den benutzerdefinierten Typ (UDT) enthält.|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|Der Name des Schemas, der den benutzerdefinierten Typ (UDT) enthält.|  
|SS_DATA_TYPE|**tinyint**|Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -Datentyp, mit der erweiterten gespeicherten Prozeduren.<br /><br /> **Hinweis** für Weitere Informationen zu den Datentypen zurückgegebenes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], finden Sie unter "Datentypen (Transact-SQL)" in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Books Online.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDatabaseMetaData-Elemente](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData-Klasse](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

