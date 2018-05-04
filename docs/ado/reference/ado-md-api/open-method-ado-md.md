---
title: Open-Methode (ADO MD) | Microsoft Docs
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
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38876d744f67ef4c218bb56fd4fa585d9dd8ade3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="open-method-ado-md"></a>Open-Methode (ADO MD)
Ruft die Ergebnisse einer MDX-Abfrage ab und gibt die Ergebnisse in einem [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>Parameter  
 *Quelle*  
 Optional. Ein **Variant** , um eine gültige MDX-Abfrage, z. B. eine Abfrage (Multidimensional Expression) ausgewertet wird. Die *Quelle* Argument entspricht dem [Quelle](../../../ado/reference/ado-md-api/source-property-ado-md.md) Eigenschaft. Weitere Informationen zu MDX finden Sie unter der [OLE DB für Online Analytical Processing (OLAP)](http://msdn.microsoft.com/en-us/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) -Dokumentation in der Microsoft Data Access Components SDK.  
  
 *ActiveConnection*  
 Optional. Ein **Variant** , ergibt eine Zeichenfolge, die entweder ein gültiges ADO [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt Variablennamen oder eine Definition für eine Verbindung. Die *ActiveConnection* Argument gibt die Verbindung für das Öffnen der [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) Objekt. Wenn Sie eine Verbindungsdefinition für dieses Argument übergeben, wird von ADO mit den angegebenen Parametern eine neue Verbindung geöffnet. Die *ActiveConnection* Argument entspricht dem [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) Eigenschaft.  
  
## <a name="remarks"></a>Hinweise  
 Die **öffnen** Methode wird ein Fehler generiert, wenn einer der Parameter ausgelassen wird und der entsprechenden Eigenschaftswert nicht festgelegt wurde vor dem Öffnen der **Cellset**.  
  
## <a name="applies-to"></a>Gilt für  
 [Cellset-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Cellset-Beispiel (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [ActiveConnection-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Close-Methode (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Source-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [State-Eigenschaft (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
