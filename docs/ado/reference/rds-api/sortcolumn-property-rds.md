---
title: SortColumn-Eigenschaft (RDS) | Microsoft Docs
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.topic: article
apitype: COM
helpviewer_keywords: SortColumn property [RDS]
ms.assetid: f6f80f67-f0fb-4e63-a5f5-8fdf312aac63
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3103fcf5a0ed7df6853c1d8ad2472c0c68ce9260
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="sortcolumn-property-rds"></a>SortColumn-Eigenschaft (RDS)
Gibt an, welche Spalte die Datensätze zu sortieren.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>Parameter  
 *DataControl*  
 Objektvariable stellt eine [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
 *String*  
 Ein **Zeichenfolge** Wert, der den Namen oder Alias der Spalte, nach denen sortiert die Datensätze darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Die **SortColumn**, [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), und [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)Eigenschaften bereitstellen, Sortier- und Filterfunktionen im clientseitigen Cache. Die Funktion zum Sortieren sortiert Datensätze mit Werten aus einer Spalte. Die Filterfunktionalität wird eine Teilmenge der Datensätze auf Grundlage von Suchkriterien, während die vollständige [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) im Cache bleibt. Die [zurücksetzen](../../../ado/reference/rds-api/reset-method-rds.md) -Methode führen Sie die Kriterien und Ersetzen Sie den aktuellen **Recordset** mit einem aktualisierbaren **Recordset**.  
  
 Sortiert eine **Recordset**, müssen Sie zuerst alle ausstehenden Änderungen speichern. Bei Verwendung der **RDS. DataControl**, können Sie die [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) Methode. Beispielsweise, wenn Ihre **RDS. DataControl** ist mit dem Namen ADC1, ist der Code wäre `ADC1.SubmitChanges`. Wenn Sie ADO verwenden **Recordset**, können Sie dessen [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode. Mit **UpdateBatch** ist die empfohlene Methode zum **Recordset** Objekte erstellt, mit der [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) Methode. Der Code kann z. B. `myRS.UpdateBatch` oder `ADC1.Recordset.UpdateBatch`.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, SortDirection Eigenschaften und Reset-Methode (Beispiel) (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Sort-Eigenschaft](../../../ado/reference/ado-api/sort-property.md)   
 [SortDirection-Eigenschaft (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)





