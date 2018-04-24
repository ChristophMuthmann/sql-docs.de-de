---
title: Description-Eigenschaft | Microsoft Docs
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
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9906861f0c0ae5dc0e45a5ced5a3ec20101a57d8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="description-property"></a>Description-Eigenschaft
Beschreibt eine [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Zeichenfolge** Wert, der eine Beschreibung des Fehlers enthält.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Beschreibung** Eigenschaft, um eine kurze Beschreibung des Fehlers zu erhalten. Zeigen Sie diese Eigenschaft, um die Benachrichtigung des Benutzers zu einem Fehler, die nicht oder nicht behandeln möchten. Die Zeichenfolge stammen aus den ADO- oder einen Anbieter.  
  
 Anbieter sind verantwortlich für die Übergabe von bestimmten Fehlertext ADO. ADO fügt eine [Fehler](../../../ado/reference/ado-api/error-object.md) -Objekt an die **Fehler** Auflistung für jeden Anbieter, Fehler oder Warnung empfängt. Auflisten der **Fehler** -Auflistung, um die Fehler zu verfolgen, die der Anbieter übergibt.  
  
## <a name="applies-to"></a>Gilt für  
 [Error-Objekt](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState-Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext HelpFile-Eigenschaften](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number-Eigenschaft (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source-Eigenschaft (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
