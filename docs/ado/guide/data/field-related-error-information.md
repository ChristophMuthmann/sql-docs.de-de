---
title: Fehler im Zusammenhang mit dem Feld Informationen | Microsoft Docs
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
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b53698e1042af197db9d9fa7ddfc4af555721607
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="field-related-error-information"></a>Fehler im Zusammenhang mit dem Feld Informationen
Wenn ein Fehler auf ein Feld direkt verknüpft ist – z. B. wenn die Daten nicht vorhanden ist oder wenn es sich um den falschen Typ für das Feld ist – Sie können weitere Informationen zur Ursache des Problems abrufen, indem Sie untersuchen die **Feld** des Objekts **Status**  Eigenschaft. Diese Eigenschaft wurde verbessert, um spezifische Informationen zum Problem bereit. Dies der Fall ist, z. B. bei einem Aufruf von **UpdateBatch** ein Fehler auftritt, die Ursache des Problems können ermittelt werden die **Status** Eigenschaft von der **Felder** in jeder von den betroffenen Datensätze. Die Eigenschaft enthält einen der Werte in der **FieldStatusEnum** konstant. Die folgende Tabelle enthält die Werte, die von besonderem Interesse sind, wenn ein Fehler auftritt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Gibt an, dass das Feld kann nicht abgerufen werden oder, ohne dass Daten verloren gehen gespeichert.|  
|**adFieldDataOverflow**|6|Gibt an, dass die Daten, die vom Anbieter zurückgegebene den Datentyp des Felds ist übergelaufen.|  
|**adFieldDefault**|13|Gibt an, dass der Standardwert für das Feld beim Festlegen der Daten verwendet wurde.|  
|**adFieldIgnore**|15|Gibt an, dass dieses Feld ausgelassen wurde, wenn die Einstellung Datenwerte in der Quelle. Vom Anbieter wurde kein Wert festgelegt.|  
|**adFieldIntegrityViolation**|10|Gibt an, dass das Feld kann nicht geändert werden, da es sich um ein berechneter oder abgeleiteter Entität handelt.|  
|**adFieldIsNull**|3|Gibt an, dass der Anbieter hat einen null-Wert zurückgegeben.|  
|**adFieldOutOfSpace**|22|Gibt an, dass der Anbieter ist nicht genügend Speicherplatz zum Abschließen eines Verschiebe- oder Kopiervorgang zu erhalten.|
