---
title: DBSCHEMA_CATALOGS-Rowset | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DBSCHEMA_CATALOGS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_CATALOGS rowset
ms.assetid: f02dc75d-5442-4eea-b33a-567dc816be7a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe0b9bd6fa59114d95720b4c0b5b631ea88c2748
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dbschemacatalogs-rowset"></a>DBSCHEMA_CATALOGS-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Gibt die physischen Attribute an, die Katalogen zugeordnet sind, auf die über das Datenbankverwaltungssystem (Database Management System, DBMS) zugegriffen werden kann.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DBSCHEMA_CATALOGS** -Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Länge|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|255|Der Katalogname. Lässt keine NULL-Werte zu.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Eine lesbare Beschreibung der Tabelle.|  
|**ROLLEN**|**DBTYPE_WSTR**||Eine durch Trennzeichen getrennte Liste von Rollen, zu der der aktuelle Benutzer gehört.<br /><br /> Ein Sternchen (\*) als eine Rolle enthalten ist, wenn der aktuelle Benutzer ein Server- oder Datenbankadministrator ist.<br /><br /> **Username** wird an **ROLES** angefügt, wenn eine der Rollen dynamische Sicherheit verwendet.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||Das Datum, an dem der Katalog zuletzt geändert wurde.|  
  
 Das Rowset wird nach **CATALOG_NAME**sortiert.  
  
## <a name="restriction-columns"></a>Einschränkungsspalten  
 Das **DBSCHEMA_CATALOGS** -Rowset kann auf die in der folgenden Tabelle aufgeführten Spalten eingeschränkt werden.  
  
|Spaltenname|Typindikator|Einschränkungsstatus|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Optional|  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Schemarowsets](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
