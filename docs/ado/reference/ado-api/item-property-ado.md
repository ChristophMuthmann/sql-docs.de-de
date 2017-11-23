---
title: Item-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Parameters::GetItem
- Indexes::GetItem
- Parameters::Item
- Tables::Item
- Procedures::Item
- Users::GetItem
- Tables::GetItem
- Procedures::GetItem
- Users::get_Item
- Users::Item
- Views::GetItem
- Groups::Item
- Groups::get_Item
- Columns::Item
- Indexes::Item
- Fields15::GetItem
- Columns::GetItem
- Fields::Item
- Indexes::get_Item
- Columns::get_Item
- Fields15::Item
- Views::get_Item
- Groups::GetItem
- Errors::get_Item
- Fields15::get_Item
- Tables::get_Item
- Views::Item
- Errors::GetItem
- Parameters::get_Item
- Errors::Item
- Procedures::get_Item
helpviewer_keywords: Item property [ADO]
ms.assetid: e11484bb-c5c7-42d8-9bb8-21572125d727
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b82a73846dacf2607bdd86e3b4d75609d575ebe9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="item-property-ado"></a>Item-Eigenschaft (ADO)
Gibt ein bestimmtes Element einer Auflistung nach Name oder Ordinalzahl an.  
  
## <a name="syntax"></a>Syntax  
  
```  
Set object = collection.Item ( Index )  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt einen Objektverweis zurück.  
  
## <a name="parameters"></a>Parameter  
 *Index*  
 Ein **Variant** Ausdruck, der auf den Namen oder die Ordinalzahl eines Objekts in einer Auflistung ausgewertet wird.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Element** Eigenschaft, um ein bestimmtes Objekt in einer Auflistung zurück. Wenn **Element** ein Objekt kann nicht gefunden werden, in der Auflistung entspricht der *Index* Argument, ein Fehler auftritt. Darüber hinaus unterstützen einige Sammlungen nicht benannte Objekte; für diese Auflistungen müssen Sie die Ordinalzahl Verweise verwenden.  
  
 Die **Element** Eigenschaft ist die Standardeigenschaft für alle Auflistungen; deshalb sind die folgenden Syntaxformen austauschbar:  
  
```  
collection.Item (Index)  
collection (Index)  
```  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Die Achsenauflistung (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Columns-Auflistung (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Auflistung von Dimensionen (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Errors-Collection (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields-Collection (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Groups-Auflistung (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies Collection (ADO MD) (Hierarchy-Auflistung (ADO MD))](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Auflistung von Indizes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys Collection (ADOX) (Keys-Auflistung (ADOX))](../../../ado/reference/adox-api/keys-collection-adox.md)|[Levels-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Members-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Parameters-Collection (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Positionen-Auflistung (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Procedures Collection (ADOX) (Procedures-Auflistung (ADOX))](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Tables-Auflistung (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Users-Auflistung (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Views-Auflistung (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Element-Eigenschaft (VB)](../../../ado/reference/ado-api/item-property-example-vb.md)   
 [Item-Eigenschaft – Beispiel (VC++)](../../../ado/reference/ado-api/item-property-example-vc.md)   
