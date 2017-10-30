---
title: Entwickeln einer benutzerdefinierten Datenflusskomponente | Microsoft Docs
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
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f25c74b52eaccb6c7b0e92cb7dace3d56f3cdd83
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="developing-a-custom-data-flow-component"></a>Entwickeln einer benutzerdefinierten Datenflusskomponente
  Die Datenflusstask besteht aus Komponenten, die eine Verbindung zu einer Reihe von Datenquellen herstellen und die Daten dann mit Hochgeschwindigkeit transformieren und routen. [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] stellt ein erweiterbares Objektmodell, mit dem Entwickler erstellen benutzerdefinierte Quellen, Transformationen und Ziele, die Sie verwenden können [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] und in bereitgestellten Paketen. Dieser Abschnitt enthält Themen, die Sie durch die Entwicklung benutzerdefinierter Datenflusskomponenten führen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Erstellen einer benutzerdefinierten Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/creating-a-custom-data-flow-component.md)  
 Erläutert die ersten Schritte zum Erstellen einer benutzerdefinierten Datenflusskomponente.  
  
 [Entwurfszeitmethoden einer Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)  
 Erläutert die Entwurfszeitmethoden, die in eine benutzerdefinierte Datenflusskomponente implementiert werden sollen.  
  
 [Laufzeitmethoden einer Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/run-time-methods-of-a-data-flow-component.md)  
 Erläutert die Laufzeitmethoden, die in eine benutzerdefinierte Datenflusskomponente implementiert werden sollen.  
  
 [Ausführungsplan und Pufferzuordnung](../../../integration-services/extending-packages-custom-objects/data-flow/execution-plan-and-buffer-allocation.md)  
 Erläutert den Datenfluss-Ausführungsplan und die Zuordnung von Datenpuffern.  
  
 [Verwenden von Datentypen im Datenfluss](../../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)  
 Erklärt, wie der Datenfluss von .NET Framework verwalteten Daten [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]-Datentypen zuordnet.  
  
 [Überprüfen einer Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)  
 Erklärt die Methoden, mit denen die Komponentenkonfiguration überprüft und Komponentenmetadaten neu konfiguriert werden.  
  
 [Implementieren externer Metadaten](../../../integration-services/extending-packages-custom-objects/data-flow/implementing-external-metadata.md)  
 Erklärt, wie Daten mit externen Metadatenspalten überprüft werden.  
  
 [Auslösen und Definieren von Ereignissen in einer Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/raising-and-defining-events-in-a-data-flow-component.md)  
 Erklärt, wie vordefinierte und benutzerdefinierte Ereignisse ausgelöst werden.  
  
 [Protokollieren und Definieren von Protokolleinträgen in einer Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/logging-and-defining-log-entries-in-a-data-flow-component.md)  
 Erklärt, wie benutzerdefinierte Protokolleinträge erstellt und hinzugefügt werden.  
  
 [Verwenden von Fehlerausgaben in einer Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)  
 Erklärt, wie Fehlerzeilen zu einer alternativen Ausgabe umgeleitet werden.  
  
 [Aktualisieren der Version einer Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/upgrading-the-version-of-a-data-flow-component.md)  
 Erklärt, wie gespeicherte Komponentenmetadaten aktualisiert werden, wenn eine neue Version der Komponente zuerst verwendet wird.  
  
 [Entwickeln einer Benutzeroberfläche für eine Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
 Erklärt, wie ein benutzerdefinierter Editor für eine Komponente implementiert wird.  
  
 [Entwickeln bestimmte Arten von Daten von Datenflusskomponenten](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
 Enthält Informationen zum Entwickeln der drei Arten von Datenflusskomponenten: Quellen, Transformationen und Ziele.  
  
## <a name="reference"></a>Verweis  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Enthält die Klassen und Schnittstellen zur Erstellung benutzerdefinierter Datenflusskomponenten.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Enthält die Klassen und Schnittstellen, aus denen sich das Objektmodell des Datenflusstasks zusammensetzt, und wird zum Erstellen benutzerdefinierter Datenflusskomponenten oder eines Datenflusstasks verwendet.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>  
 Enthält die Klassen und Schnittstellen zur Erstellung der Benutzeroberfläche für Datenflusskomponenten.  
  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../../integration-services/integration-services-error-and-message-reference.md)  
 Listet die vordefinierten [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]-Fehlercodes mit ihren symbolischen Namen und Beschreibungen auf.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
  
### <a name="information-common-to-all-custom-objects"></a>Informationen, die alle benutzerdefinierten Objekte gemeinsam sind  
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
  
 [Entwickeln eines benutzerdefinierten Protokollanbieters](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Erläutert die Programmierung benutzerdefinierter Protokollanbieter.  
  
 [Entwickeln eines benutzerdefinierten ForEach-Enumerators](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Erläutert die Programmierung benutzerdefinierter Enumeratoren.  
  
## <a name="see-also"></a>Siehe auch  
 [Erweitern des Datenflusses mit der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
 [Vergleichen von Skriptlösungen und benutzerdefinierten Objekten](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  

