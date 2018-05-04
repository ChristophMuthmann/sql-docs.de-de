---
title: Delete-Methode (ADOX Sammlungen) | Microsoft Docs
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
- Views::Delete
- Groups::Delete
- Indexes::raw_Delete
- Columns::raw_Delete
- Tables::Delete
- Keys::Delete
- Users::Delete
- Users::raw_Delete
- Keys::raw_Delete
- Procedures::raw_Delete
- Views::raw_Delete
- Indexes::Delete
- Procedures::Delete
- Groups::raw_Delete
- Tables::raw_Delete
- Columns::Delete
helpviewer_keywords:
- delete method [ADOX]
ms.assetid: e6b6e3a4-8952-4d79-81f4-51019c338374
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c059ef4390f504363c9cfaa7f42bb99c6799a2da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="delete-method-adox-collections"></a>Delete-Methode (ADOX Sammlungen)
Entfernt ein Objekt aus einer Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>Parameter  
 *Name*  
 Ein **Variant** , der den Namen oder die Ordnungsposition (Index) des zu löschenden Objekts angibt.  
  
## <a name="remarks"></a>Hinweise  
 Es wird eine Fehlermeldung angezeigt, wenn die *Namen* in der Auflistung nicht vorhanden.  
  
 Für [Tabellen](../../../ado/reference/adox-api/tables-collection-adox.md) und [Benutzer](../../../ado/reference/adox-api/users-collection-adox.md) Auflistungen, wenn der Anbieter beim Löschen von Tabellen oder Benutzer bzw. nicht unterstützt, wird eine Fehlermeldung angezeigt. Für [Prozeduren](../../../ado/reference/adox-api/procedures-collection-adox.md) und [Ansichten](../../../ado/reference/adox-api/views-collection-adox.md) Sammlungen **löschen** schlägt fehl, wenn der Anbieter keine persistenten Befehle unterstützt.  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Columns-Auflistung (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Groups-Auflistung (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Auflistung von Indizes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys Collection (ADOX) (Keys-Auflistung (ADOX))](../../../ado/reference/adox-api/keys-collection-adox.md)|[Procedures Collection (ADOX) (Procedures-Auflistung (ADOX))](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Tables-Auflistung (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Users-Auflistung (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Views-Auflistung (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>Siehe auch  
 [Prozeduren löschen Methodenbeispiel (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Views Delete-Methode – Beispiel (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
