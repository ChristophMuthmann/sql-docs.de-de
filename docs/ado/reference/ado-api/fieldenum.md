---
title: FieldEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2d38463ec703335530e33017f77b46cf91c68f0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="fieldenum"></a>FieldEnum
Gibt an, die spezielle Felder, die auf die verwiesen wird einem [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) des Objekts [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung.  
  
## <a name="remarks"></a>Hinweise  
 Diese Konstanten bieten eine "Verknüpfung" für den Zugriff auf spezielle zugeordneten Feldern ein **Datensatz**. Abrufen der [Feld](../../../ado/reference/ado-api/field-object.md) -Objekt aus der **Felder** -Auflistung, und rufen Sie dann auf dessen Inhalt mit der **Feld** des Objekts [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Verweist auf das Feld mit dem Standardwert [Stream](../../../ado/reference/ado-api/stream-object-ado.md) zugeordnete Objekt eine **Datensatz**.|  
|**adRecordURL**|-2|Verweist auf das Feld, enthält die absolute URL-Zeichenfolge für den aktuellen **Datensatz**.|
