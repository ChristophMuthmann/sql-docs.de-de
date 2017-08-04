---
title: Erweitern des Datenflusses with the Script Component | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
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
helpviewer_keywords:
- data flow task [Integration Services], components
- data flow [Integration Services], extending
- debugging [Integration Services], components
- code design mode [Integration Services]
- metadata [Integration Services]
- scripts [Integration Services], extending data flow
- data flow components [Integration Services], Script component
- components [Integration Services], data flow
- Script component [Integration Services], about Script component
- Script component [Integration Services]
- data flow [Integration Services], components
ms.assetid: 072bc4b8-363a-4131-87c3-240338e2fa5c
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c58a854082fcbd12333be63995e4fcdf2d55aac7
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="extending-the-data-flow-with-the-script-component"></a>Extending the Data Flow with the Script Component
  Die Skriptkomponente erweitert die datenflussfunktionen von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Paketen durch benutzerdefinierten Code geschrieben [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual c#, der kompiliert und zur Laufzeit des Pakets ausgeführt wird. Die Skriptkomponente vereinfacht die Entwicklung von benutzerdefinierten Datenflussquellen, -transformationen oder -zielen, falls die in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] enthaltenen Quellen, Transformationen und Ziele Ihre Anforderungen nicht voll erfüllen. Nach Konfiguration der Komponente mit den erwarteten Eingaben und Ausgaben schreibt sie den nötigen Infrastrukturcode für Sie, damit Sie sich vollständig auf den Code konzentrieren können, der für die benutzerdefinierte Verarbeitung erforderlich ist.  
  
 Eine Skriptkomponente interagiert mit dem entsprechenden Paket und mit dem Datenfluss über die automatisch generierten Klassen in der **ComponentWrapper** und **BufferWrapper** Projektelemente, die Instanzen sind von der <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> und <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> bzw. Klassen. Diese Klassen machen Verbindungen, Variablen und andere Paketelemente als typisierte Objekte verfügbar und verwalten Eingaben und Ausgaben. Die Skriptkomponente kann außerdem den [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]-Namespace und die [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Klassenbibliothek sowie benutzerdefinierte Assemblys zum Implementieren benutzerdefinierter Funktionen verwenden.  
  
 Die Skriptkomponente und der Infrastrukturcode, den sie generieren, erleichtern Ihnen die Entwicklung benutzerdefinierter Datenflusskomponenten deutlich. Um die Funktionsweise der Skriptkomponente zu verstehen, Sie können es jedoch hilfreich Abschnitt lesen, [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) die Schritte zu verstehen, die bei der Entwicklung einer benutzerdefinierten Datenflusskomponente beteiligt sind.  
  
 Wenn Sie eine Quelle, Transformation oder ein Ziel erstellen, das Sie in mehreren Paketen wiederverwenden möchten, sollten Sie keine Skriptkomponente verwenden, sondern eine benutzerdefinierte Komponente entwickeln. Weitere Informationen finden Sie unter [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In den folgenden Themen werden weitere Informationen zur Skriptkomponente bereitgestellt.  
  
 [Configuring the Script Component in the Script Component Editor](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
 Eigenschaften, die Sie in Konfigurieren der **Skript Transformations-Editor** wirken sich auf die Funktionen und die Leistung von skriptkomponentencode.  
  
 [Beim Codieren und Debuggen der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
 Verwenden Sie die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA)-Entwicklungsumgebung, die in der Skriptkomponente enthaltenen Skripts zu entwickeln.  
  
 [Grundlegendes zu den Script Component Object Model](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 Ein neues Skriptkomponentenprojekt enthält drei Projektelemente mit mehreren Klassen sowie automatisch generierten Eigenschaften und Methoden.  
  
 [Verwenden von Variablen in der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)  
 Die **ComponentWrapper** Projektelement enthält stark typisierte Accessoreigenschaften für Variablen des Pakets.  
  
 [Herstellen einer Verbindung mit Datenquellen in der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)  
 Die **ComponentWrapper** -Projektelement enthält auch stark typisierte Accessoreigenschaften für Verbindungen im Paket definiert.  
  
 [Auslösen von Ereignissen in der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)  
 Sie können Ereignisse auslösen, um die Benachrichtigung von Problemen und Fehlern sicherzustellen.  
  
 [Protokollierung in der Skriptkomponente](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)  
 Sie können Informationen für im Paket aktivierte Protokollanbieter protokollieren.  
  
 [Entwickeln bestimmter Arten von Skriptkomponenten](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
 Diese einfachen Beispiele erläutern und veranschaulichen, wie mithilfe der Skriptkomponente benutzerdefinierte Datenflussquellen, Transformationen und Ziele entwickelt werden.  
  
 [Zusätzliche Skriptkomponentenbeispiele](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
 In diesen einfachen Beispielen werden einige mögliche Verwendungsbereiche für die Skriptkomponente erklärt und veranschaulicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Skriptkomponente](../../../integration-services/data-flow/transformations/script-component.md)   
 [Vergleichen den Skripttask und Skriptkomponente](../../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
  
  
