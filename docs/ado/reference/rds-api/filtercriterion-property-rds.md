---
title: FilterCriterion-Eigenschaft (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24e64adb684435f40c52c55d1c97b1c863551ecb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="filtercriterion-property-rds"></a>FilterCriterion-Eigenschaft (RDS)
Gibt an, die Evaluation-Operator, um in den Filterwert verwenden.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>Parameter  
 *DataControl*  
 Objektvariable stellt eine [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
 *String*  
 Ein **Zeichenfolge** -Wert, der den Operator für die Auswertung der gibt an, die [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md) Datensätze informiert. Kann eine der folgenden sein: <, \<=, >, > =, =, oder <>.  
  
## <a name="remarks"></a>Hinweise  
 Die [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), **FilterCriterion**, und [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)Eigenschaften bereitstellen, Sortier- und Filterfunktionen im clientseitigen Cache. Die Funktion zum Sortieren sortiert Datensätze mit Werten aus einer Spalte. Die Filterfunktionalität wird eine Teilmenge der Datensätze auf Grundlage von Suchkriterien, während die vollständige [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) im Cache bleibt. Die [zurücksetzen](../../../ado/reference/rds-api/reset-method-rds.md) -Methode führen Sie die Kriterien und Ersetzen Sie den aktuellen **Recordset** mit einem aktualisierbaren **Recordset**.  
  
 Die "! ="-Operator gilt nicht für **FilterCriterion**; stattdessen "<>" verwenden.  
  
 Wenn sowohl die Filter- und sortierungsausdrücke Eigenschaften festgelegt sind, und Sie rufen die **zurücksetzen** -Methode, das Rowset zuerst gefiltert, und klicken Sie dann sortiert. Die null-Werte sind für eine aufsteigende Sortierung, am oberen; für eine absteigende Sortierung an, der null-Werte werden im unteren Bereich (Standardverhalten aufsteigender ist).  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, SortDirection Eigenschaften und Reset-Methode (Beispiel) (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn-Eigenschaft (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [FilterValue-Eigenschaft (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [SortColumn-Eigenschaft (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection-Eigenschaft (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


