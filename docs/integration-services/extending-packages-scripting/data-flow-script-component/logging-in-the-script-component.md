---
title: Protokollierung in the Script Component | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 410a2472399574753d67a44b93437b1698c8b086
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="logging-in-the-script-component"></a>Protokollieren in der Skriptkomponente
  Durch die Protokollierung in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]-Paketen können Sie detaillierte Informationen zum Fortschritt sowie über die Ergebnisse und Probleme der Ausführung speichern, indem Sie vordefinierte Ereignisse bzw. benutzerdefinierte Meldungen für die spätere Analyse erfassen. Die Skriptkomponente können die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> Methode der **ScriptMain** Klasse, um benutzerdefinierte Daten zu protokollieren. Wenn die Protokollierung aktiviert ist, und die **ScriptComponentLogEntry** Ereignis ausgewählt ist, für die Protokollierung auf der **Details** auf der Registerkarte die **SSIS-Protokolle konfigurieren** (Dialogfeld), ein einzelner Aufruf der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> Methode speichert die Ereignisinformationen in allen Protokollanbietern, die für den Datenflusstask konfiguriert wurden.  
  
 Im Folgenden ein einfaches Beispiel für die Protokollierung:  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  Obwohl Sie Protokollierungen direkt von der Skriptkomponente ausführen können, ist ggf. eine Implementierung von Ereignissen einer Protokollierung vorzuziehen. Bei der Verwendung von Ereignissen können Sie nicht nur die Protokollierung von Ereignismeldungen aktivieren, sondern auch auf das Ereignis mit standardmäßigen oder benutzerdefinierten Ereignishandlern reagieren.  
  
 Weitere Informationen zur Protokollierung finden Sie unter [Integration Services &#40; SSIS &#41; Protokollierung](../../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Protokollierung](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

