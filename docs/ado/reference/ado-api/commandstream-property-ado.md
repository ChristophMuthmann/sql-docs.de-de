---
title: CommandStream-Eigenschaft (ADO) | Microsoft Docs
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
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 28e4c73b4fdc94be1687ec011ad3a42e5b51bd78
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="commandstream-property-ado"></a>CommandStream-Eigenschaft (ADO)
Gibt den Datenstrom verwendet als Eingabe für eine [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt den Datenstrom verwendet als Eingabe für eine **Befehl** Objekt. Das Format für diesen Datenstrom ist anbieterspezifisch; finden Sie Einzelheiten s. Dokumentation des Anbieters. Diese Eigenschaft ähnelt der [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft, die an eine Zeichenfolge für die Eingabe verwendet eine **Befehl**.  
  
## <a name="remarks"></a>Hinweise  
 **CommandStream** und **CommandText** gegenseitig aus. Wenn vom Benutzer festgelegt die **CommandStream** -Eigenschaft, die **CommandText** Eigenschaftensatz auf die leere Zeichenfolge (""). Vom Benutzer festgelegt die **CommandText** -Eigenschaft, die **CommandStream** -Eigenschaftensatz auf **nichts**.  
  
 Das Verhalten von der **Command.Parameters.Refresh** und **Command.Prepare** Methoden vom Anbieter definiert werden. Die Werte von Parametern in einem Datenstrom können nicht aktualisiert werden.  
  
 Der Eingabedatenstrom ist nicht verfügbar für andere ADO-Objekte, die die Quelle der Zurückgeben einer **Befehl**. Z. B. wenn die [Quelle](../../../ado/reference/ado-api/source-property-ado-recordset.md) von einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) auf festgelegt ist eine **Befehl** -Objekt, das über einen Stream als Eingabe, **Recordset.Source** weiterhin zurück, die **CommandText** Eigenschaft, die eine leere Zeichenfolge enthält (""), anstatt den Inhalt des Streams von der **CommandStream** Eigenschaft.  
  
 Bei Verwendung einer befehlsdatenstrom (nach den Angaben von **CommandStream**), der einzige gültige [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) Werte für die [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) -Eigenschaft sind  **AdCmdText** und **AdCmdUnknown**. Jeder andere Wert verursacht einen Fehler.  
  
## <a name="applies-to"></a>Gilt für  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CommandText-Eigenschaft (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Dialect-Eigenschaft](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)

