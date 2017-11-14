---
title: GetChildren-Methode (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::raw_GetChildren
- _Record::GetChildren
helpviewer_keywords:
- GetChildren method [ADO]
ms.assetid: b3f09bac-4f66-49f6-aa5a-6fbb4fb28338
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 84f146c110b50cc3c73329dd72feb26f1ebf3858
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getchildren-method-ado"></a>GetChildren-Methode (ADO)
Gibt eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) , deren Zeilen darstellen, die untergeordneten Elemente einer Auflistung [Datensatz](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set recordset = record.GetChildren  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Recordset** für die jede Zeile steht für ein untergeordnetes Element des aktuellen Objekts **Datensatz** Objekt. Angenommen, die untergeordneten Elemente des eine **Datensatz** stellt ein Verzeichnis die Dateien und Unterverzeichnisse innerhalb des übergeordneten Verzeichnisses enthalten wäre.  
  
## <a name="remarks"></a>Hinweise  
 Der Anbieter bestimmt, welche Spalten im zurückgegebenen vorhanden **Recordset**. Ein Anbieter gibt z. B. immer eine Ressource **Recordset**.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Das Datensatzobjekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|

