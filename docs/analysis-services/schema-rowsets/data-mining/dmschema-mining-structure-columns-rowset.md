---
title: DMSCHEMA_MINING_STRUCTURE_COLUMNS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ff811a339635f5ff914224a060e14a52e3f94d6c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingstructurecolumns-rowset"></a>DMSCHEMA_MINING_STRUCTURE_COLUMNS-Rowset
  Beschreibt die einzelnen Spalten aller Miningstrukturen, die auf einen Server mit bereitgestellten [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **DMSCHEMA_MINING_STRUCTURE_COLUMNS** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||Der Katalogname.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||Der nicht gekennzeichnete Schemaname. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]unterstützt keine Schemas, daher ist diese Spalte stets **NULL**.|  
|**STRUKTURNAME**|**DBTYPE_WSTR**||Der Name der Struktur. Diese Spalte darf keine enthalten eine **NULL**.|  
|**SPALTENNAME**|**DBTYPE_WSTR**||Name der Spalte. Eindeutigkeit wird nur für Spalten garantiert, die das gleiche Muster besitzen. Beispielsweise können zwei geschachtelte Spalten den gleichen Namen besitzen, wenn sie zu zwei unterschiedlichen geschachtelten Tabellen innerhalb der gleichen Struktur gehören.|  
|**COLUMN_GUID**|**DBTYPE_GUID**||Der Spalten-GUID Anbieter, die keine GUIDs zur Identifizierung von Spalten verwenden, sollten zurückgeben **NULL** in dieser Spalte.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||Die Spalteneigenschaften-ID. Anbieter, die Spalten keine Eigenschaften-IDs zuordnen sollten zurückgeben **NULL** in dieser Spalte. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] gibt **NULL** für diese Spalte.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||Die Ordnungszahl der Spalte. Spalten werden beginnend mit 1 nummeriert. **NULL** Wenn kein stabiler Ordinalwert für die Spalte vorhanden ist.|  
|**COLUMN_HASDEFAULT**|**DBTYPE_BOOL**||Ein boolescher Wert, der angibt, ob diese Spalte einen Standardwert besitzt.<br /><br /> **"True"** , wenn die Spalte einen Standardwert besitzt.<br /><br /> **"False"** , wenn die Spalte nicht über einen Standardwert besitzt oder wenn nicht bekannt ist, ob die Spalte einen Standardwert besitzt.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||Der Standardwert der Spalte. Ein Anbieter kann ausgesetzt **DBCOLUMN_DEFAULTVALUE** , aber nicht **DBCOLUMN_HASDEFAULT** (für ISO-Tabellen) in das zurückgegebene Rowset **IColumnsRowset:: GetColumnsRowset**.<br /><br /> Wenn der Standardwert ist **NULL**, **COLUMN_HASDEFAULT** ist **"true"** und **COLUMN_DEFAULT** Spalte ist eine **NULL** Wert.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||Eine Bitmaske, die Spaltenmerkmale beschreibt. Die **DBCOLUMNFLAGS** Aufzählungstyp gibt die Bits in dieser Bitmaske fest. Diese Spalte darf keine enthalten eine **NULL** Wert. Gültige Werte sind:<br /><br /> **DBCOLUMNFLAGS_ISNULLABLE** (**0 x 20**)<br /><br /> **DBCOLUMNFLAGS_MAYBENULL** (**0 x 40**)<br /><br /> **DBCOLUMNFLAGS_ISLONG** (**0 x 80**)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||Ein boolescher Wert, der angibt, ob diese Spalte einen Standardwert besitzt.<br /><br /> **"True"** , wenn die Spalte enthalten kann **NULL**; **"False"**, andernfalls.|  
|**DATA_TYPE**|**DBTYPE_UI2**||Der Zähler des Datentyps der Spalte. Beispiel:<br /><br /> "**TABELLE**" = **DBTYPE_HCHAPTER**<br /><br /> "**TEXT**" = **DBTYPE_WCHAR**<br /><br /> "**LANGE**" = **DBTYPE_I8**<br /><br /> "**DOPPELTE**" = **DBTYPE_R8**<br /><br /> "**DATUM**" = **DBTYPE_DATE**|  
|**TYPE_GUID**|**DBTYPE_GUID**||Der GUID des Datentyps der Spalte. Anbieter, die keine GUIDs zur Identifizierung von Datentypen verwenden, sollten zurückgeben **NULL** in dieser Spalte.|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||Die maximal mögliche Länge eines Werts in der Spalte. Für Zeichen-, Binär- oder Bitspalten gelten folgende Werte:<br /><br /> Die maximale Länge der Spalte in Zeichen, Bytes oder Bits, wenn die Länge definiert ist. Eine `CHAR(5)`-Spalte in einer SQL-Tabelle besitzt beispielsweise eine maximale Länge von 5.<br /><br /> Die maximale Länge des Datentyps in Zeichen, Bytes oder Bits, wenn die Spalte keine definierte Länge besitzt.<br /><br /> Null (0), wenn weder die Spalte noch der Datentyp eine definierte Maximallänge besitzt.<br /><br /> **NULL** für alle anderen Spaltentypen.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||Die maximale Länge der Spalte in Oktetten (Bytes), wenn der Spaltentyp Zeichen oder Binär ist. Der Wert 0 (null) bedeutet, dass die Spalte keine maximale Länge verfügt. **NULL** für alle anderen Spaltentypen.|  
|**"NUMERIC_PRECISION"**|**DBTYPE_UI2**||Die maximale Genauigkeit der Spalte, wenn der Datentyp der Spalte mit einem numerischen Datentyp außer **VARNUMERIC**; **NULL** Wenn der Spaltendatentyp nicht numerisch ist oder **VARNUMERIC**.<br /><br /> Die Genauigkeit von Spalten mit dem Datentyp **DBTYPE_DECIMAL** oder **DBTYPE_NUM**ERIC hängt von der Definition der Spalte.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||Die Anzahl der Ziffern rechts vom Dezimaltrennzeichen ist die Spalte "Typindikator" **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**, oder **DBTYPE_VARNUMERIC**. Andernfalls ist der Wert **NULL**.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||Die DateTime-Genauigkeit (die Anzahl der Stellen im Bereich der Sekundenbruchteile) der Spalte, wenn die Spalte den Datentyp "Datetime" oder "Intervall" besitzt. Wenn der Datentyp der Spalte nicht "DateTime" ist, ist dies die **NULL**.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||Der Name des Katalogs, in dem der Zeichensatz definiert ist. **NULL** , wenn der Anbieter keine Kataloge oder unterschiedliche Zeichensätze unterstützt.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||Der nicht qualifizierte Schemaname, in dem der Zeichensatz definiert ist. **NULL** , wenn der Anbieter keine Schemas oder unterschiedliche Zeichensätze unterstützt.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||Der Zeichensatzname. **NULL** , wenn der Anbieter keine anderen Zeichensätze unterstützt.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||Der Name des Katalogs, in dem die Sortierung definiert ist. **NULL** , wenn der Anbieter keine Kataloge oder unterschiedliche Sortierungen unterstützt.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||Der nicht qualifizierte Schemaname, in dem die Sortierung definiert ist. **NULL** , wenn der Anbieter keine Schemas oder unterschiedliche Sortierungen unterstützt.|  
|**SORTIERUNGSNAME**|**DBTYPE_WSTR**||Der Sortierungsname. **NULL** , wenn der Anbieter keine unterschiedliche Sortierungen unterstützt.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||Der Name des Katalogs, in dem die Domäne definiert ist. **NULL** , wenn der Anbieter keine Kataloge oder Domänen unterstützt.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||Nicht gekennzeichneter Name des Schemas, in dem das Objekt definiert ist. **NULL** , wenn der Anbieter keine Schemas oder Domänen unterstützt.|  
|**DOMÄNENNAME**|**DBTYPE_WSTR**||der Domänenname. **NULL** , wenn der Anbieter keine Domänen unterstützt.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Eine lesbare Beschreibung der Spalte. **NULL** , wenn es keine Beschreibung der Spalte zugeordnet ist.|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**||Die Verteilung der Miningstrukturspalte:<br /><br /> "**NORMAL**"<br /><br /> "**LOG_NORM**AL"<br /><br /> "**UNIFORM**"|  
|**INHALTSTYP**|**DBTYPE_WSTR**||Der Inhaltstyp der Miningstrukturspalte:<br /><br /> "**SCHLÜSSEL**"<br /><br /> "**DISKRETE**"<br /><br /> "**FORTLAUFEND**"<br /><br /> "**DISCRETIZED (**[Argumente]**)**"<br /><br /> "**ORDERED**"<br /><br /> "**SEQUENCE_TIME**"<br /><br /> "**ZYKLISCH**"<br /><br /> "**WAHRSCHEINLICHKEIT**"<br /><br /> "**VARIANZ**"<br /><br /> "**STDEV**"<br /><br /> "**UNTERSTÜTZUNG**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**||Eine durch Trennzeichen getrennte Liste von Modellierungsflags. Die einzige unterstützte Flag einer strukturspalte ist "**NOT NULL**".|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**||Ein boolescher Wert, der angibt, ob diese Spalte zu dem Schlüssel gehört.<br /><br /> **VARIANT_TRUE** , wenn diese Spalte mit dem Schlüssel verknüpft ist **VARIANT_FALSE** andernfalls. Wenn der Schlüssel eine einzelne Spalte, die **RELATED_ATTRIBUTE** Feld kann optional seinen Spaltennamen enthalten.|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**||Der Name der Zielspalte, der die aktuelle Spalte zugeordnet ist oder von der sie eine spezielle Eigenschaft ist.|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**||Der Name des der **Tabelle** Spalte, die diese Spalte enthält. **NULL** Wenn keine Tabelle die Spalte enthält.|  
|**IS_POPULATED**|**DBTYPE_BOOL**||Ein boolescher Wert, der angibt, ob diese Spalte einen Satz von möglichen Werten erfasst hat.<br /><br /> **"True"** , wenn die Spalte einen Satz möglicher Werte erfasst hat **"False"**, andernfalls.|  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **DMSCHEMA_MINING_STRUCTURE_COLUMNS** Rowset kann eingeschränkt werden, für die Spalten in der folgenden Tabelle.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|Optional.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|Optional.|  
|**STRUKTURNAME**|**DBTYPE_WSTR**|Optional.|  
|**SPALTENNAME**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Schemarowsets](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

