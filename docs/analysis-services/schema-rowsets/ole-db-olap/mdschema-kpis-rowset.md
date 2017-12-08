---
title: MDSCHEMA_KPIS-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
apiname: MDSCHEMA_KPIS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5eae9579701d6f3c2bea0235994cce3325c93130
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemakpis-rowset"></a>MDSCHEMA_KPIS-Rowset
  Beschreibt die Key Performance Indicators (KPIs) innerhalb einer Datenbank.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Die **MDSCHEMA_KPIS** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Die Quelldatenbank.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Nicht unterstützt.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Der übergeordnete Cube für den KPI.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|Die dem KPI zugeordnete Measuregruppe.<br /><br /> Sie können diese Spalte verwenden, um die Dimensionalität des KPI zu bestimmen. Wenn "**\<NULL >**", wird der KPI von allen Measuregruppen dimensioniert werden.<br /><br /> Der Standardwert ist "**\<NULL >**".|  
|**KPI_NAME**|**DBTYPE_WSTR**|Der Name des KPI.|  
|**KPI_CAPTION**|**DBTYPE_WSTR**|Eine Bezeichnung oder Beschriftung, die dem KPI zugeordnet ist. Wird hauptsächlich für Anzeigezwecke verwendet. Wenn keine Beschriftung vorhanden, **KPI_NAME** zurückgegeben wird.|  
|**KPI_DESCRIPTION**|**DBTYPE_WSTR**|Eine lesbare Beschreibung des KPI.|  
|**KPI_DISPLAY_FOLDER**|**DBTYPE_WSTR**|Eine Zeichenfolge, die den Pfad des Anzeigeordners angibt, der von der Clientanwendung zum Anzeigen des Elements verwendet wird. Das Trennzeichen für Ordnerebenen wird von der Clientanwendung definiert. Zu den Tools und Clients, die vom [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], den umgekehrten Schrägstrich (\\) ebenentrennzeichen ist. Um mehrere Anzeigeordner bereitzustellen, verwenden Sie ein Semikolon (;), um die Ordner zu trennen.|  
|**KPI_VALUE**|**DBTYPE_WSTR**|Der eindeutige Name des Elements in der Measuredimension für den KPI-Wert.|  
|**KPI_GOAL**|**DBTYPE_WSTR**|Der eindeutige Name des Elements in der Measuredimension für das KPI-Ziel.<br /><br /> Gibt **NULL** Wenn kein definiert Ziel.|  
|**KPI_STATUS**|**DBTYPE_WSTR**|Der eindeutige Name des Elements in der Measuredimension für den KPI-Status.<br /><br /> Gibt **NULL** Wenn kein definiert Status.|  
|**KPI_TREND**|**DBTYPE_WSTR**|Der eindeutige Name des Elements in der Measuredimension für den KPI-Trend.<br /><br /> Gibt **NULL** Wenn kein definiert Trend.|  
|**KPI_STATUS_GRAPHIC**|**DBTYPE_WSTR**|Die standardmäßige grafische Darstellung des KPI.|  
|**KPI_TREND_GRAPHIC**|**DBTYPE_WSTR**|Die standardmäßige grafische Darstellung des KPI.|  
|**KPI_WEIGHT**|**DBTYPE_WSTR**|Der eindeutige Name des Elements in der Measuredimension für die KPI-Gewichtung.|  
|**KPI_CURRENT_TIME_MEMBER**|**DBTYPE_WSTR**|Der eindeutige Name des Elements in der Zeitdimension, die den zeitlichen Kontext des KPI definiert.<br /><br /> Gibt **NULL** es ist kein Zeitelement definiert.|  
|**KPI_PARENT_KPI_NAME**|**DBTYPE_WSTR**|Der Name des übergeordneten KPI.|  
|**BEREICH**|**DBTYPE_I4**|Der Gültigkeitsbereich des KPI. Der KPI kann ein Sitzungs-KPI oder ein globaler KPI sein.<br /><br /> Diese Spalte kann einen der folgenden Werte besitzen:<br /><br /> MDKPI_SCOPE_GLOBAL=1<br /><br /> MDKPI_SCOPE_SESSION=2|  
|**ANMERKUNGEN**|**DBTYPE_WSTR**|(Optional) Ein Satz von Hinweisen im XML-Format.|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Die **MDSCHEMA_KPIS** Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Optional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Optional.|  
|**KPI_NAME**|**DBTYPE_WSTR**|Optional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Optional) Die standardeinschränkung besitzt den Wert **1**. Eine Bitmap mit einem der folgenden gültigen Werten:<br /><br /> **1** CUBE<br /><br /> **2** DIMENSION|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB für OLAP-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
