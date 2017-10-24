---
title: SaveToFile-Methode | Microsoft Docs
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
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2326257da632839c9b60d630f25adb604018272d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="savetofile-method"></a>SaveToFile-Methode
Speichert den binären Inhalt von einem [Stream](../../../ado/reference/ado-api/stream-object-ado.md) in eine Datei.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>Parameter  
 *FileName*  
 Ein **Zeichenfolge** -Wert, der den vollqualifizierten Namen der Datei, enthält, den Inhalt der **Stream** gespeichert werden sollen. Sie können auf alle gültigen lokalen Speicherort speichern oder einem beliebigen Speicherort verfügbar sein, über einen UNC-Wert.  
  
 *SaveOptions*  
 Ein [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) Wert, der angibt, ob eine neue Datei erstellt werden soll, indem Sie **SaveToFile**, sofern sie nicht bereits vorhanden ist. Standardwert ist **AdSaveCreateNotExists**. Mit diesen Optionen können Sie angeben, dass ein Fehler auftritt, wenn die angegebene Datei nicht vorhanden ist. Sie können auch angeben, **SaveToFile** überschreibt den aktuellen Inhalt einer vorhandenen Datei.  
  
> [!NOTE]
>  Wenn Sie eine vorhandene Datei überschrieben (Wenn **AdSaveCreateOverwrite** festgelegt ist), **SaveToFile** kürzt alle Bytes aus der ursprünglichen vorhandene Datei, die die neue folgen [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Hinweise  
 **SaveToFile** kann verwendet werden, um das Kopieren des Inhalts der eine **Stream** Objekt in einer lokalen Datei. Erfolgt keine Änderung in den Inhalt oder die Eigenschaften der **Stream** Objekt. Die **Stream** Objekt muss vor dem Aufruf geöffnet sein **SaveToFile**.  
  
 Diese Methode ändert nicht die Zuordnung von der **Stream** Objekt, das die zugrunde liegende Datenquelle. Die **Stream** Objekt immer noch die ursprüngliche URL zugeordnet werden oder **Datensatz** , die als Quelle, wenn geöffnet wurde.  
  
 Nach einem **SaveToFile** Vorgang, der aktuellen Position ([Position](../../../ado/reference/ado-api/position-property-ado.md)) im Datenstrom an den Anfang des Datenstroms (0) festgelegt ist.  
  
## <a name="applies-to"></a>Gilt für  
 [Streamobjekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Open-Methode (ADO-Datenstrom)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save-Methode](../../../ado/reference/ado-api/save-method.md)

