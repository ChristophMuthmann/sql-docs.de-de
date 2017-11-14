---
title: FieldEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a8533cd43964bf7bd2a456ff2cadce1be00b223
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="fieldenum"></a>FieldEnum
Gibt an, die spezielle Felder, die auf die verwiesen wird einem [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) des Objekts [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung.  
  
## <a name="remarks"></a>Hinweise  
 Diese Konstanten bieten eine "Verknüpfung" für den Zugriff auf spezielle zugeordneten Feldern ein **Datensatz**. Abrufen der [Feld](../../../ado/reference/ado-api/field-object.md) -Objekt aus der **Felder** -Auflistung, und rufen Sie dann auf dessen Inhalt mit der **Feld** des Objekts [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Verweist auf das Feld mit dem Standardwert [Stream](../../../ado/reference/ado-api/stream-object-ado.md) zugeordnete Objekt eine **Datensatz**.|  
|**adRecordURL**|-2|Verweist auf das Feld, enthält die absolute URL-Zeichenfolge für den aktuellen **Datensatz**.|

