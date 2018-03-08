---
title: FilterColumn-Eigenschaft (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- FilterColumn property [ADO]
ms.assetid: 0a5473e8-8ce6-4518-83fb-4920b827e285
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62e04ee49313e60dd7f474ed38e179b0ca084ddf
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="filtercolumn-property-rds"></a>FilterColumn-Eigenschaft (RDS)
Gibt die Spalte auf dem die Filterkriterien angeben, die ausgewertet werden soll.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataControl.FilterColumn = String  
```  
  
#### <a name="parameters"></a>Parameter  
 *DataControl*  
 Objektvariable stellt eine [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
 *String*  
 Ein **Zeichenfolge** Wert, der angibt, die Spalte auf dem die Filterkriterien angeben, die ausgewertet werden soll. Die Filterkriterien werden angegeben, der [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md) Eigenschaft.  
  
## <a name="remarks"></a>Hinweise  
 Die [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), und **FilterColumn**Eigenschaften bereitstellen, Sortier- und Filterfunktionen im clientseitigen Cache. Die Funktion zum Sortieren sortiert Datensätze mit Werten aus einer Spalte. Die Filterfunktionalität wird eine Teilmenge der Datensätze auf Grundlage von Suchkriterien, während die vollständige [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) im Cache bleibt. Die [zurücksetzen](../../../ado/reference/rds-api/reset-method-rds.md) -Methode führen Sie die Kriterien und Ersetzen Sie den aktuellen **Recordset** mit einem aktualisierbaren **Recordset**.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, and SortDirection Properties and Reset Method Example (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterCriterion-Eigenschaft (RDS)](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [FilterValue-Eigenschaft (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn-Eigenschaft (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection-Eigenschaft (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


