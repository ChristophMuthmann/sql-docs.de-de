---
title: MDSCHEMA_ACTIONS-Rowsets | Microsoft Docs
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
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_ACTIONS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_ACTIONS rowset
ms.assetid: f73081f8-ac51-4286-b46e-2b34e792c3e0
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e9abd044460f463b952eb6fbd88cd7d7a4ea2821
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemaactions-rowset"></a>MDSCHEMA_ACTIONS-Rowset
  Beschreibt die Aktionen, die der Clientanwendung möglicherweise zur Verfügung stehen.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **MDSCHEMA_ACTIONS** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||Der Name der Datenbank.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Wird nicht unterstützt. Enthält immer **VT_NULL**.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||Der Name des Cubes, zu dem diese Aktion gehört.|  
|**AKTIONSNAME**|**DBTYPE_WSTR**||Der Name dieser Aktion.|  
|**ACTION_TYPE**|**DBTYPE_I4**||Eine Bitmap, die verwendet wird, um die Triggermethode der Aktion anzugeben. Die Datei Msmd.h definiert die folgenden Bitwertkonstanten für diese Bitmap:<br /><br /> **MDACTION_TYPE_URL** (**0 x 01**)<br /><br /> **MDACTION_TYPE_HTML** (**0 x 02**)<br /><br /> **MDACTION_TYPE_STATEMENT** (**0 x 04**)<br /><br /> **MDACTION_TYPE_DATASET** (**0 x 08**)<br /><br /> **MDACTION_TYPE_ROWSET** (**0 x 10**)<br /><br /> **MDACTION_TYPE_COMMANDLINE** (**0 x 20**)<br /><br /> **MDACTION_TYPE_PROPRIETARY** (**0 x 40**)<br /><br /> **MDACTION_TYPE_REPORT** (**0 x 80**)<br /><br /> **MDACTION_TYPE_DRILLTHROUGH** (**0 x 100**)|  
|**KOORDINIEREN**|**DBTYPE_WSTR**||Ein MDX-Ausdruck (Multidimensional Expressions), der ein Objekt oder eine Koordinate im mehrdimensionalen Raum angibt, in dem die Aktion ausgeführt wird. Die Clientanwendung ist für die Bereitstellung des Werts für diese Einschränkungsspalte zuständig.<br /><br /> Die **CORDINATE** muss in dem im angegebenen Objekt aufgelöst **COORDINATE_TYPE**.|  
|**COORDINATE_TYPE**|**DBTYPE_I4**||Eine Bitmap, die angibt, wie die **KOORDINIEREN** -Einschränkungsspalte interpretiert wird. Die Datei Msmd.h definiert die folgenden Bitwertkonstanten für diese Bitmap:<br /><br /> **MDACTION_COORDINATE_CUBE** (**1**)<br /><br /> **MDACTION_COORDINATE_DIMENSION** (**2**): bezieht sich auf die Dimensionshierarchien.<br /><br /> **MDACTION_COORDINATE_LEVEL** (**3**)<br /><br /> **MDACTION_COORDINATE_MEMBER** (**4**)<br /><br /> **MDACTION_COORDINATE_SET** (**5**)<br /><br /> **MDACTION_COORDINATE_CELL** (**6**)|  
|**ACTION_CAPTION**|**DBTYPE_WSTR**||Der Aktionsname, wenn in der DDL keine Beschriftung und keine Übersetzungen angegeben wurden.<br /><br /> Wenn eine Beschriftung oder Übersetzungen angegeben wurden, und **CaptionIsMDX** "false" ist eine der folgenden Zeichenfolgen:<br /><br /> -Die Übersetzung für die entsprechende Sprache.<br /><br /> -Die angegebene Beschriftung, wenn keine Übersetzung für die angegebene Sprache gefunden wurde.<br /><br /> – Der Aktionsname, wenn keine Übersetzung gefunden und der Beschriftung wurde nicht im DDL-Code angegeben.<br /><br /> Wenn eine Beschriftung oder Übersetzungen angegeben wurden, und **CaptionIsMDX** ist "true", die aus der Suche nach der entsprechenden Übersetzung für die angegebene Sprache oder die angegebene Verschiebung in der DDL-Beschriftung und das Berechnen der resultierenden Zeichenfolge die Formel zum Erstellen der Zeichenfolge.<br /><br /> Wenn die Aktion im MDX-Skript angegeben wurde, gibt es keine Übersetzungen und die Beschriftung wird stets als MDX-Ausdruck behandelt.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Eine benutzerfreundliche Beschreibung der Aktion.|  
|**INHALT**|**DBTYPE_WSTR**||Der Ausdruck oder Inhalt der Aktion, die ausgeführt werden soll.|  
|**ANWENDUNG**|**DBTYPE_WSTR**||Der Name der Anwendung, die zur Ausführung der Aktion verwendet werden soll.|  
|**AUFRUF**|**DBTYPE_I4**||Informationen darüber, wie die Aktion aufgerufen werden soll:<br /><br /> **MDACTION_INVOCATION_INTERACTIVE** (**1**) gibt eine reguläre, während normaler Vorgänge verwendete Aktion an. Dies ist der Standardwert für diese Spalte.<br /><br /> **MDACTION_INVOCATION_ON_OPEN** (**2**) gibt an, dass die Aktion ausgeführt werden soll, wenn der Cube erstmalig geöffnet wird.<br /><br /> **MDACTION_INVOCATION_BATCH** (**4**) gibt an, dass die Aktion, als Teil eines Batchvorgangs ausgeführt wird oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Aufgabe.<br /><br /> <br /><br /> Beachten Sie, dass diese Enumerationswerte in der Datei Msmd.h definiert sind.|  
  
 Das Rowset wird sortiert nach **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **ACTION_NAME**.  
  
