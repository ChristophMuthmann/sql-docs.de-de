---
title: ActiveCommand-Eigenschaft (ADO) | Microsoft Docs
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
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b221cc04d9a9e7d4d6c163867d6b77be71292e5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="activecommand-property-ado"></a>ActiveCommand-Eigenschaft (ADO)
Gibt an, die [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt, das die zugeordnete erstellt [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt eine **Variant** , enthält eine **Befehl** Objekt. Standardwert ist ein null-Objekt-Verweis.  
  
## <a name="remarks"></a>Hinweise  
 Die **ActiveCommand** Eigenschaft ist schreibgeschützt.  
  
 Wenn eine **Befehl** Objekt wurde nicht zum Erstellen des aktuellen **Recordset**, und klicken Sie dann eine **Null** Objektverweis wird zurückgegeben.  
  
 Diese Eigenschaft verwenden, um die zugeordnete suchen **Befehl** Objekt, wenn Sie nur das resultierende Dateinamenangabe **Recordset** Objekt.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für ActiveCommand-Eigenschaft (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [Beispiel für ActiveCommand-Eigenschaft (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [ActiveCommand-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
