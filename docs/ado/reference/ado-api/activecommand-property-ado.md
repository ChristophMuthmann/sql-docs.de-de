---
title: ActiveCommand-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset20::ActiveCommand
helpviewer_keywords: ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e5384aff9ee8646493d26272cdeaae33ab49157
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
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
