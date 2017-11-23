---
title: CommandTimeout-Eigenschaft (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Command15::CommandTimeout
helpviewer_keywords: CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 908ca954d2165b92287fe6ae3c2cba5eb927a0fd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout-Eigenschaft (ADO)
Gibt an, wie lange warten, während der Ausführung eines Befehls, bevor der Versuch beendet und ein Fehler generiert.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **lange** Wert an, in Sekunden an, wie viel Zeit zur Ausführung eines Befehls gewartet. Standardwert ist 30.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **CommandTimeout** Eigenschaft auf einen [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt oder [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt, das den Abbruch zu ermöglichen eine [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) Methode Rufen Sie aufgrund von Verzögerungen aus Netzwerkverkehrs oder extremer die Nutzung des Servers. Wenn das Intervall, in Festlegen der **CommandTimeout** Eigenschaft verstreicht, bevor der Befehl abgeschlossen ist, die Ausführung ein Fehler auftritt und ADO bricht den Befehl ab. Wenn Sie die Eigenschaft auf 0 (null) festlegen, wartet ADO unbegrenzt, bis die Ausführung abgeschlossen ist. Stellen Sie sicher, den Anbieter und die Datenquelle, Sie Code Unterstützung schreiben, der **CommandTimeout** Funktionalität.  
  
 Die **CommandTimeout** festlegen für eine **Verbindung** Objekt hat keine Auswirkungen auf die **CommandTimeout** festlegen für eine **Befehl** -Objekt, auf die dieselbe **Verbindung**, d. h. die **Befehl** des Objekts **CommandTimeout** Eigenschaft erbt nicht den Wert von der **Verbindung** des Objekts **CommandTimeout** Wert.  
  
 Auf einer **Verbindung** -Objekt, das **CommandTimeout** Eigenschaft bleibt Lese-/Schreibzugriff nach der **Verbindung** wird geöffnet.  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Richtung Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ConnectionTimeout-Eigenschaft (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
