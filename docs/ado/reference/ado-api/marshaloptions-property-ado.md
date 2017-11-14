---
title: Marshalling (ADO) | Microsoft Docs
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
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 01ea12405f6b00ba834b624403891d4ddf66d066
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="marshaloptions-property-ado"></a>Marshalling (ADO)
Gibt an, welche Datensätze von der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) zurück an den Server gemarshallt werden sollen.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen [MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md) Wert. Der Standardwert ist **AdMarshalAll**.  
  
## <a name="remarks"></a>Hinweise  
 Bei Verwendung einer clientseitigen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), Datensätze, die auf dem Client geändert wurden der mittleren Ebene oder Web-Server über ein Verfahren namens Marshalling, das Packen und Senden der Schnittstellenmethode zurückgeschrieben werden Parameter Prozess oder Thread hinweg. Festlegen der **MarshalOptions** Eigenschaft kann die Leistung verbessern, wenn geänderte Remotedaten für die Aktualisierung wieder auf die mittlere Ebene oder Webserver gemarshallt werden.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** diese Eigenschaft wird nur für eine clientseitige verwendet **Recordset**.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Marshalling-Beispiel (VB)](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [Marshalling (VC++-Beispiel)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   

