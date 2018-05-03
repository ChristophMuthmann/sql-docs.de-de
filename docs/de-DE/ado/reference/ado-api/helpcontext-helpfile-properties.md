---
title: HelpFile-Eigenschaften, HelpContext | Microsoft Docs
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
- Error::GetHelpContext
- Error::GetHelpFile
- Error::get_HelpFile
- Error::get_HelpContext
- Error::HelpContext
- Error::HelpFile
helpviewer_keywords:
- HelpContext property [ADO]
- HelpFile property [ADO]
ms.assetid: 2b9ef441-993c-44d4-8f87-fac0979dac1d
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74b6cab9fdd337bef8b36da027abbd7d7d87bb57
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext HelpFile-Eigenschaften
Gibt an, die Hilfedatei sowie zugeordnete Thema ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt.  
  
## <a name="return-values"></a>Rückgabewerte  
  
-   **Hilfekontext-ID** gibt eine Kontext-ID als ein **lange** Wert für ein Thema in einer Hilfedatei.  
  
-   **HelpFile** gibt eine **Zeichenfolge** Wert, der einen vollständigen Pfad zu einer Hilfedatei ergibt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn in eine Hilfedatei angegeben ist die **HelpFile** -Eigenschaft, die **HelpContext** Eigenschaft wird verwendet, um automatisch das Hilfethema anzuzeigen, identifiziert. Wenn keine entsprechenden Hilfethema verfügbar, die **HelpContext** Eigenschaft gibt NULL zurück und die **HelpFile** Eigenschaft gibt eine Zeichenfolge der Länge 0 (null) zurück ("").  
  
## <a name="applies-to"></a>Gilt für  
 [Error-Objekt](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState-Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description-Eigenschaft](../../../ado/reference/ado-api/description-property.md)   
 [Number-Eigenschaft (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source-Eigenschaft (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
