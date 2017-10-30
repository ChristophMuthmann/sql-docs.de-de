---
title: "Auslösen von Ereignissen in der Skriptkomponente | Microsoft Docs"
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
- Script component [Integration Services], raising events
ms.assetid: bb389073-e1d0-4794-8d29-c8b293b6a5e3
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 505855e82b683fc15ca00073f58e1f9cb348f830
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="raising-events-in-the-script-component"></a>Auslösen von Ereignissen in der Skriptkomponente
  Ereignisse bieten eine Möglichkeit, Fehler, Warnungen und andere Informationen, wie z. B. den Fortschritt oder Status eines Tasks, an das entsprechende Paket zu melden. Das Paket stellt Ereignishandler zum Verwalten von Ereignisbenachrichtigungen bereit. Die Skriptkomponente Ereignisse auslösen kann, durch Aufrufen von Methoden für die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> Eigenschaft von der **ScriptMain** Klasse. Weitere Informationen dazu, wie [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Pakete Ereignisse behandeln, finden Sie unter [Integration Services &#40; SSIS &#41; Ereignishandler](../../../integration-services/integration-services-ssis-event-handlers.md).  
  
 Ereignisse können in jedem Protokollanbieter protokolliert werden, der im Paket aktiviert wird. Protokollanbieter speichern Informationen über Ereignisse in einem Datenspeicher. Die Skriptkomponente kann ebenfalls die <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>-Methode verwenden, um Informationen in einem Protokollanbieter zu protokollieren, ohne ein Ereignis auszulösen. Weitere Informationen zur Verwendung der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>-Methode finden Sie im folgenden Abschnitt.  
  
 Um ein Ereignis auszulösen, ruft der Skripttask eine der folgenden Methoden der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>-Schnittstelle auf, die von der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>-Eigenschaft verfügbar gemacht wird:  
  
|Ereignis|Description|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>|Löst ein benutzerdefiniertes Ereignis im Paket aus.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A>|Informiert das Paket über eine Fehlerbedingung.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A>|Stellt Informationen für den Benutzer bereit.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireProgress%2A>|Informiert das Paket über den Fortschritt der Komponente.|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A>|Informiert das Paket darüber, dass die Komponente einen Status aufweist, der eine Benutzerbenachrichtigung erfordert, bei dem es sich aber nicht um eine Fehlerbedingung handelt.|  
  
 Nachfolgend finden Sie ein einfaches Beispiel zur Auslösung eines Error-Ereignisses:  
  
 `Dim myMetadata as IDTSComponentMetaData100`  
  
 `myMetaData = Me.ComponentMetaData`  
  
 `myMetaData.FireError(...)`  
  
## <a name="see-also"></a>Siehe auch  
 [Integrationsservices &#40; SSIS &#41; Ereignishandler](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [Hinzufügen eines Ereignishandlers zu einem Paket](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  

