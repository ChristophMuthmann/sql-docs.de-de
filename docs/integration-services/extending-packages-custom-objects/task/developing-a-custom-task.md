---
title: Entwickeln eines benutzerdefinierten Tasks | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: extending-packages-custom-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom tasks [Integration Services], about custom tasks
- Task class
- custom tasks [Integration Services]
- SSIS custom tasks
- SSIS custom tasks, about custom tasks
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- tasks [Integration Services], custom
- TaskHost object
ms.assetid: dcbd8615-fa6d-4ddb-b8a5-0b19dddd6239
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ec021e3c167aac91beaad4dbcc8b15ca9465e577
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="developing-a-custom-task"></a>Entwickeln eines benutzerdefinierten Tasks
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] nutzt Tasks, um Arbeitseinheiten auszuführen, die das Extrahieren, Umwandeln und Laden von Daten unterstützen. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] beinhaltet verschiedene Tasks, durch die häufig auftretende Aktionen ausgeführt werden, z. B. das Ausführen von SQL-Anweisungen oder das Herunterladen einer Datei von einer FTP-Site. Wenn die enthaltenen Tasks und unterstützten Aktionen Ihre Anforderungen nicht vollständig erfüllen, können Sie einen benutzerdefinierten Task erstellen.  
  
 Zum Erstellen eines benutzerdefinierten Tasks müssen Sie eine Klasse erstellen, die von der <xref:Microsoft.SqlServer.Dts.Runtime.Task>-Basisklasse erbt, das <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>-Attribut auf die neue Klasse anwenden und die Hauptmethoden und -eigenschaften der Basisklasse, einschließlich der <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>-Methode, überschreiben.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In diesem Abschnitt wird beschrieben, wie Sie einen benutzerdefinierten Task und seine optionale benutzerdefinierte Benutzeroberfläche erstellen, konfigurieren und codieren.  
  
 [Erstellen eines benutzerdefinierten Tasks](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)  
 Beschreibt den ersten Schritt, durch den der benutzerdefinierte Task erstellt wird.  
  
 [Codieren eines benutzerdefinierten Tasks](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)  
 Beschreibt, wie die Hauptmethoden eines benutzerdefinierten Tasks codiert werden.  
  
 [Herstellen einer Verbindung mit Datenquellen in einem benutzerdefinierten Task](../../../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
 Beschreibt, wie Sie einen benutzerdefinierten Task mit einer Datenquelle verbinden können.  
  
 [Auslösen und Definieren von Ereignissen in einem benutzerdefinierten Task](../../../integration-services/extending-packages-custom-objects/task/raising-and-defining-events-in-a-custom-task.md)  
 Beschreibt, wie Ereignisse ausgelöst und benutzerdefinierte Ereignisse in dem benutzerdefinierten Task definiert werden.  
  
 [Bereitstellen von Unterstützung für das Debuggen in einem benutzerdefinierten Task](../../../integration-services/extending-packages-custom-objects/task/adding-support-for-debugging-in-a-custom-task.md)  
 Beschreibt, wie Breakpointziele in dem benutzerdefinierten Task erstellt werden.  
  
 [Entwickeln einer Benutzeroberfläche für einen benutzerdefinierten Task](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
 Beschreibt, wie eine Benutzeroberfläche erstellt wird, die im [!INCLUDE[ssIS](../../../includes/ssis-md.md)]-Designer angezeigt wird, um Eigenschaften für den benutzerdefinierten Task zu konfigurieren.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
  
### <a name="information-common-to-all-custom-objects"></a>Informationen, die für alle benutzerdefinierten Objekte gelten  
 Informationen zu allen Arten benutzerdefinierter Objekte, die Sie in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] erstellen können, finden Sie in den folgenden Themen:  
  
 [Entwickeln benutzerdefinierter Objekte für Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Beschreibt die grundlegenden Schritte bei der Implementierung aller Arten von benutzerdefinierten Objekten in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Beibehalten von benutzerdefinierten Objekten](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Beschreibt die benutzerdefinierte Persistenz und erklärt, wann diese notwendig ist.  
  
 [Erstellen, Bereitstellen und Debuggen von benutzerdefinierten Objekten](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Beschreibt die Techniken für das Erstellen, Signieren, Bereitstellen und Debuggen von benutzerdefinierten Objekten.  
  
### <a name="information-about-other-custom-objects"></a>Informationen zu anderen benutzerdefinierten Objekten  
 Informationen zu den anderen Arten benutzerdefinierter Objekte, die Sie in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] erstellen können, finden Sie in den folgenden Themen:  
  
 [Entwickeln eines benutzerdefinierten Verbindungs-Managers](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Erläutert die Programmierung benutzerdefinierter Verbindungs-Manager.  
  
 [Entwickeln eines benutzerdefinierten Protokollanbieters](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Erläutert die Programmierung benutzerdefinierter Protokollanbieter.  
  
 [Entwickeln eines benutzerdefinierten ForEach-Enumerators](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Erläutert die Programmierung benutzerdefinierter Enumeratoren.  
  
 [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 Erläutert die Programmierung benutzerdefinierter Datenflussquellen, Transformationen und Ziele.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweitern von Paketen mithilfe des Skripttasks](../../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [Vergleichen von Skriptlösungen und benutzerdefinierten Objekten](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
