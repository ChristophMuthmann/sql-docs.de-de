---
title: Reset-Methode (RDS) | Microsoft Docs
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Reset method [ADO]
ms.assetid: 3957197a-f543-4d6b-9e11-67a77c2063b7
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f95d5bf30a0646d3e67ae366e29794018095706a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="reset-method-rds"></a>Reset-Methode (RDS)
Führt Sie der Sortier- oder Filtereigenschaften für eine clientseitige **Recordset** basierend auf den angegebenen Eigenschaften der sortieren und filtern.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DataControl.Reset(value)  
```  
  
#### <a name="parameters"></a>Parameter  
 *DataControl*  
 Objektvariable stellt eine [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
 *value*  
 Optional. Ein **booleschen** Wert, der **"true"** (Standard), wenn das aktuelle "gefilterten" Rowset gefiltert werden soll. **"False"** gibt an, dass Sie auf das ursprüngliche Rowset filtern alle vorherigen Filteroptionen entfernen.  
  
## <a name="remarks"></a>Hinweise  
 Die [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), und [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)Eigenschaften bereitstellen, Sortier- und Filterfunktionen im clientseitigen Cache. Die Funktion zum Sortieren sortiert Datensätze mit Werten aus einer Spalte. Die Filterfunktionalität wird eine Teilmenge der Datensätze auf Grundlage einer Suchkriterien, während die vollständige [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) im Cache bleibt. Die **zurücksetzen** -Methode führen Sie die Kriterien und Ersetzen Sie den aktuellen **Recordset** mit einem aktualisierbaren **Recordset**.  
  
 Wenn Änderungen an den ursprünglichen Daten, die nicht übermittelt wurden, werden die **zurücksetzen** Methode fehl. Verwenden Sie zuerst die [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) aufzurufende Methode zum Speichern von Änderungen in einer Lese-/Schreibzugriff **Recordset**, und verwenden Sie dann die **zurücksetzen** Verfahren zum Sortieren oder filtern Sie die Datensätze.  
  
 Wenn Sie mehr als ein Filter für Ihr Rowset ausführen möchten, können Sie das optionale *booleschen* Argument mit den **zurücksetzen** Methode. Im folgende Beispiel veranschaulicht dies:  
  
```  
ADC.SQL = "Select au_lname from authors"  
ADC.Refresh    ' Get the new rowset.  
  
ADC.FilterColumn = "au_lname"  
ADC.FilterCriterion = "<"  
ADC.FilterValue = "'M'"  
ADC.Reset         ' Rowset now has all Last Names < "M".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'F'"  
' Passing True is not necessary, because it is the   
' default filter on the current "filtered" rowset.  
ADC.Reset(TRUE)     ' Rowset now has all Last   
                    ' Names < "M" and > "F".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'T'"  
' Filter on the original rowset, throwing out the  
' previous filter options.  
ADC.Reset(FALSE)   ' Rowset now has all Last Names > "T".  
```  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, and SortDirection Properties and Reset Method Example (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [SubmitChanges-Methode (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



