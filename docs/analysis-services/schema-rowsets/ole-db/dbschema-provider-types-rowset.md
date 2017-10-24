---
title: DBSCHEMA_PROVIDER_TYPES-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DBSCHEMA_PROVIDER_TYPES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_PROVIDER_TYPES rowset
ms.assetid: 255e01ba-53a9-478d-9b86-45faba76710e
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6906aec1d1c1dd53b8c833d59483aa0453cf284b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbschemaprovidertypes-rowset"></a>DBSCHEMA_PROVIDER_TYPES-Rowset
  Gibt die von dem Datenanbieter unterstützten (Basis-)Datentypen an.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DBSCHEMA_PROVIDER_TYPES** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**TYPE_NAME**|**DBTYPE_WSTR**|Der anbieterspezifische Datentypname.|  
|**DATA_TYPE**|**DBTYPE_UI2**|Der Indikator des Datentyps.|  
|**COLUMN_SIZE**|**DBTYPE_UI4**|Die Länge einer nicht numerischen Spalte oder eines Parameters, der im Allgemeinen entweder die maximale oder die vom Anbieter definierte Länge für diesen Typ bezeichnet. Bei Zeichendaten ist dies die maximale Länge oder die definierte Länge, angegeben in Zeichen. Bei DateTime-Datentypen ist dies die Länge der Zeichenfolgendarstellung (wobei die maximal zulässige Genauigkeit der Komponente für Sekundenbruchteile vorausgesetzt wird).<br /><br /> Wenn der Datentyp numerisch ist, ist dies die obere Grenze der maximalen Genauigkeit des Datentyps.|  
|**LITERAL_PREFIX-ZEICHEN**|**DBTYPE_WSTR**|Das Zeichen oder die Zeichen, die in einem Textbefehl als Präfix für ein Literal von diesem Typ verwendet werden.|  
|**LITERAL_SUFFIX**|**DBTYPE_WSTR**|Das Zeichen oder die Zeichen, die in einem Textbefehl als Suffix für ein Literal von diesem Typ verwendet werden.|  
|**CREATE_PARAMS**|**DBTYPE_WSTR**|Die vom Consumer angegebenen Erstellungsparameter beim Erstellen einer Spalte dieses Datentyps. Der SQL-Datentyp **DECIMAL,** erfordert beispielsweise eine Genauigkeit und Dezimalstellen. In diesem Fall könnten die Erstellungsparameter die Zeichenfolge "precision,scale" sein. In einem Textbefehl zur Erstellung einer **DECIMAL** -Spalte mit einer Genauigkeit von 10 und mit 2 Dezimalstellen könnte der Wert der Spalte **TYPE_NAME** **DECIMAL()** lauten, und die vollständige Typspezifikation wäre **DECIMAL(10,2)**.<br /><br /> Die Erstellungsparameter werden als eine Liste mit durch Trennzeichen getrennten Werten dargestellt, die in der Reihenfolge, in der sie bereitgestellt werden müssen, und ohne umgebende Klammern angegeben sind. Wenn Länge, maximale Länge, Genauigkeit, Dezimalstellen, Ausgangswert oder Inkrement ein Erstellungsparameter ist, verwenden Sie "length", "max length", "precision", "scale", "seed" bzw. "increment". Wenn der Erstellungsparameter ein anderer Wert ist, bestimmt der Anbieter den Text, der zur Beschreibung des Erstellungsparameters verwendet werden soll.<br /><br /> Wenn der Datentyp Erstellungsparameter erfordert, enthält der Typname normalerweise Klammern. Sie geben die Position an, bei der die Erstellungsparameter eingefügt werden müssen. Wenn der Typname keine Klammern enthält, werden die Erstellungsparameter in Klammern gesetzt und an den Datentypnamen angehängt.|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob für diesen Datentyp NULL zulässig ist.<br /><br /> **VARIANT_TRUE** gibt an, dass für diesen Datentyp NULL zulässig ist.<br /><br /> **VARIANT_FALSE** gibt an, dass für diesen Datentyp NULL nicht zulässig ist.<br /><br /> **NULL**gibt an, dass nicht bekannt ist, ob NULL für diesen Datentyp zulässig ist.|  
|**CASE_SENSITIVE**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob der Datentyp ein Zeichentyp ist und die Groß-/Kleinschreibung beachtet.<br /><br /> **VARIANT_TRUE** gibt an, dass der Datentyp ein Zeichentyp ist und die Groß-/Kleinschreibung beachtet.<br /><br /> **VARIANT_FALSE** gibt an, dass der Datentyp kein Zeichentyp ist und die Groß-/Kleinschreibung nicht beachtet.|  
|**DURCHSUCHBARE**|**DBTYPE_UI4**|Eine Ganzzahl, die angibt, wie der Datentyp für Suchen verwendet werden kann, wenn der Anbieter **ICommandText**unterstützt; andernfalls lautet der Wert **NULL**. Diese Spalte kann die folgenden Werte enthalten:<br /><br /> **DB_UNSEARCHABLE** gibt an, dass der Datentyp nicht in einer **WHERE** -Klausel verwendet werden kann.<br /><br /> **DB_LIKE_ONLY** gibt an, dass der Datentyp in einer **WHERE** -Klausel nur mit dem Prädikat **LIKE** verwendet werden kann.<br /><br /> **DB_ALL_EXCEPT_LIKE** gibt an, dass der Datentyp in einer **WHERE** -Klausel mit allen Vergleichsoperatoren mit Ausnahme von **LIKE**verwendet werden kann.<br /><br /> **DB_SEARCHABLE** gibt an, dass der Datentyp in einer **WHERE** -Klausel mit jedem Vergleichsoperator verwendet werden kann.|  
|**UNSIGNED_ATTRIBUTE**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob dieser Datentyp ein Vorzeichen aufweist oder nicht.<br /><br /> **VARIANT_TRUE** gibt an, dass der Datentyp kein Vorzeichen aufweist.<br /><br /> **VARIANT_FALSE** gibt an, dass der Datentyp ein Vorzeichen aufweist.<br /><br /> **NULL** gibt an, dass dies nicht für diesen Datentyp gilt.|  
|**FIXED_PREC_SCALE**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob der Datentyp über eine feste Genauigkeit und Dezimalstellen verfügt.<br /><br /> **VARIANT_TRUE** gibt an, dass der Datentyp über eine feste Genauigkeit und Dezimalstellen verfügt.<br /><br /> **VARIANT_FALSE** gibt an, dass der Datentyp über keine feste Genauigkeit und Dezimalstellen verfügt.|  
|**AUTO_UNIQUE_VALUE ENTHÄLT**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob dieser Datentyp eine automatische Inkrementierung aufweist oder nicht.<br /><br /> **VARIANT_TRUE** gibt an, dass Werte dieses Typs automatisch inkrementieren können.<br /><br /> **VARIANT_FALSE** gibt an, dass Werte dieses Typs nicht automatisch inkrementieren können.<br /><br /> Wenn dieser Wert **VARIANT_TRUE**lautet, ist die automatische Inkrementierung einer Spalte dieses Typs stets von der Spalteneigenschaft **DBPROP_COL_AUTOINCREMENT** des Anbieters abhängig. Wenn die Eigenschaft **DBPROP_COL_AUTOINCREMENT** Lese- und Schreibzugriff bietet, ist die automatische Inkrementierung einer Spalte dieses Typs von der Einstellung der Eigenschaft **DBPROP_COL_AUTOINCREMENT** abhängig. Wenn **DBPROP_COL_AUTOINCREMENT** nur Lesezugriff bietet, werden entweder alle oder keine der Spalten dieses Typs automatisch inkrementiert.|  
|**LOCAL_TYPE_NAME**|**DBTYPE_WSTR**|Die lokalisierte Version von **TYPE_NAME**. Wenn ein lokalisierter Name vom Datenbieter nicht unterstützt wird, wird**NULL** zurückgegeben.|  
|**MINIMUM_SCALE**|**DBTYPE_I2**|Der Typindikator lautet **DBTYPE_VARNUMERIC**, **DBTYPE_DECIMAL**oder **DBTYPE_NUMERIC**, die Mindestanzahl von Stellen rechts neben dem Dezimalkomma, die zulässig ist. Andernfalls **NULL**.|  
|**MAXIMUM_SCALE**|**DBTYPE_I2**|Die maximale Anzahl von Stellen rechts neben dem Dezimalkomma, wenn der Typindikator **DBTYPE_VARNUMERIC**, **DBTYPE_DECIMAL**oder **DBTYPE_NUMERIC**lautet; andernfalls N**U**LL.|  
|**GUID**|**DBTYPE_GUID**|(Für zukünftige Verwendung vorgesehen) Die **GUID** des Typs, wenn der Typ in einer Typbibliothek beschrieben ist. Andernfalls **NULL**.|  
|**DER TYPBIBLIOTHEK**|**DBTYPE_WSTR**|(Für zukünftige Verwendung vorgesehen) Die Typbibliothek, die die Beschreibung des Typs enthält, wenn der Typ in einer Typbibliothek beschrieben ist. Andernfalls wird NULL verwendet.|  
|**VERSION**|**DBTYPE_WSTR**|(Für zukünftige Verwendung vorgesehen) Die Version der Typdefinition. Manche Anbieter verwenden möglicherweise Versionstypdefinitionen. Andere Anbieter verwenden möglicherweise andere Versionsschemas, z. B. einen Zeitstempel oder eine Zahl (integer oder float). **NULL** , wenn nicht unterstützt.|  
|**IS_LONG**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob der Datentyp ein BLOB (Binary Large Object) darstellt und sehr lange Daten aufweist.<br /><br /> **VARIANT_TRUE** gibt an, dass der Datentyp ein **BLOB** ist, das sehr lange Daten enthält; die Definition von "sehr lange Daten" ist anbieterspezifisch.<br /><br /> **VARIANT_FALSE** gibt an, dass der Datentyp ein **BLOB** ist, der keine sehr langen Daten enthält, oder dass er kein **BLOB**ist.<br /><br /> Dieser Wert bestimmt die Einstellung des **DBCOLUMNFLAGS_ISLONG** -Flag, das von **GetColumnInfo** in **IColumnsInfo** und **GetParameterInfo** in **ICommandWithParameters**zurückgegeben wird.|  
|**BEST_MATCH**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob dieser Datentyp eine größte Übereinstimmung darstellt oder nicht.<br /><br /> **VARIANT_TRUE** gibt an, dass der Datentyp die beste Übereinstimmung zwischen allen Datentypen im Datenspeicher und dem OLE DB-Datentyp darstellt, der durch den Wert in der **DATA_TYPE** -Spalte angegeben wird.<br /><br /> **VARIANT_FALSE** gibt an, dass der Datentyp nicht die beste Übereinstimmung darstellt.<br /><br /> Für jede Gruppe von Zeilen, in denen der Wert der **DATA_TYPE** -Spalte gleich ist, wird die **BEST_MATCH** -Spalte in nur einer Zeile auf **VARIANT_TRUE** festgelegt.|  
|**IS_FIXEDLENGTH**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob die Spalte eine feste Länge hat.<br /><br /> **VARIANT_TRUE** gibt an, dass Spalten dieses Typs, die durch die Datendefinitionssprache (DDL) erstellt werden, eine feste Länge haben.<br /><br /> **VARIANT_FALSE** gibt an, dass Spalten dieses Typs, die durch die Datendefinitionssprache (DDL) erstellt werden, eine variable Länge haben.<br /><br /> Wenn das Feld den Wert **NULL**enthält, ist nicht bekannt, ob der Anbieter dieses Feld einer Spalte mit fester oder variabler Länge zuordnet.|  
  
 Das Rowset wird nach **DATA_TYPE**sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DBSCHEMA_PROVIDER_TYPES** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|  
|-----------------|--------------------|  
|**DATA_TYPE**|**DBTYPE_UI2**|  
|**BEST_MATCH**|**DBTYPE_BOOL**|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  

