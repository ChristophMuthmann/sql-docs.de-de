---
title: DefinedSize-Eigenschaft | Microsoft Docs
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
f1_keywords: Field20::DefinedSize
helpviewer_keywords: DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a730e33ba9d3ce73a1178ee38ef1b9a5e58b5965
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="definedsize-property"></a>DefinedSize-Eigenschaft
Gibt die Datenkapazität von einem [Feld](../../../ado/reference/ado-api/field-object.md) Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **lange** -Wert, der die definierte Größe eines Felds zu, die für den Datentyp der Field-Objekt abhängig ist wiedergeben, finden Sie unter [Typ](../../../ado/reference/ado-api/type-property-ado.md) für Weitere Informationen. Für ein Feld, das einen Datentyp mit fester Länge verwendet, ist der Rückgabewert die Größe des Datentyps in Byte. Für ein Feld, das einen Datentyp mit variabler Länge verwendet wird, wird eine der folgenden:  
  
1.  Die maximale Länge des Felds in Zeichen (für **AdVarChar** und **AdVarWChar**) oder in Bytes (für **AdVarBinary**, und **AdVarNumeric**) Wenn das Feld eine definierte Länge aufweist. Beispielsweise **adVarChar(5)** Feld hat eine maximale Länge von 5.  
  
2.  Die maximale Länge des Datentyps in Zeichen (für **AdChar** und **AdWChar**) oder in Bytes (für **AdBinary** und **Type**) Wenn die Feld muss nicht definierte Länge.  
  
3.  ~ 0 (bitweises, der Wert ist 0; nicht alle Bits auf 1 festgelegt), wenn weder das Feld noch der Datentyp eine definierte Maximallänge besitzt.  
  
4.  Für Datentypen, die nicht mit eine Länge verfügen, wird dies festgelegt auf ~ 0 (bitweises, der Wert ist 0; nicht alle Bits auf 1 festgelegt).  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **DefinedSize** Eigenschaft zum Ermitteln der Datenkapazität von einem **Feld** Objekt.  
  
 Die **DefinedSize** und [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) Eigenschaften unterschiedlich sind. Betrachten Sie beispielsweise eine **Feld** Objekt mit dem deklarierten Typ **AdVarChar** und ein **DefinedSize** Eigenschaftswert von 50 enthält ein einzelnes Zeichen. Die **ActualSize** Eigenschaftswert zurückgegeben wird, die Länge in Bytes, der das einzelne Zeichen steht.  
  
## <a name="applies-to"></a>Gilt für  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ActualSize und DefinedSize Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize und DefinedSize Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize-Eigenschaft (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
