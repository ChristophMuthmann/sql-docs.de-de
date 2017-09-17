---
title: CommandType-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::CommandType
helpviewer_keywords:
- CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d670a188c89ed96001c93d17a33dc0c03d601a82
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="commandtype-property-ado"></a>CommandType-Eigenschaft (ADO)
Gibt den Typ des eine [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen oder mehrere [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) Werte.  
  
> [!NOTE]
>  Verwenden Sie nicht die **CommandTypeEnum** Werte **AdCmdFile** oder **AdCmdTableDirect** mit **CommandType**. Diese Werte können nur verwendet werden, als Optionen für die [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) und [Requery](../../../ado/reference/ado-api/requery-method.md) Methoden eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **CommandType** Eigenschaft zur Auswertung der Optimierung der [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft.  
  
 Wenn die **Befehlstyp (CommandType)** -Eigenschaftswert festgelegt ist, auf den Standardwert **AdCmdUnknown**, Leistungseinbußen hinnehmbar kann auftreten, weil ADO Aufrufe an den Anbieter, um festzustellen, muss die ** CommandText** Eigenschaft ist eine SQL-Anweisung, eine gespeicherte Prozedur oder einen Tabellennamen an. Wenn Sie wissen, welche Art von Befehl, den Sie verwenden, wird durch Festlegen der **CommandType** Eigenschaft weist ADO, um direkt auf den gewünschten Code zu wechseln. Wenn der **CommandType** Eigenschaft entspricht nicht dem Typ des Befehls in die **CommandText** -Eigenschaft, ein Fehler auftritt, beim Aufrufen der [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) Methode.  
  
## <a name="applies-to"></a>Gilt für  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Richtung Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)

