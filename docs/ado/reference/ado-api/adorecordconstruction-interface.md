---
title: ADORecordConstruction Schnittstelle | Microsoft Docs
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
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76a13ea05920d1a479734b26bdc57bedfe2d6817
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
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
