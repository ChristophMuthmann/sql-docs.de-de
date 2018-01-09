---
title: "Deskriptorfelder für Tabellenwertparameter-Spalten | Microsoft Docs"
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
helpviewer_keywords: table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c274a80980586881aa5faf2b2490acec7b97b7c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>Deskriptorfelder für aus Tabellenwertparameter bestehenden Spalten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die in diesem Abschnitt beschriebenen deskriptorfelder für Tabellenwertparameter werden mit bearbeitet [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) und [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) mit dem Handle für die Implementierung Parameter Descriptor ( IPD).  
  
## <a name="remarks"></a>Hinweise  
 SQL_DESC_AUTO_UNIQUE_VALUE wird für Tabellenwertparameter sowie für andere Funktionen verwendet.  
  
|Attributname|Typ|Description|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE gibt an, dass es sich bei dieser Spalte um eine Identitätsspalte handelt.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]können diese Informationen verwenden, um die Leistung zu optimieren sind, Anwendungen jedoch nicht für Identitätsspalten festlegen.|  
  
 Die folgenden Attribute werden allen Parametertypen im Anwendungsparameterdeskriptor (Application Parameter Descriptor, APD) und Implementierungsparameterdeskriptor (Implementation Parameter Descriptor, IPD) hinzugefügt:  
  
|Attributname|Typ|Description|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE gibt an, dass diese Spalte berechnet wird.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]können diese Informationen verwenden, um die Leistung zu optimieren sind, Anwendungen jedoch nicht für berechnete Spalten festlegen.<br /><br /> Dieses Attribut wird für Bindungen ignoriert, die keine Tabellenwertparameter-Spalten sind.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE gibt an, dass eine Tabellenwertparameter-Spalte zu einem eindeutigen Schlüssel gehört. Dies kann zu einer verbesserten Abfrageleistung führen. Dieses Attribut wird für Bindungen ignoriert, die keine Tabellenwertparameter-Spalten sind.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|Gibt die Sortierreihenfolge einer Tabellenwertparameter-Spalte an. Dies kann zu einer verbesserten Abfrageleistung führen. Dieses Attribut wird für Bindungen ignoriert, die keine Tabellenwertparameter-Spalten sind. Die möglichen Werte sind folgende: <br />**SQL_SS_ASCENDING_ORDER**<br />**SQL_SS_DESCENDING_ORDER**<br />**SQL_SS_ORDER_UNSPECIFIED**<br /><br /> Andere Werte als **SQL_SS_ASCENDING_ORDER** und **SQL_SS_DESCENDING_ORDER** erzeugen einen Fehler mit **SQLSTATE HY024** Meldung 'Ungültiger Attributwert', und sind als behandelt **SQL_SS_ORDER_UNSPECIFIED**, dies ist der Standardwert für dieses Attribut.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|Gibt die Ordnungszahl einer Tabellenwertparameter-Spalte in einer Gruppe von Spalten an, die die Gesamtreihenfolge für einen Tabellenwertparameter festlegt. Dies kann zu einer verbesserten Abfrageleistung führen. Dieses Attribut wird für Bindungen ignoriert, die keine Tabellenwertparameter-Spalten sind. Die Sortierung der Ordinalzahlen beginnt bei 1. Der Wert 0 ist der Standardwert und gibt eine Tabellenwertparameter-Spalte an, für die keine Spaltenreihenfolge angegeben wurde.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|Gibt an, ob alle Zeilen im Tabellenwertparameter den Standardwert für diese Spalte enthalten. Für Tabellenwertparameter ist es nicht möglich, den Standardwert auf Zeilenbasis auszuwählen. Der Wert SQL_FALSE gibt an, dass Zeilen nicht standardmäßige Werte enthalten. Dies ist die Standardeinstellung. Der Wert SQL_TRUE gibt an, dass diese Spalte Standardwerte für alle Zeilen enthält.<br /><br /> Wurde der Wert auf SQL_TRUE festgelegt, werden keine Daten an den Server gesendet.<br /><br /> Dieses Feld kann auch mit Identitätsspalten oder berechneten Spalten verwendet werden, wenn die Spaltenwerte nicht für die Serververarbeitung erforderlich sind.|  
  
 Diese Attribute sind nur für Tabellenwertparameter-Spalten gültig. Sie werden für andere Parameter ignoriert.  
  
 Wenn SQL_CA_SS_COL_HAS_DEFAULT_VALUE für eine Tabellenwertparameter-Spalte festgelegt wurde, muss SQL_DESC_DATA_PTR für diese Spalte ein NULL-Zeiger sein. Andernfalls gibt SQLExecute oder SQLExecDirect SQL_ERROR zurück. Generiert ein Diagnosedatensatz mit SQLSTATE = 07S01 und der Meldung "Verwendung des Standardparameters ungültig für Parameter \<p >, Spalte \<c >", wobei \<p > ist der Parameter ordinal und \<c > ist der Ordnungszahl der Spalte.  
  
## <a name="see-also"></a>Siehe auch  
 [Table-Valued Parameters &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
