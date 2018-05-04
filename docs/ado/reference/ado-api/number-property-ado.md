---
title: Number-Eigenschaft (ADO) | Microsoft Docs
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
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a78db13f7f7789dd66c6358279220d4686ff21d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="number-property-ado"></a>Number-Eigenschaft (ADO)
Gibt die Anzahl, die eindeutig eine [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **lange** -Wert, der einem entsprechen möglicherweise die [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) Konstanten.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Anzahl** -Eigenschaft können Sie bestimmen, welche Fehler aufgetreten ist. Der Wert der Eigenschaft ist eine eindeutige Zahl, die den Fehlerzustand entspricht.  
  
 Die [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung gibt ein HRESULT im Hexadezimalformat (z. B. 0 x 80004005) oder long-Wert (z. B. 2147467259) zurück. Diese HRESULTs können von zugrunde liegenden Komponenten, z. B. OLE DB oder sogar OLE selbst ausgelöst werden. Weitere Informationen zu diesen Telefonnummern, finden Sie unter [Fehler (OLE DB)](http://msdn.microsoft.com/en-us/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd) in der [OLE DB Programmer's Reference](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)*.*  
  
## <a name="applies-to"></a>Gilt für  
 [Error-Objekt](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState-Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description-Eigenschaft](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext HelpFile-Eigenschaften](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Source-Eigenschaft (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
