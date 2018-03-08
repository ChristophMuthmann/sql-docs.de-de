---
title: Update Resync Eigenschaft dynamisch (ADO) | Microsoft Docs
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
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6084a0075508c8a9a3658b4a8c694957409376c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="update-resync-property-dynamic-ado"></a>Aktualisieren Sie die Resync Eigenschaft dynamisch (ADO)
Gibt an, ob die [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode einen impliziten gefolgt [Resync](../../../ado/reference/ado-api/resync-method.md) Vorgangs-Methode, und wenn dies der Fall ist, den Bereich dieses Vorgangs.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen oder mehrere der [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) Werte.  
  
## <a name="remarks"></a>Hinweise  
 Die Werte von ADCPROP_UPDATERESYNC_ENUM können kombiniert werden, mit Ausnahme von AdResyncAll, die bereits die Kombination aus den restlichen Werten darstellt.  
  
 Die Konstante **AdResyncConflicts** speichert die Resync-Werte als zugrunde liegenden Werte, jedoch wird keine ausstehenden Änderungen überschrieben.  
  
 **Resync aktualisieren** ist eine dynamische Eigenschaft angefügt die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung bei der [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft auf festgelegt ist **AdUseClient**.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
