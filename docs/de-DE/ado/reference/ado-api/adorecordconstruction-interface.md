---
title: ADORecordConstruction Schnittstelle | Microsoft Docs
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
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 564d06235e5fcb6e0f12cd17dcb98dda76ddc280
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction-Schnittstelle
Die **ADORecordConstruction**Schnittstelle wird verwendet, um eine ADO erstellen **Datensatz** Objekt aus einer OLE DB- **Zeile** Objekt in einer C-/C++-Anwendung.  
  
 Diese Schnittstelle unterstützt die folgenden Eigenschaften:  
  
## <a name="properties"></a>Eigenschaften  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|Nur Schreibzugriff.<br />Legt den Container eines OLE DB- **Zeile** dieser ADO-Objekt **Datensatz** Objekt.|  
|[Zeile](../../../ado/reference/ado-api/row-property-ado.md)|Lese-/Schreibzugriff.<br />Ruft ab oder legt ihn fest, einen OLE DB- **Zeile** Objekt vom bzw. auf diesen ADO **Datensatz** Objekt.|  
  
## <a name="methods"></a>Methoden  
 Keine.  
  
## <a name="events"></a>Ereignisse  
 Keine.  
  
## <a name="remarks"></a>Hinweise  
 Erhält einen OLE DB- **Zeile** Objekt (`pRow`), die zur Erstellung eines ADO **Datensatz** Objekt (`adoR`), läuft auf die folgenden drei grundlegende Vorgänge:  
  
1.  Erstellen Sie ein ADO **Datensatz** Objekt:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  Abfrage der **IADORecordConstruction** -Schnittstelle für die **Datensatz** Objekt:  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  Rufen Sie die **IADORecordConstruction:: Put_row** Property-Methode legen Sie den OLE DB- **Zeile** das ADO-Objekt **Datensatz** Objekt:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 Die resultierenden **AdoR** Objekt stellt nun das ADO **Datensatz** Objekte aus der OLE DB- **Zeile** Objekt.  
  
 Ein ADO **Datensatz** Objekt kann auch erstellt werden, aus dem Container des OLE DB- **Zeile** Objekt.  
  
## <a name="requirements"></a>Anforderungen  
 **Version:** ADO 2.0 und höher  
  
 **Bibliothek:** "MSADO15.dll"  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
