---
title: DMSCHEMA_MINING_STRUCTURES-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DMSCHEMA_MINING_STRUCTURES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_STRUCTURES rowset
ms.assetid: 6224556b-08a0-496e-bd7c-632c3e833e26
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e75e8c17baba84bd690ec51605ffac9f577de35c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="dmschemaminingstructures-rowset"></a>DMSCHEMA_MINING_STRUCTURES-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Listet Informationen über die Miningstrukturen im aktuellen Katalog auf.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DMSCHEMA_MINING_STRUCTURES** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||Der Katalogname.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||Der nicht gekennzeichnete Schemaname. **NULL** , wenn vom Anbieter keine Schemas unterstützt werden.|  
|**STRUKTURNAME**|**DBTYPE_WSTR**||Der Name der Struktur. Diese Spalte darf keinen **NULL**-Wert enthalten.|  
|**STRUCTURE_GUID**|**DBTYPE_GUID**||Eine GUID, die die Struktur eindeutig bezeichnet. **NULL** , wenn sie vom Anbieter nicht unterstützt wird.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Eine knappe Beschreibung der Struktur. **NULL** , wenn der Struktur keine Beschreibung zugeordnet ist.|  
|**STRUCTURE_PROPID**|**DBTYPE_UI4**||Die Eigenschaften-ID der Struktur. **NULL** , wenn sie vom Anbieter nicht unterstützt wird.|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||Das Datum, an dem die Struktur erstellt wurde. **NULL** , wenn vom Anbieter nicht verfügbar.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||Das Datum, an dem die Struktur zuletzt geändert wurde. **NULL** , wenn vom Anbieter nicht verfügbar.|  
|**CREATION_STATEMENT**|**DBTYPE_WSTR**||(Optional) Die für die Erstellung des ursprünglichen Data Mining-Modells verwendete Anweisung.|  
|**IS_POPULATED**|**DBTYPE_BOOL**||Ein boolescher Wert, der angibt, ob die Struktur aufgefüllt wurde.<br /><br /> **VARIANT_TRUE** , wenn die Struktur aufgefüllt wurde, andernfalls **VARIANT_FALSE** .|  
|**LAST_PROCESSED**|**DBTYPE_DBTIMESTAMP**||Das Datum, an dem die Struktur zuletzt verarbeitet wurde. **NULL** , wenn vom Anbieter nicht verfügbar.|  
|**HOLDOUT_MAXPERCENT**|**DBTYPE_ UI1**||Benutzerdefinierter Wert, der den maximalen Prozentsatz der Eingabefälle angibt, die als Testsatz zurückgehalten werden.<br /><br /> 0 oder **NULL** zeigt an, dass keine Einschränkung besteht.|  
|**HOLDOUT_MAXCASES**|**DBTYPE_UI8**||Benutzerdefinierter Wert, der die maximale Anzahl der Eingabefälle angibt, die als Testsatz zurückgehalten werden.<br /><br /> 0 oder **NULL** zeigt an, dass keine Einschränkung besteht.|  
|**HOLDOUT_SEED**|**DBTYPE_UI8**||Benutzerdefinierter Wert, der als Ausgangswert für wiederholbare Partitionierungen verwendet wird.<br /><br /> 0 gibt an, dass ein Hash der Miningstruktur-ID als Ausgangswert verwendet wird.|  
|**HOLDOUT_ACTUAL_SIZE**|**DBTYPE_UI8**||Wenn die Miningstruktur verwendet wird, wird hier die tatsächliche Größe des Testdatensatzen angegeben, ausgedrückt in Anzahl von Fällen.<br /><br /> **NULL** gibt an, dass die Miningstruktur nicht verarbeitet wird.|  
  
 Das Rowset wird sortiert nach **STRUCTURE_CATALOG**, **STRUCTURE_SCHEMA**und **STRUCTURE_NAME**.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DMSCHEMA_MINING_STRUCTURES** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|Optional.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|Optional.|  
|**STRUKTURNAME**|**DBTYPE_WSTR**|Optional.|  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining Schema Rowsets](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
