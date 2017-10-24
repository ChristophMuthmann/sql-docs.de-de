---
title: AppendChunk-Methode (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 812566487a453d806e1defcd7b2b7977e5f1935f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="appendchunk-method-ado"></a>AppendChunk-Methode (ADO)
Fügt Daten an eine große Text- oder Binärdaten [Feld](../../../ado/reference/ado-api/field-object.md), oder auf eine [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>Parameter  
 *Objekt*  
 Ein **Feld** oder **Parameter** Objekt.  
  
 *Daten*  
 Ein **Variant** enthält die Daten, auf das Objekt angefügt werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **AppendChunk** Methode auf eine **Feld** oder **Parameter** Objekt mit dem lange Binär-oder Zeichendatentypen gefüllt. In Situationen, in dem Systemspeicher beschränkt ist, können Sie die **AppendChunk** Methode, um lange Werte in Teilen anstatt in ihrer Gesamtheit zu bearbeiten.  
  
## <a name="field"></a>Feld  
 Wenn die **AdFldLong** bit in der [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) Eigenschaft eine **Feld** -Objekts festgelegt wird, um **"true"**, können Sie die ** AppendChunk** Methode für dieses Feld.  
  
 Die erste **AppendChunk** rufen Sie für eine **Feld** Objekt schreibt Daten in das Feld alle vorhandenen Daten überschrieben. Nachfolgende **AppendChunk** Aufrufe an die vorhandenen Daten hinzufügen. Anfügen von Daten werden an ein Feld, und klicken Sie dann festlegen oder Lesen Sie den Wert eines anderen Felds im aktuellen Datensatz, geht davon aus ADO, dass Sie die Daten an das erste Feld anfügen abgeschlossen haben. Beim Aufrufen der **AppendChunk** Methode auf das erste Feld erneut ADO interpretiert den Aufruf als ein neues **AppendChunk** Vorgang und die vorhandenen Daten überschrieben. Zugriff auf Felder in anderen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekte, die nicht der ersten Klone sind **Recordset** Objekt wird nicht unterbrochen. **AppendChunk** Vorgänge.  
  
 Wenn kein aktueller Datensatz vorhanden, beim Aufrufen von ist **AppendChunk** auf eine **Feld** -Objekt, ein Fehler auftritt.  
  
> [!NOTE]
>  Die **AppendChunk** Methode kann nicht ausgeführt werden, auf **Feld** Objekte von einem [Datensatz Object (ADO)](../../../ado/reference/ado-api/record-object-ado.md) Objekt. Es führt keine Vorgänge und einen Laufzeitfehler erzeugt.  
  
## <a name="parameter"></a>Parameter  
 Wenn die **AdParamLong** bit in der **Attribute** Eigenschaft eine **Parameter** -Objekts festgelegt wird, um **"true"**, können Sie die ** AppendChunk** Methode für diesen Parameter.  
  
 Die erste **AppendChunk** rufen Sie für eine **Parameter** Objekt schreibt Daten in den Parameter alle vorhandenen Daten überschrieben. Nachfolgende **AppendChunk** Ruft für einen **Parameter** -Objekt vorhandenen Parameterdaten hinzugefügt. Ein **AppendChunk** Aufruf, der einen null-Wert übergibt verwirft alle der Parameterdaten.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Field-Objekt](../../../ado/reference/ado-api/field-object.md)|[Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [AppendChunk und GetChunk Methoden Beispiel (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk und GetChunk Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Attribute-Eigenschaft (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [GetChunk-Methode (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)

