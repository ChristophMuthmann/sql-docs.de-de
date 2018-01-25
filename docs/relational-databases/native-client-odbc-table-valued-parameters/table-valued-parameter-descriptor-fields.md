---
title: "Deskriptorfelder für Tabellenwertparameter | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: table-valued parameters (ODBC), descriptor fields
ms.assetid: 4e009eff-c156-4d63-abcf-082ddd304de2
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfea7aa106988fc0b188dd1f1eb9da0efb206b33
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="table-valued-parameter-descriptor-fields"></a>Deskriptorfelder für Tabellenwertparameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die Unterstützung für Tabellenwertparameter bietet neue, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifische Felder in ODBC-Anwendungsparameterdeskriptoren (Application Parameter Descriptor, APD) und Implementierungsparameterdeskriptoren (Implementation Parameter Descriptor, IPD).  
  
## <a name="remarks"></a>Hinweise  
  
|Name|Speicherort|Typ|Description|  
|----------|--------------|----------|-----------------|  
|SQL_CA_SS_TYPE_NAME|IPD|SQLTCHAR*|Der Servertypname des Tabellenwertparameters.<br /><br /> Wenn ein Tabellenwertparameter-Typnamen bei einem Aufruf von SQLBindParameter angegeben ist, muss es als Unicode-Wert, auch bei Anwendungen angegeben werden, die als ANSI-Anwendungen erstellt werden. Der Wert für den Parameter verwendet *StrLen_or_IndPtr* sollte entweder SQL_NTS oder die Länge der Zeichenfolge multipliziert mit sizeof(WCHAR) sein.<br /><br /> Wird erstellt, wenn ein Tabellenwertparameter-Typname angegeben über SQLSetDescField, mit ein, die die Art und Weise der Anwendung kompatibles Literal angegeben werden können. Der ODBC-Treiber-Manager führt die eventuell erforderliche Unicode-Konvertierung aus.|  
|SQL_CA_SS_TYPE_CATALOG_NAME (schreibgeschützt)|IPD|SQLTCHAR*|Der Katalog, in dem der Typ definiert ist.|  
|SQL_CA_SS_TYPE_SCHEMA_NAME|IPD|SQLTCHAR*|Das Schema, in dem der Typ definiert ist.|  
  
 Anwendungen dürfen für Tabellenwertparameter SQL_CA_SS_TYPE_CATALOG_NAME nicht festlegen. Andernfalls werden ein SQL_ERROR und ein Diagnosedatensatz mit SQLSTATE = HY091 und der Meldung "Ungültiger Deskriptorfeldbezeichner" zurückgegeben.  
  
 Die folgenden Anweisungsattribute und Deskriptorheaderfelder gelten für Tabellenwertparameter, wenn der Parameterfokus auf einen Tabellenwertparameter festgelegt ist:  
  
|Name|Speicherort|Typ|Description|  
|----------|--------------|----------|-----------------|  
|SQL_ATTR_PARAMSET_SIZE<br /><br /> (Dies entspricht SQL_DESC_ARRAY_SIZE im APD.)|APD|SQLUINTEGER|Die Arraygröße der Pufferarrays für einen Tabellenwertparameter. Dies entspricht der maximalen Anzahl an Zeilen, die die Puffer enthalten können, oder der Größe der Puffer in Zeilen ausgedrückt. Der Wert des Tabellenwertparameters selbst kann darüber- oder darunterliegen. Standard ist 1.<br /><br /> Hinweis: Wenn SQL_SOPT_SS_PARAM_FOCUS auf den Standardwert 0 festgelegt ist, verweist SQL_ATTR_PARAMSET_SIZE bezieht sich auf die Anweisung und gibt die Anzahl von Parametersätzen an. Wenn SQL_SOPT_SS_PARAM_FOCUS auf die Ordnungszahl eines Tabellenwertparameters festgelegt ist, verweist das Attribut auf den Tabellenwertparameter und gibt die Anzahl der Zeilen pro Parameterset des Tabellenwertparameters an.|  
|SQL_ATTR_PARAM _BIND_TYPE|APD|SQLINTEGER|Der Standard ist SQL_PARAM_BIND_BY_COLUMN.<br /><br /> Zum Auswählen der zeilenbezogenen Bindung wird dieses Feld auf die Länge der Struktur oder die Instanz eines Puffers festgelegt, der an einen Satz von Tabellenwert-Parameterzeilen gebunden wird. Die Längenangabe muss Platz für alle gebundenen Spalten und möglicherweise vorhandene Auffüllzeichen der Struktur bzw. des Puffers vorsehen. Auf diese Weise wird sichergestellt, dass bei einer um eine angegebene Länge inkrementierten Adresse einer gebundenen Spalte das Ergebnis auf den Anfang derselben Spalte in der nächsten Zeile zeigt. Bei Verwendung der **"sizeof"** -Operator in ANSI C, wird dieses Verhalten garantiert.|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|APD|SQLINTEGER*|Der Standardwert ist ein NULL-Zeiger.<br /><br /> Wenn dieses Feld nicht NULL ist, hebt der Treiber den Verweis auf den Zeiger auf, fügt den verweislosen Wert jedem der zurückgestellten Felder im Deskriptordatensatz (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR und SQL_DESC_OCTET_LENGTH_PTR) hinzu und verwendet die neuen Zeigerwerte, um auf die Datenwerte zuzugreifen.|  
  
 Diese Felder sind nur mit Tabellenwertparametern gültig und werden für andere Datentypen ignoriert.  
  
 SQL_CA_SS_TYPE_NAME ist für Aufrufe von gespeicherten Prozeduren optional. SQL_CA_SS_TYPE_NAME muss für SQL-Anweisungen angegeben werden, die keine Prozeduraufrufe sind, damit der Server den Typ des Tabellenwertparameters ermitteln kann.  
  
 Wenn der Name des Typs erforderlich ist und der Tabellentyp des Tabellenwertparameters in einem anderen Schema definiert ist als die gespeicherte Prozedur, muss SQL_CA_SS_TYPE_SCHEMA_NAME im Implementierungsparameterdeskriptor (Implementation Parameter Descriptor, IPD) angegeben werden. Andernfalls ist der Server nicht in der Lage, den Typ des Tabellenwertparameters zu ermitteln. Dies führt zu einem Fehler beim Aufrufen des SQLExecute oder SQLExecDirect. Der Fehler ist SQLSTATE = 07006 und enthält die Meldung "Attributverletzung beschränkter Datentypen".  
  
 Tabellenwert-Parameterspalten können entweder zeilenweise oder spaltenweise Bindungen verwenden. Der Standard ist die spaltenweise Bindung. Die Zeilenweise Bindung kann angegeben werden, indem SQL_ATTR_PARAM_BIND_TYPE und SQL_ATTR_ PARAM_BIND_OFFSET_PTR festgelegt werden. Dies entspricht der zeilenweisen Bindung von Spalten und Parametern.  
  
 SQL_CA_SS_TYPE_CATALOG_NAME und SQL_CA_SS_TYPE_SCHEMA_NAME können auch verwendet werden, um den Katalog und das Schema abzurufen, die mit Parametern des CLR-benutzerdefinierten Typs verbunden sind. Dabei handelt es sich um Alternativen zu den vorhandenen typspezifischen Katalogschemaattributen für diese Typen.  
  
## <a name="see-also"></a>Siehe auch  
 [Table-Valued Parameters &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
