---
title: DMSCHEMA_MINING_COLUMNS Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_COLUMNS rowset
ms.assetid: ae35ccde-4438-46f4-8611-40b2b1a42fce
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa9ee7c66193eb84f883ba0500a8617421f2228e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingcolumns-rowset"></a>DMSCHEMA_MINING_COLUMNS-Rowset
  Beschreibt die einzelnen Spalten aller Datamining-Modellen in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Dieses Rowset wird auf den aktuellen Katalog eingeschränkt.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **DMSCHEMA_MINING_COLUMNS** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Der Katalogname. Wird mit dem Namen der Datenbank aufgefüllt, von der das Modell ein Element ist.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Der nicht gekennzeichnete Schemaname. Diese Spalte wird nicht von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|Der Miningmodellname. Diese Spalte enthält den Namen des Miningmodells, dem eine Spalte zugeordnet ist. Sie ist niemals leer.|  
|**SPALTENNAME**|**DBTYPE_WSTR**|Name der Spalte.|  
|**COLUMN_GUID**|**DBTYPE_GUID**|Der Spalten-GUID Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**|Die Spalteneigenschaften-ID. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**|Die Ordnungsposition der Spalte. Spalten werden beginnend mit 1 nummeriert. Diese Spalte enthält **NULL** Wenn kein stabiler Ordinalwert für die Spalte vorhanden ist.|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob die Spalte einen Standardwert besitzt.<br /><br /> **"True"** , wenn die Spalte einen Standardwert, andernfalls hat **"false"**.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**|Der Standardwert der Spalte.<br /><br /> Wenn der Standardwert ist die **NULL** Wert **COLUMN_HASDEFAULT** enthält **"true"**, und diese Spalte enthält **NULL**.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**|Eine Bitmaske, die die Eigenschaften der Spalte beschreibt. Die **DBCOLUMNFLAGS** Aufzählungstyp gibt die Bits in dieser Bitmaske fest. Diese Spalte ist niemals leer.|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob in dieser Spalte NULL zulässig ist.<br /><br /> **"False"** , wenn die Spalte bekannt ist, werden NULL-Werte zulässt, andernfalls **"true"**.|  
|**DATA_TYPE**|**DBTYPE_UI2**|Der Zähler des Datentyps der Spalte. Die folgende Liste zeigt Beispiele der zurückgegebenen Indikatortypen:<br /><br /> "**Tabelle**" würde zurückgeben **DBTYPE_HCHAPTER**.<br /><br /> "**TEXT**" würde zurückgeben **DBTYPE_WCHAR**.<br /><br /> "**Lange**" würde zurückgeben **DBTYPE_I8**.<br /><br /> "**Doppelte**" würde zurückgeben **DBTYPE_R8**.<br /><br /> "**Datum**" würde zurückgeben **DBTYPE_DATE**.|  
|**TYPE_GUID**|**DBTYPE_GUID**|Der GUID des Datentyps der Spalte. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **VT_NULL**.|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**|Die maximal mögliche Länge eines Werts in der Spalte. Für Zeichen-, Binär- oder Bitspalten gelten folgende Werte:<br /><br /> Die maximale Länge der Spalte in Zeichen, Bytes oder Bits, je nach Spaltentyp, wenn eine Länge definiert ist. Z. B. eine **CHAR(5)** Spalte in einer SQL-Tabelle weist eine maximale Länge von 5.<br /><br /> Die maximale Länge des Datentyps in Zeichen, Bytes oder Bits, je nach Spaltentyp, wenn die Spalte keine definierte Länge besitzt.<br /><br /> Null (0), wenn weder die Spalte noch der Datentyp eine definierte Maximallänge besitzt.<br /><br /> **NULL** für alle anderen Typen von Spalten|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**|Die maximale Länge der Spalte in Oktetten (Bytes), wenn der Spaltentyp Zeichen oder Binär ist. Der Wert 0 (null) bedeutet, dass die Spalte keine maximale Länge verfügt. Diese Spalte enthält **NULL** für alle anderen Spaltentypen.|  
|**"NUMERIC_PRECISION"**|**DBTYPE_UI2**|Die maximale Genauigkeit der Spalte, wenn der Datentyp der Spalte mit einem numerischen Datentyp außer **VARNUMERIC**.<br /><br /> **NULL** Wenn der Spaltendatentyp nicht numerisch ist oder **VARNUMERIC**.<br /><br /> Die Genauigkeit von Spalten mit dem Datentyp **DBTYPE_DECIMAL** oder **DBTYPE_NUMERIC** richtet sich nach der Definition der Spalte.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**|Die Anzahl der Ziffern rechts vom Dezimaltrennzeichen ist die Spalte "Typindikator" **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**, oder **DBTYPE_VARNUMERIC**. Andernfalls enthält diese Spalte **VT_NULL**.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**|Die Datum/Uhrzeit-Genauigkeit (Anzahl der Ziffern im Bereich Sekundenbruchteile) der Spalte, wenn der Datentyp der Spalte einen "DateTime" oder "Intervall" ist; andernfalls **NULL**.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**|Der Name des Katalogs, in dem der Zeichensatz definiert ist. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**|Der nicht gekennzeichnete Schemaname, in dem der Zeichensatz definiert ist. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**|Der Zeichensatzname. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**|Der Name des Katalogs, in dem die Sortierung definiert ist. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**|Der nicht gekennzeichnete Schemaname, in dem die Sortierung definiert ist. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**SORTIERUNGSNAME**|**DBTYPE_WSTR**|Der Sortierungsname. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**|Der Name des Katalogs, in dem die Domäne definiert ist. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**|Nicht gekennzeichneter Name des Schemas, in dem das Objekt definiert ist. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**DOMÄNENNAME**|**DBTYPE_WSTR**|der Domänenname. Diese Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Eine benutzerfreundliche Beschreibung der Spalte in dieser Spalte wird nicht von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; er enthält immer **NULL**.|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**|Eine Beschreibung der statistischen Verteilung der Spalte. Diese Spalte enthält einen der folgenden Werte:<br /><br /> "**NORMAL**"<br /><br /> "**LOG_NORMAL**"<br /><br /> "**UNIFORM**"|  
|**INHALTSTYP**|**DBTYPE_WSTR**|Eine Beschreibung des Spalteninhalts. Diese Spalte enthält einen der folgenden Werte:<br /><br /> "**SCHLÜSSEL**"<br /><br /> "**DISKRETE**"<br /><br /> "**FORTLAUFEND**"<br /><br /> "**DISCRETIZED (**[Argumente]**)**"<br /><br /> "**ORDERED**"<br /><br /> "**SCHLÜSSELZEIT**"<br /><br /> "**ZYKLISCH**"<br /><br /> "**WAHRSCHEINLICHKEIT**"<br /><br /> "**VARIANZ**"<br /><br /> "**STDEV**"<br /><br /> "**UNTERSTÜTZUNG**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"<br /><br /> **"KEY SEQUENCE**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**|Eine durch Trennzeichen getrennte Liste von Flags. Folgende Flags werden definiert:<br /><br /> "**MODEL_EXISTENCE_ONLY**"<br /><br /> "**REGRESSOR**"<br /><br /> Diese Spalte kann auch ein algorithmusspezifisches Modellierungsflag enthalten.|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob die Spalte zum Schlüssel gehört.<br /><br /> **"True"** , wenn diese Spalte zum Schlüssel gehört. Wenn der Schlüssel eine einzelne Spalte, die **RELATED_ATTRIBUTE** Feld kann optional seinen Spaltennamen enthalten.|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**|Der Name der Zielspalte, die die aktuelle Spalte bezieht oder ist eine spezielle Eigenschaft.|  
|**IS_INPUT**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob die Spalte eine Eingabespalte ist.<br /><br /> **VARIANT_TRUE** ist dies eine Eingabespalte.|  
|**IS_PREDICTABLE**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob die Spalte vorhersagbar ist.<br /><br /> **"True"** , wenn die Spalte vorhersagbar ist.|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**|Der Name des der **Tabelle** Spalte, die diese Spalte enthält. Diese Spalte enthält **NULL** , wenn die Spalte nicht in einer anderen Spalte enthalten ist.|  
|**PREDICTION_SCALAR_FUNCTIONS**|**DBTYPE_WSTR**|Eine durch Trennzeichen getrennte Liste von Skalarfunktionen, die auf die Spalte angewendet werden können.|  
|**PREDICTION_TABLE_FUNCTIONS**|**DBTYPE_WSTR**|Eine durch Trennzeichen getrennte Liste von Funktionen, die auf die Spalte angewendet werden können. Die Funktionen sollten eine Tabelle zurückgeben. Die Liste weist folgendes Format auf:<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> Das Format ermöglicht der Clientanwendung, die Signatur (Liste der Parameter) für die jeweilige Funktion zu bestimmen.|  
|**IS_POPULATED**|**DBTYPE_BOOL**|Ein boolescher Wert, der angibt, ob die Spalte mit einem Satz möglicher Werten trainiert wurde.<br /><br /> **"True"** , wenn die Spalte mit einem Satz möglicher Werte trainiert wurde.<br /><br /> Enthält **"false"** , wenn die Spalte nicht aufgefüllt wird.|  
|**PREDICTION_SCORE**|**DBTYPE_R8**|Das Ergebnis des Modells bei der Vorhersage der Spalte. Das Ergebnis wird verwendet, um die Genauigkeit des Modells zu messen.|  
|**SOURCE_COLUMN**|**DBTYPE_WSTR**|Der Name der Quellminingstruktur-Spalte für die aktuelle Miningspalte.|  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **DMSCHEMA_MINING_COLUMNS** Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Optional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Optional.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|Optional.|  
|**SPALTENNAME**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Schemarowsets](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