> [!NOTE]  
>  Aktionen des **MDACTION_TYPE_PROPRIETARY** Typ muss Geben Sie einen Wert für die **Anwendung** Spalte.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **MDSCHEMA_ACTIONS** Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Optional|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Optional|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Obligatorisch.|  
|**AKTIONSNAME**|**DBTYPE_WSTR**|Optional|  
|**ACTION_TYPE**|**DBTYPE_I4**|Optional|  
|**KOORDINIEREN**|**DBTYPE_WSTR**|Obligatorisch.|  
|**COORDINATE_TYPE**|**DBTYPE_I4**|Obligatorisch.|  
|**AUFRUF**|**DBTYPE_I4**|(Optional) Die **AUFRUF** -Einschränkungsspalte wird standardmäßig auf den Wert der **MDACTION_INVOCATION_INTERACTIVE**. Verwenden Sie zum Abrufen aller Aktionen den **MDACTION_INVOCATION_ALL** Wert in der **AUFRUF** Einschränkungsspalte.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Optional) Standardeinschränkung besitzt den Wert 1. Eine Bitmap mit einem der folgenden gültigen Werten:<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
  
> [!IMPORTANT]  
>  Die **AUFRUF** -Einschränkungsspalte verfügt über einen Standardwert von **MDACTION_INVOCATION_INTERACTIVE**. Jedes Schemarowset, das nicht ausdrücklich einen Wert für diese Spalte angibt, enthält nur Zeilen mit diesem Wert. Verwenden Sie gegebenenfalls das Rowset enthält den gesamten Satz an Aktionen, die **MDACTION_INVOCATION_ALL** Konstanten in der **AUFRUF** Einschränkungsspalte.  
  
 Clientanwendungen können mehrere definieren **ACTION_TYPE** mithilfe des OR-Operators.  
  
## <a name="remarks"></a>Hinweise  
 Die folgende Tabelle enthält die gültigen **KOORDINIEREN** und **COORDINATE_TYPE** Kombinationen.  
  
|COORDINATE-Objekttyp|COORDINATE_TYPE|  
|----------------------------|----------------------|  
|**Cube**|**MDACTION_COORDINATE_CUBE**|  
|**Dimension**|**MDACTION_COORDINATE_DIMENSION**<br /><br /> **MDACTION_COORDINATE_LEVEL**<br /><br /> **MDACTION_COORDINATE_MEMBER**<br /><br /> **MDACTION_COORDINATE_SET**<br /><br /> **MDACTION_COORDINATE_CELL**|  
|**Hierarchy**|**MDACTION_COORDINATE_DIMENSION**|  
|**Level**|**MDACTION_COORDINATE_LEVEL**|  
|**Member**|**MDACTION_COORDINATE_MEMBER**|  
|**Festlegen**|**MDACTION_COORDINATE_SET**|  
|**Zelle**|**MDACTION_COORDINATE_CELL**|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

