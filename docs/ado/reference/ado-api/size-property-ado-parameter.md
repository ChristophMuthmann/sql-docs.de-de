---
title: Size-Eigenschaft (ADO-Parameter) | Microsoft Docs
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
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 643e5e4603b91eb66e57bf3519b31a647fb49d5d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="size-property-ado-parameter"></a>Eigenschaft "Größe" (ADO-Parameter)
Gibt die maximale Größe in Bytes oder Zeichen, der eine [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **lange** -Wert, der die maximale Größe in Bytes oder Zeichen eines Werts in einer **Parameter** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Größe** Eigenschaft zum Ermitteln der maximalen Größe für die geschriebenen Werte oder Auslesen der [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft eine **Parameter** Objekt.  
  
 Wenn Sie einen Datentyp mit variabler Länge für angeben einer **Parameter** Objekt (z. B. eine **Zeichenfolge** eingeben, z. B. **AdVarChar**), müssen Sie des Objekts festlegen  **Größe** Eigenschaft, bevor es zum Anfügen der [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung enthalten ist, andernfalls ein Fehler auftritt.  
  
 Wenn Sie bereits angefügt haben die **Parameter** -Objekt an die **Parameter** Auflistung von eine [Befehl](../../../ado/reference/ado-api/command-object-ado.md) -Objekt, und Sie ändern den Typ in einen Datentyp mit variabler Länge, müssen Sie Legen Sie die **Parameter** des Objekts **Größe** Eigenschaft vor dem Ausführen der **Befehl** Objekt; andernfalls ein Fehler auftritt.  
  
 Bei Verwendung der [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode zum Abrufen von Parameterinformationen von dem Anbieter, und es gibt eine oder mehrere Daten variabler Länge-Typ **Parameter** Objekte ADO möglicherweise Arbeitsspeicher für die Parameter basierend Klicken Sie auf ihre maximal möglichen Größe, die während der Ausführung einen Fehler verursachen könnte. Sie sollten explizit festlegen, um Fehler zu vermeiden, die **Größe** Eigenschaft für diese Parameter vor Ausführung des Befehls.  
  
 Die **Größe** Eigenschaft gilt Lese-/Schreibzugriff.  
  
## <a name="applies-to"></a>Gilt für  
 [Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Richtung Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size-Eigenschaft (ADO Stream)](../../../ado/reference/ado-api/size-property-ado-stream.md)
