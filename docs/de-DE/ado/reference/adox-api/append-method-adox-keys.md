---
title: Append-Methode (ADOX-Schlüssel) | Microsoft Docs
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
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2151cea22c4841904262e3618b9f8fbeaa5bbcdb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="append-method-adox-keys"></a>Append-Methode (ADOX-Schlüssel)
Fügt ein neues [Schlüssel](../../../ado/reference/adox-api/key-object-adox.md) -Objekt an die [Schlüssel](../../../ado/reference/adox-api/keys-collection-adox.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>Parameter  
 *Key*  
 Die **Schlüssel** anzufügende Objekt oder den Namen des Schlüssels, der erstellt oder ergänzt.  
  
 *KeyType*  
 Optional. Ein **lange** Wert, der den Typ des Schlüssels angibt. Die *Schlüssel* Parameter entspricht der [Typ](../../../ado/reference/adox-api/type-property-key-adox.md) Eigenschaft von einem **Schlüssel** Objekt.  
  
 *Column*  
 Optional. Ein **Zeichenfolge** Wert, der den Namen der zu indizierenden Spalte angibt. Die *Spalten* Parameter entspricht dem Wert von der [Namen](../../../ado/reference/adox-api/name-property-adox.md) Eigenschaft eine [Spalte](../../../ado/reference/adox-api/column-object-adox.md) Objekt.  
  
 *RelatedTable*  
 Optional. Ein **Zeichenfolge** Wert, der den Namen der verknüpften Tabelle angibt. Die *RelatedTable* Parameter entspricht dem Wert von der **Namen** Eigenschaft eine [Tabelle](../../../ado/reference/adox-api/table-object-adox.md) Objekt.  
  
 *RelatedColumn*  
 Optional. Ein **Zeichenfolge** Wert, der den Namen der verknüpften Spalte für einen Fremdschlüssel angibt. Die *RelatedColumn* Parameter entspricht dem Wert von der **Namen** Eigenschaft eine [Spalte](../../../ado/reference/adox-api/column-object-adox.md) Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Die *Spalten* -Parameter akzeptiert entweder den Namen einer Spalte oder ein Array von Spaltennamen.  
  
## <a name="applies-to"></a>Gilt für  
 [Keys Collection (ADOX) (Keys-Auflistung (ADOX))](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Append-Keys-Methode, Typ des Schlüssels, RelatedColumn, RelatedTable und UpdateRule Eigenschaften Beispiel (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append-Methode (ADOX-Spalten)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append-Methode (ADOX-Gruppen)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append-Methode (ADOX Indizes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append-Methode (ADOX Prozeduren)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append-Methode (ADOX-Tabellen)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append-Methode (ADOX-Benutzer)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append-Methode (ADOX-Ansichten)](../../../ado/reference/adox-api/append-method-adox-views.md)
