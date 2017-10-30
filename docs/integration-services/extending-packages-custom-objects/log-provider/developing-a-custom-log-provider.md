---
title: Entwickeln eines benutzerdefinierten Protokollanbieters | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- SSIS packages, log providers
- custom log providers [Integration Services]
- SQL Server Integration Services packages, log providers
- log providers [Integration Services]
- packages [Integration Services], logs
- Integration Services packages, log providers
ms.assetid: 3f715b95-7074-4f5c-8ae2-246998052e78
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9d5dee6649539d340fd9954798db913136553aae
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-custom-log-provider"></a>Entwickeln eines benutzerdefinierten Protokollanbieters
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] bietet umfassende Protokollierungsfunktionen, mit denen Sie bei der Paketausführung auftretende Ereignisse erfassen können. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]enthält eine Vielzahl von Protokollanbietern, Protokolle erstellt und in Formaten wie XML, Text, in Datenbanken oder im Windows-Ereignisprotokoll gespeichert werden. Sollten die Protokollanbieter und die angebotenen Ausgabeformate Ihre Anforderungen nicht vollständig erfüllen, können Sie benutzerdefinierte Protokollanbieter erstellen.  
  
 Zum Erstellen eines benutzerdefinierten Protokollanbieters müssen Sie eine Klasse erstellen, die von der <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>-Basisklasse erbt, das <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>-Attribut auf die neue Klasse anwenden und die Hauptmethoden und -eigenschaften der Basisklasse, einschließlich der <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A>-Eigenschaft und der <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>-Methode, überschreibt.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In diesem Abschnitt wird beschrieben, wie Sie einen benutzerdefinierten Protokollanbieter erstellen, konfigurieren und den entsprechenden Code schreiben.  
  
 [Erstellen eines benutzerdefinierten Protokollanbieters](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)  
 Beschreibt die Erstellung der Klassen für ein benutzerdefiniertes Protokollanbieterprojekt.  
  
 [Codieren eines benutzerdefinierten Protokollanbieters](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)  
 Beschreibt die Implementierung eines benutzerdefinierten Protokollanbieters durch Überschreiben der Methoden und Eigenschaften der Basisklasse.  
  
 [Entwickeln einer Benutzeroberfläche für einen benutzerdefinierten Protokollanbieter](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)  
 Individuelle Benutzeroberflächen für benutzerdefinierte Protokollanbieter werden in nicht unterstützt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
## <a name="related-topics"></a>Verwandte Themen  
  
### <a name="information-common-to-all-custom-objects"></a>Informationen, die für alle benutzerdefinierten Objekte gelten  
 Informationen zu allen Arten benutzerdefinierter Objekte, die Sie in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] erstellen können, finden Sie in den folgenden Themen:  
  
 [Entwickeln benutzerdefinierter Objekte für Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Beschreibt die grundlegenden Schritte bei der Implementierung aller Arten benutzerdefinierter Objekte für [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Beibehalten von benutzerdefinierten Objekten](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Beschreibt die benutzerdefinierte Persistenz und erklärt, wann diese notwendig ist.  
  
 [Erstellen, Bereitstellen und Debuggen von benutzerdefinierten Objekten](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Beschreibt die Techniken für das Erstellen, Signieren, Bereitstellen und Debuggen von benutzerdefinierten Objekten.  
  
### <a name="information-about-other-custom-objects"></a>Informationen zu anderen benutzerdefinierten Objekten  
 Informationen zu den anderen Arten benutzerdefinierter Objekte, die Sie, in erstellen können [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], finden Sie unter den folgenden Themen:  
  
 [Entwickeln eines benutzerdefinierten Tasks](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Erläutert die Programmierung benutzerdefinierter Tasks.  
  
 [Entwickeln eines benutzerdefinierten Verbindungs-Managers](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Erläutert die Programmierung benutzerdefinierter Verbindungs-Manager.  
  
 [Entwickeln eines benutzerdefinierten ForEach-Enumerators](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Erläutert die Programmierung benutzerdefinierter Enumeratoren.  
  
 [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 Erläutert die Programmierung benutzerdefinierter Datenflussquellen, Transformationen und Ziele.  
  

