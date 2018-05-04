---
title: SQLState-Eigenschaft | Microsoft Docs
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
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddc3d1e21bd4ba860dbb00e814518b658a9aa11e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlstate-property"></a>SQLState-Eigenschaft
Gibt den SQL-Status für einen bestimmten [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt einen fünf Zeichen **Zeichenfolge** Wert, der den ANSI SQL-Standard folgt und den Fehlercode angibt.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **SQLState** Eigenschaft, die den Fehlercode mit fünf Zeichen gelesen, die der Anbieter zurückgibt, tritt ein Fehler bei der Verarbeitung einer SQL-Anweisung. Z. B. stammen bei Verwendung von Microsoft OLE DB-Anbieter für ODBC mit einer Microsoft SQL Server-Datenbank, SQL-Statusfehlercodes ODBC, basierend auf bestimmten ODBC-Fehler oder zu Fehlern, die von Microsoft SQL Server stammen und klicken Sie dann auf ODBC zugeordnet werden Fehler. Diese Fehlercodes in der ANSI SQL-standard dokumentiert sind jedoch möglicherweise von verschiedenen Datenquellen unterschiedlich implementiert werden.  
  
## <a name="applies-to"></a>Gilt für  
 [Error-Objekt](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState-Eigenschaften-Beispiel (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Beschreibung, HelpContext HelpFile, NativeError, Anzahl, Quelle und SQLState Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
