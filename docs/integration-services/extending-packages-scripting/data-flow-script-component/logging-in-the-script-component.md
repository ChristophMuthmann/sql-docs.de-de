---
title: Protokollieren in der Skriptkomponente | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b8673343ce198cdf61f7726888694045d4fff4df
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="logging-in-the-script-component"></a>Protokollieren in der Skriptkomponente
  Durch die Protokollierung in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]-Paketen können Sie detaillierte Informationen zum Fortschritt sowie über die Ergebnisse und Probleme der Ausführung speichern, indem Sie vordefinierte Ereignisse bzw. benutzerdefinierte Meldungen für die spätere Analyse erfassen. Die Skriptkomponente kann die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>-Methode der **ScriptMain**-Klasse verwenden, um benutzerdefinierte Daten zu protokollieren. Wenn die Protokollierung aktiviert ist und in der Registerkarte **Details** des Dialogfelds **SSIS-Protokolle konfigurieren** das Ereignis **ScriptComponentLogEntry** für die Protokollierung ausgewählt ist, dann speichert ein einzelner Aufruf der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>-Methode die Ereignisinformationen in allen Protokollanbietern, die für den Datenflusstask konfiguriert wurden.  
  
 Im Folgenden ein einfaches Beispiel für die Protokollierung:  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  Obwohl Sie Protokollierungen direkt von der Skriptkomponente ausführen können, ist ggf. eine Implementierung von Ereignissen einer Protokollierung vorzuziehen. Bei der Verwendung von Ereignissen können Sie nicht nur die Protokollierung von Ereignismeldungen aktivieren, sondern auch auf das Ereignis mit standardmäßigen oder benutzerdefinierten Ereignishandlern reagieren.  
  
 Weitere Informationen zur Protokollierung finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../../integration-services/performance/integration-services-ssis-logging.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integration Services-Protokollierung &#40;SSIS&#41;](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
