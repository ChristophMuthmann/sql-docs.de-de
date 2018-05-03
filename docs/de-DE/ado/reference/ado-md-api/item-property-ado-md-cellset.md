---
title: Item-Eigenschaft (ADO MD Cellset) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 888a3b32ef7800b711f4ac5ccd9ca60b6a5d7517
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="item-property-ado-md-cellset"></a>Eigenschaft "Element" (ADO MD Cellset)
Ruft eine Zelle aus einem [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) über dessen Koordinaten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>Parameter  
 *Positionen*  
 Ein **VariantArray** von Werten, die eine Zelle eindeutig anzugeben. *Positionen* kann eines der folgenden sein:  
  
-   Ein Array von Positionsnummern  
  
-   Ein Array von Elementnamen  
  
-   Die Ordnungsposition  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Element** -Eigenschaft zum Zurückgeben einer [Zelle](../../../ado/reference/ado-md-api/cell-object-ado-md.md) -Objekts innerhalb einer [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) Objekt. Wenn die **Element** Eigenschaft kann nicht gefunden werden, entspricht Zelle der *Positionen* Argument, ein Fehler auftritt.  
  
 Die **Element** Eigenschaft ist die Standardeigenschaft für die **Cellset** Objekt. Die folgenden Syntaxformen sind austauschbar:  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>Hinweise  
 Die *Positionen* Argument gibt an, welche Zelle zurückgegeben. Sie können die Zelle nach Ordnungsposition oder durch die Position an jeder Achse angeben. Wenn Sie die Zelle nach Position an jeder Achse angeben möchten, können Sie den numerischen Wert der Position oder den Namen der Member für die einzelnen Positionen angeben.  
  
 Die Ordnungsposition ist eine Zahl, die Identifizierung einer Zelle innerhalb der **Cellset**. Grundsätzlich werden Zellen in nummeriert eine **Cellset** als wäre die **Cellset** wurden eine *p*--dimensionales Array, in dem *p* ist die Anzahl der Achsen. Die Zellen werden in zeilengerichteter Reihenfolge adressiert. Unten finden Sie die Formel zum Berechnen der Ordinalzahl einer Zelle ein:  
  
 Wenn Elementnamen übergeben werden als Formatzeichenfolgen auf **Element**, müssen die Elemente in aufsteigender Reihenfolge der Achse numerische Bezeichner aufgeführt werden. Innerhalb einer Achse müssen die Elemente in aufsteigender Reihenfolge der Dimension Schachtelung aufgeführt werden, d. h. der äußersten Dimension Member welches Ereignis zuerst eintritt, gefolgt von einem Mitglied der inneren Dimensionen. Jede Dimension durch eine separate Zeichenfolge dargestellt werden soll, und die Liste der Member Zeichenfolgen durch Kommas getrennt werden soll.  
  
> [!NOTE]
>  Abrufen von Zellen nach Elementnamen möglicherweise nicht von der Datenanbieter unterstützt werden. Finden Sie in der Dokumentation für Ihren Anbieter für Weitere Informationen.  
  
## <a name="applies-to"></a>Gilt für  
 [Cellset-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Cell-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Cellset-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
