---
title: Erweitern von Paketen mit Skripts | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SQL Server Integration Services, scripting
- SSIS, scripting
- scripts [Integration Services], about scripting
ms.assetid: 67fe18ef-f3aa-41d4-9b9d-5defd4618c4b
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8ed9de3849d0c68af740d6256c53307f1606822a
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="extending-packages-with-scripting"></a>Erweitern von Paketen mit Skripts
  Wenn die integrierten Komponenten in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Ihren Anforderungen nicht entsprechen, können Sie die Effektivität von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] durch Codieren eigener Erweiterungen erhöhen. Ihnen stehen zwei unterschiedliche Optionen zur Erweiterung der Pakete zur Verfügung: Sie können Code in die leistungsstarken Wrapper schreiben, die vom Skripttask und der Skriptkomponente bereitgestellt werden, oder benutzerdefinierte [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Erweiterungen durch Ableitung von den Basisklassen, die im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objektmodell zur Verfügung stehen, vollständig neu erstellen.  
  
 In diesem Abschnitt wird die einfachere der zwei Optionen beschrieben: das Erweitern von Paketen mit Skripts.  
  
 Der Skripttask und Skriptkomponente können Sie die ablaufsteuerung und Datenfluss Erweitern einer [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Paket mit sehr wenig Code. Beide Objekte verwenden die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)-Entwicklungsumgebung und die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Programmiersprachen Visual C#- und profitieren Sie von der alle Funktionen von der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Klassenbibliothek sowie benutzerdefinierte Assemblys. Mit dem Skripttask und der Skriptkomponente können Entwickler benutzerdefinierte Funktionen erstellen, ohne den kompletten Infrastrukturcode schreiben zu müssen, der normalerweise bei der Entwicklung einer benutzerdefinierten Aufgabe oder Datenflusskomponente erforderlich ist.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Vergleichen den Skripttask und Skriptkomponente](../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
 Beschreibt die Gemeinsamkeiten und Unterschiede zwischen Skripttask und Skriptkomponente.  
  
 [Vergleichen von Skriptlösungen und benutzerdefinierten Objekten](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
 Veranschaulicht die Kriterien bei der Wahl zwischen einer Skripterstellungslösung und der Entwicklung eines benutzerdefinierten Objekts.  
  
 [Verweisen auf andere Assemblys in Skriptlösungen](../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 Beschreibt die erforderlichen Schritte, um in einem Skriptprojekt auf externe Assemblys und Namespaces zu verweisen und diese zu verwenden.  
  
 [Erweitern Sie das Paket mit dem Skripttask](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)  
 Erläutert die Erstellung benutzerdefinierter Tasks mit dem Skripttask. Ein Task wird normalerweise einmal pro Paketausführung aufgerufen oder einmal für jede Datenquelle, die ein Paket öffnet.  
  
 [Erweitern des Datenflusses mit der Skriptkomponente](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
 Erläutert, wie mithilfe der Skriptkomponente benutzerdefinierte Datenflussquellen, Transformationen und Ziele erstellt werden. Eine Datenflusskomponente wird i. d. R. für jede verarbeitete Datenzeile einmal aufgerufen.  
  
## <a name="reference"></a>Verweis  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)  
 Listet die vordefinierten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Fehlercodes mit ihren symbolischen Namen und Beschreibungen auf.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
 [Erweitern von Paketen mit benutzerdefinierten Objekten](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Beschreibt, wie benutzerdefinierte Tasks, Datenflusskomponenten und andere Paketobjekte für die Verwendung in mehreren Paketen erstellt und programmiert werden.  
  
 [Programmgesteuertes Erstellen von Paketen](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Erläutert, wie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete programmgesteuert erstellt, konfiguriert, ausgeführt, geladen, gespeichert und verwaltet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  

