---
title: ADOStreamConstruction Schnittstelle | Microsoft Docs
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
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55e7f81233b7cc5cbdf79ea2a71858b3376f46f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction-Schnittstelle
Die **ADOStreamConstruction** Schnittstelle wird verwendet, um eine ADO erstellen **Stream** Objekt aus einer OLE DB- **IStream** Objekt in einer C-/C++-Anwendung.  
  
## <a name="properties"></a>Eigenschaften  
  
|||  
|-|-|  
|[Stream-Eigenschaft](../../../ado/reference/ado-api/stream-property.md)|Lese-/Schreibzugriff. Ruft ab oder legt ihn fest, einen OLE DB- **Stream** Objekt.|  
  
## <a name="methods"></a>Methoden  
 Keine.  
  
## <a name="events"></a>Ereignisse  
 Keine.  
  
## <a name="remarks"></a>Hinweise  
 Erhält einen OLE DB- **IStream** Objekt (`pStream`), die zur Erstellung eines ADO **Stream** Objekt (`adoStr`) läuft auf die folgenden drei grundlegende Vorgänge:  
  
1.  Erstellen Sie ein ADO **Stream** Objekt:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  Abfrage der **IADOStreamConstruction** -Schnittstelle für die **Stream** Objekt:  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 Rufen Sie die `IADOStreamConstruction::get_Stream` Property-Methode legen Sie den OLE DB- **IStream** das ADO-Objekt **Stream** Objekt:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 Die resultierenden `adoStr` Objekt stellt nun das ADO **Stream** Objekte aus der OLE DB- **IStream** Objekt.  
  
## <a name="requirements"></a>Anforderungen  
 **Version:** ADO 2.0 oder höher  
  
 **Bibliothek:** "MSADO15.dll"  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Siehe auch  
 [ADO – API-Referenz](../../../ado/reference/ado-api/ado-api-reference.md)
