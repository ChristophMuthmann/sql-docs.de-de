---
title: FieldEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: FieldEnum
helpviewer_keywords: FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3816a8a810c6ad3bfc50c0dd960b6abc4f859737
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="fieldenum"></a>FieldEnum
Gibt an, die spezielle Felder, die auf die verwiesen wird einem [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) des Objekts [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung.  
  
## <a name="remarks"></a>Hinweise  
 Diese Konstanten bieten eine "Verknüpfung" für den Zugriff auf spezielle zugeordneten Feldern ein **Datensatz**. Abrufen der [Feld](../../../ado/reference/ado-api/field-object.md) -Objekt aus der **Felder** -Auflistung, und rufen Sie dann auf dessen Inhalt mit der **Feld** des Objekts [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft.  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Verweist auf das Feld mit dem Standardwert [Stream](../../../ado/reference/ado-api/stream-object-ado.md) zugeordnete Objekt eine **Datensatz**.|  
|**adRecordURL**|-2|Verweist auf das Feld, enthält die absolute URL-Zeichenfolge für den aktuellen **Datensatz**.|
