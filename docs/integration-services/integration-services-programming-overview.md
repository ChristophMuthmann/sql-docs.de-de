---
title: "Übersicht über die Programmierung von Integration Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services, programming
- architecture [Integration Services]
- assemblies [Integration Services]
- SSIS, programming
- SQL Server Integration Services, programming
- run-time engine [Integration Services]
- packages [Integration Services], programming
- data flow engine [Integration Services]
- languages [Integration Services]
ms.assetid: 262babc6-eea5-4609-bc65-07d64cbcfee9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ac7e1c7a179455d662dddb3e01af3cb2ff55bc66
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-programming-overview"></a>Übersicht über die Programmierung von 'Integration Services'
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] verfügt über eine Architektur, die die Datenverschiebung und -transformation von der Paketablaufsteuerung und Verwaltung trennt. Diese Architektur wird durch zwei unterschiedliche Module definiert, die bei der Programmierung von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] automatisiert und erweitert werden können. Das Laufzeitmodul implementiert die Infrastruktur der Ablaufsteuerung und Paketverwaltung, mit deren Hilfe Entwickler den Ausführungsprozess steuern und Optionen für die Protokollierung, Ereignishandler und Variablen festlegen können. Das Datenflussmodul ist ein spezialisiertes Hochleistungsmodul, das ausschließlich dem Extrahieren, Transformieren und Laden von Daten dient. Beim Programmieren von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] programmieren Sie mit diesen beiden Modulen.  
  
 Im folgenden Bild wird die Architektur von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dargestellt.  
  
 ![Integration Services-Architektur](../integration-services/media/mw-dts-01.gif "Integration Services architecture")  
  
## <a name="integration-services-run-time-engine"></a>Integration Services-Laufzeitmodul  
 Das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Laufzeitmodul steuert durch die Implementierung der Infrastruktur, die die Ausführungsreihenfolge, Protokollierung, Variablen und die Ereignisbehandlung ermöglicht, die Verwaltung und Ausführung von Paketen. Durch die Programmierung des [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Laufzeitmoduls können Entwickler die Erstellung, Konfiguration und Ausführung von Paketen automatisieren sowie benutzerdefinierte Tasks und andere Erweiterungen erstellen.  
  
 Weitere Informationen finden Sie unter [Erweitern von Paketen mithilfe des Skripttasks](../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md), [Entwickeln eines benutzerdefinierten Tasks](../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md) und [Programmgesteuertes Erstellen von Paketen](../integration-services/building-packages-programmatically/building-packages-programmatically.md).  
  
## <a name="integration-services-data-flow-engine"></a>Integration Services-Datenflussmodul  
 Das Datenflussmodul verwaltet den Datenflusstask. Dies ist ein spezialisierter Hochleistungstask, der dem Verschieben und Transformieren von Daten verschiedener Quellen dient. Im Gegensatz zu anderen Tasks enthält der Datenflusstask zusätzliche Objekte, die sogenannten Datenflusskomponenten, bei denen es sich um Quellen, Transformationen oder Ziele handeln kann. Diese Komponenten sind die wichtigsten verschiebbaren Teile des Tasks. Sie definieren die Bewegung und die Transformation von Daten. Durch die Programmierung des Laufzeitmoduls können Entwickler die Erstellung und Konfiguration der Komponenten in einem Datenflusstask automatisieren sowie benutzerdefinierte Komponenten erstellen.  
  
 Weitere Informationen finden Sie unter [Extending the Data Flow with the Script Component](../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md) (Erweitern des Datenflusses mit der Skriptkomponente), [Entwickeln einer benutzerdefinierten Datenflusskomponente](../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) und [Programmgesteuertes Erstellen von Paketen](../integration-services/building-packages-programmatically/building-packages-programmatically.md).  
  
## <a name="supported-languages"></a>Unterstützte Sprachen  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] unterstützt vollständig [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. Dadurch können Entwickler [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in ihren bevorzugten .NET-kompatiblen Sprachen programmieren. Obwohl das Laufzeitmodul und das Datenflussmodul in einem systemeigenen Code geschrieben wurden, sind sie beide über ein vollständig verwaltetes Objektmodell verfügbar.  
  
 Sie können [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakete, benutzerdefinierte Tasks und Komponenten in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] oder einem anderen Code- bzw. Text-Editor programmieren. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] enthält viele Tools und Funktionen für Entwickler, die die iterativen Zyklen, bestehend aus Codierung, Debugging und Test, sowie vereinfachen und beschleunigen. Auch die Bereitstellung ist mit [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] einfacher. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] wird jedoch nicht benötigt, um [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Codeprojekte zu kompilieren und zu erstellen. Das [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]-SDK enthält die [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]- und [!INCLUDE[csprcs](../includes/csprcs-md.md)]-Compiler sowie zugehörige Tools.  
  
> [!IMPORTANT]  
>  Standardmäßg wird [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installiert, das [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]-SDK jedoch nicht. Die in diesem Abschnitt vorkommenden Links auf SDK-Inhalte funktionieren nur, wenn das SDK auf Ihrem Computer installiert und die SDK-Dokumentation in der Onlinedokumentation enthalten ist. Fügen Sie das SDK nach der Installation des [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK zur Onlinedokumentation und dem Inhaltsverzeichnis hinzu, indem Sie die Anweisungen unter [Hinzufügen oder Entfernen der Produktdokumentation für SQL Server](http://msdn.microsoft.com/library/ef798cc8-87cf-4d60-a7bf-9e061bdd0052) befolgen.  
  
 Der Skripttask und die Skriptkomponente von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] verwenden [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA) als eingebettete Skriptumgebung. VSTA unterstützt [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic und [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#.  
  
> [!NOTE]  
>  Die [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Anwendungsprogrammierschnittstellen sind mit COM-basierten Skriptsprachen, z. B. VBScript, nicht kompatibel.  
  
## <a name="locating-assemblies"></a>Suchen von Assemblys  
 In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] wurden die [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Assemblys auf .NET 4.0 aktualisiert. Es ist ein separater globaler Assemblycache für .NET 4 verfügbar, der sich im Verzeichnis „*\<Laufwerk>*:\Windows\Microsoft.NET\assembly“ befindet. Normalerweise befinden sich alle [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Assemblys unter diesem Pfad im Ordner GAC_MSIL.  
  
 Wie bei früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] befinden sich die zentralen DLL-Dateien für die [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Erweiterbarkeit auch im Verzeichnis „*\<Laufwerk>*:\Programme\Microsoft SQL Server\100\SDK\Assemblies“.  
  
## <a name="commonly-used-assemblies"></a>Häufig verwendete Assemblys  
 In der folgenden Tabelle sind die Assemblys, die häufig beim Programmieren von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] mithilfe von [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] verwendet werden, aufgelistet.  
  
|Assembly|Description|  
|--------------|-----------------|  
|Microsoft.SqlServer.ManagedDTS.dll|Enthält das verwaltete Laufzeitmodul.|  
|Microsoft.SqlServer.RuntimeWrapper.dll|Enthält die primäre Interopassembly (PIA) oder den Wrapper für das systemeigene Laufzeitmodul.|  
|Microsoft.SqlServer.PipelineHost.dll|Enthält das verwaltete Datenflussmodul.|  
|Microsoft.SqlServer.PipelineWrapper.dll|Enthält die primäre Interopassembly (PIA) oder den Wrapper für das systemeigene Datenflussmodul.|  
  
  
