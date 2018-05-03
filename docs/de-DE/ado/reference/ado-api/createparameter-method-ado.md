---
title: CreateParameter-Methode (ADO) | Microsoft Docs
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
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b67abec7ab37d16ed6a444d5355412dd4dff5e03
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="createparameter-method-ado"></a>CreateParameter-Methode (ADO)
Erstellt ein neues [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekt mit den angegebenen Eigenschaften.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Parameter** Objekt.  
  
#### <a name="parameters"></a>Parameter  
 *Name*  
 Optional. Ein **Zeichenfolge** -Wert, der den Namen der enthält die **Parameter** Objekt.  
  
 *Typ*  
 Optional. Ein [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) Wert, der angibt, den den Datentyp des der **Parameter** Objekt.  
  
 *Richtung*  
 Optional. Ein [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) Wert, der angibt, den Typ des **Parameter** Objekt.  
  
 *Größe*  
 Optional. Ein **lange** Wert, der die maximale Länge für den Parameterwert in Zeichen oder Bytes angibt.  
  
 *Wert*  
 Optional. Ein **Variant** , die angibt, dass des Werts für die **Parameter** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **CreateParameter** Methode zum Erstellen eines neuen **Parameter** Objekt mit einem angegebenen Namen, Typ, Richtung, Größe und Wert. Alle Werte, die Sie in den Argumenten übergeben werden geschrieben, auf den entsprechenden **Parameter** Eigenschaften.  
  
 Diese Methode fügt keinen automatisch die **Parameter** -Objekt an die **Parameter** Auflistung von einem [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt. Auf diese Weise können Sie zusätzliche Eigenschaften festlegen, wenn Sie angefügt werden soll, deren Werte ADO überprüft, die **Parameter** Objekt der Auflistung.  
  
 Wenn Sie angeben, dass einen Datentyp mit variabler Länge, die in der *Typ* Argument, müssen Sie entweder übergeben eine *Größe* Argument oder eine Gruppe der [Größe](../../../ado/reference/ado-api/size-property-ado-parameter.md) Eigenschaft von der **Parameter**  Objekt vor dem Anfügen, damit die **Parameter** Auflistung enthalten ist, andernfalls ein Fehler auftritt.  
  
 Wenn Sie einen numerischen Datentyp angeben (**Type** oder **AdDecimal**) in der *Typ* Argument, und Sie müssen ebenfalls festgelegt. die [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) und [Genauigkeit](../../../ado/reference/ado-api/precision-property-ado.md) Eigenschaften.  
  
## <a name="applies-to"></a>Gilt für  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Anfügen und CreateParameter-Methoden (Beispiel) (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Anfügen und CreateParameter-Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Append-Methode (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)   
 [Parameters-Collection (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
