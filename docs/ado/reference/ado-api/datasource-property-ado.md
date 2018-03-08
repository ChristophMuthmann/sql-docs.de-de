---
title: DataSource-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Recordset20::DataSource
helpviewer_keywords:
- DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ecdaaeab8b09f392e5f21f365b082872e20efbfc
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="datasource-property-ado"></a>DataSource-Eigenschaft (ADO)
Gibt ein Objekt, das Daten als dargestellt, enthält eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Diese Eigenschaft wird verwendet, um datengebundene Steuerelemente mit der Daten-Umgebung zu erstellen. Der Daten-Umgebung verwaltet, Auflistungen von Daten (Datenquellen), enthält benannte Objekte (Datenmember), die als dargestellt werden, werden eine **Recordset** Objekt*.*  
  
 Die [DataMember](../../../ado/reference/ado-api/datamember-property.md) und **DataSource** Eigenschaften müssen zusammen verwendet werden.  
  
 Das referenzierte Objekt implementieren muss die **"IDataSource" sein** Schnittstelle sein und darf eine **IRowset** Schnittstelle.  
  
## <a name="usage"></a>Verwendung  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DataMember-Eigenschaft](../../../ado/reference/ado-api/datamember-property.md)
