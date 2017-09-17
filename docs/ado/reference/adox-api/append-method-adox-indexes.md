---
title: Append-Methode (ADOX Indizes) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb25d4ce8ab95f1311460f67b79a2b2199b96e62
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-indexes"></a>Append-Methode (ADOX Indizes)
Fügt ein neues [Index](../../../ado/reference/adox-api/index-object-adox.md) -Objekt an die [Indizes](../../../ado/reference/adox-api/indexes-collection-adox.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parameter  
 *Index*  
 Die **Index** anzufügende Objekt oder den Namen des Indexes erstellt oder ergänzt.  
  
 *Spalten*  
 Optional. Ein **Variant** Wert, der die Namen der zu indizierenden Spalte(n) angibt. Die *Spalten* Parameter entspricht den Werten von der [Namen](../../../ado/reference/adox-api/name-property-adox.md) Eigenschaft eine [Spalte](../../../ado/reference/adox-api/column-object-adox.md) oder mehrere Objekte.  
  
## <a name="remarks"></a>Hinweise  
 Die *Spalten* -Parameter akzeptiert entweder den Namen einer Spalte oder ein Array von Spaltennamen.  
  
 Es wird eine Fehlermeldung angezeigt, wenn der Anbieter das Erstellen von Indizes nicht unterstützt.  
  
## <a name="applies-to"></a>Gilt für  
 [Auflistung von Indizes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Indizes Append-Methode (Beispiel) (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append-Methode (ADOX-Spalten)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append-Methode (ADOX-Gruppen)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append-Methode (ADOX-Schlüssel)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append-Methode (ADOX Prozeduren)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append-Methode (ADOX-Tabellen)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append-Methode (ADOX-Benutzer)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append-Methode (ADOX Ansichten)](../../../ado/reference/adox-api/append-method-adox-views.md)
