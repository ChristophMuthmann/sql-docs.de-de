---
title: NativeError-Eigenschaft (ADO) | Microsoft Docs
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
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords:
- NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3dd8b2962e460606da23ac207daa0e5e2ad3d465
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="nativeerror-property-ado"></a>NativeError-Eigenschaft (ADO)
Gibt den anbieterspezifischen Fehlercode für einen bestimmten [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **lange** Wert, der den Fehlercode angibt.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **NativeError** Eigenschaft zum Abrufen der datenbankspezifischen Fehlerinformationen für einen bestimmten **Fehler** Objekt. Z. B. Wenn Sie den Microsoft ODBC-Datenanbieter für OLE DB mit einer Microsoft SQL Server-Datenbank verwenden zu können, systemeigenen Fehlercodes, die vom SQL Server stammen pass-through ODBC und den ODBC-Anbieter der ADO **NativeError** Eigenschaft.  
  
## <a name="applies-to"></a>Gilt für  
 [Error-Objekt](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState-Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
