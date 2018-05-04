---
title: ActualSize-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67b2f50c094b4f735cb11ebc3f762c85b043dcf6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="actualsize-property-ado"></a>ActualSize-Eigenschaft (ADO)
Gibt die tatsächliche Länge der der Wert eines Felds in Bytes an.  
  
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
