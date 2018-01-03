---
title: CompareBookmarks-Methode (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords: CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e4c3ebb53e34b8e17ae7bc3740bc33d1bfce4fe
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks-Methode (ADO)
Vergleicht zwei Textmarken und gibt eine Angabe über das Verhältnis der entsprechenden Werte zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine [CompareEnum](../../../ado/reference/ado-api/compareenum.md) Wert, der die relative Zeilenposition von zwei Datensätzen, die durch ihre Lesezeichen dargestellt angibt.  
  
#### <a name="parameters"></a>Parameter  
 *Bookmark1*  
 Das Lesezeichen der ersten Zeile.  
  
 *Bookmark2*  
 Das Lesezeichen der zweiten Zeile.  
  
## <a name="remarks"></a>Hinweise  
 Die Textmarken müssen auf den gleichen anwenden [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekt, oder ein **Recordset** Objekt und dessen [Klon](../../../ado/reference/ado-api/clone-method-ado.md). Sie können Lesezeichen aus verschiedenen nicht zuverlässig vergleichen **Recordset** Objekte, selbst wenn sie über die Quelle oder der Befehl erstellt wurden. Noch können Sie vergleichen Lesezeichen für eine **Recordset** Objekt, dessen zugrunde liegende Anbieter keine Vergleiche unterstützt.  
  
 Ein Lesezeichen identifiziert eindeutig eine Zeile in einer **Recordset** Objekt. Verwenden der [Lesezeichen](../../../ado/reference/ado-api/bookmark-property-ado.md) -Eigenschaft der aktuellen Zeile, um deren Textmarke abzurufen.  
  
 Da der Datentyp eines Lesezeichens für jeden Anbieter spezifisch ist, ADO verfügbar macht es als ein **Variant**. SQL Server-Lesezeichen sind z. B. vom Typ DBTYPE_R8 (**doppelte**). ADO würde Verfügbarmachen dieses Typs als ein **Variant** mit einem Untertyp des **doppelte**.  
  
 Beim Vergleichen von Lesezeichen versucht ADO keine Art von Umwandlung. Die Werte werden einfach an den Anbieter übergeben, in der der Vergleich auftritt. Wenn das Lesezeichen übergeben der **CompareBookmarks** Methode in unterschiedlichen Typen Stapelt-Variablen gespeichert sind, kann es die folgenden Typenkonfliktfehler generiert: "Argumente des falschen Typs sind, sind außerhalb des zulässigen Bereichs oder miteinander in Konflikt stehen miteinander."  
  
 Ein Lesezeichen, das nicht gültig oder nicht korrekt ist, verursacht einen Fehler.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CompareBookmarks-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks-Methode (VC++-Beispiel)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark-Eigenschaft (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
