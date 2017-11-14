---
title: ActualSize-Eigenschaft (ADO) | Microsoft Docs
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
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d66019d7a71dd480f1a88a28fe94d72a176497c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="actualsize-property-ado"></a>ActualSize-Eigenschaft (ADO)
Gibt die tatsächliche Länge eines Felds an??? s-Wert in Bytes.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Gibt eine **lange** Wert.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **ActualSize** die tatsächliche Länge der zurückzugebenden Eigenschaft eine [Feld](../../../ado/reference/ado-api/field-object.md) Wert des Objekts. Für alle Felder der **ActualSize** Eigenschaft ist schreibgeschützt. Wenn die Länge des ADO bestimmt werden kann die **Feld** -Wert des Objekts, das **ActualSize** -Eigenschaft gibt **ActualSize**.  
  
 Die **ActualSize** und [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) Eigenschaften unterschiedlich sind, wie im folgenden Beispiel gezeigt. Ein **Feld** Objekt mit dem deklarierten Typ **AdVarChar** und eine maximale Länge von 50 Zeichen gibt eine **DefinedSize** Eigenschaftswert von 50, aber die  **ActualSize** Eigenschaftswert zurückgegeben wird, die Länge der Daten in das Feld für den aktuellen Datensatz gespeichert. **Felder** mit einem **DefinedSize** größer als 255 Bytes als Spalten mit variabler Länge behandelt werden.  
  
## <a name="applies-to"></a>Gilt für  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ActualSize und DefinedSize Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize und DefinedSize Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize-Eigenschaft](../../../ado/reference/ado-api/definedsize-property.md)

