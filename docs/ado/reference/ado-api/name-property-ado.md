---
title: Name-Eigenschaft (ADO) | Microsoft Docs
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
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1990ae16694a9ddee3747850773a4c361881a307
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="name-property-ado"></a>Name-Eigenschaft (ADO)
Gibt den Namen eines Objekts an.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Zeichenfolge** Wert, der den Namen eines Objekts angibt.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Namen** Eigenschaft, um einen Namen zuweisen oder Abrufen des Namens des eine **Befehl**, **Eigenschaft**, **Feld**, oder **Parameter**  Objekt.  
  
 Der Wert ist Lese-/Schreibzugriff auf eine **Befehl** Objekt "und" Read-only auf eine **Eigenschaft** Objekt.  
  
 Für eine **Feld** Objekt **Namen** ist normalerweise schreibgeschützt. Allerdings für neue **Feld** Objekte, die angefügt wurden die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung von einer [Datensatz](../../../ado/reference/ado-api/record-object-ado.md), **Namen** Lese-/Schreibzugriff wird erst nach die [Wert](../../../ado/reference/ado-api/value-property-ado.md) -Eigenschaft für die **Feld** angegeben wurde und der Datenanbieter wurde erfolgreich dem neuen hinzugefügt **Feld** durch Aufrufen der [ Update](../../../ado/reference/ado-api/update-method.md) Methode der **Felder** Auflistung.  
  
 Für **Parameter** Objekte noch nicht angefügt werden, um die [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) -Auflistung, die **Namen** Eigenschaft gilt Lese-/Schreibzugriff. Für angefügt **Parameter** und alle anderen Objekte, die **Namen** Eigenschaft ist schreibgeschützt. Namen müssen nicht in einer Auflistung eindeutig sein.  
  
 Sie können Abrufen der **Namen** Eigenschaft eines Objekts von einem Ordinalzahlverweis, Sie nach dem auf das Objekt, direkt anhand Ihres Namens verweisen können. Z. B. wenn `rstMain.Properties(20).Name` ergibt `Updatability`, Sie können anschließend verweisen auf diese Eigenschaft als `rstMain.Properties("Updatability")`.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Field-Objekt](../../../ado/reference/ado-api/field-object.md)|  
|[Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)|[Property-Objekt (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute und Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [Attribute und Namen Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
