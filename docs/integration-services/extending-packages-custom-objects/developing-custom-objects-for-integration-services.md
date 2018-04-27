---
title: Entwickeln benutzerdefinierter Objekte für Integration Services | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
helpviewer_keywords:
- custom user interface [Integration Services]
- custom objects [Integration Services]
ms.assetid: ca1929a6-0ae6-47d7-b65f-08173b143720
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6672746dfbfa885921b302b05e2d2f4695ecd8d9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="developing-custom-objects-for-integration-services"></a>Entwickeln benutzerdefinierter Objekte für Integration Services
  Wenn die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthaltene Ablaufsteuerung und die Datenflussobjekte nicht vollständig Ihren Anforderungen entsprechen, können Sie eine Vielzahl von Typen benutzerdefinierter Objekte selbst entwickeln, darunter:  
  
-   **Benutzerdefinierte Tasks**.  
  
-   **Benutzerdefinierte Verbindungs-Manager**. Stellt eine Verbindung mit externen Datenquellen her, die derzeit nicht unterstützt werden.  
  
-   **Benutzerdefinierte Protokollanbieter**. Protokollieren Paketereignisse in Formaten, die derzeit nicht unterstützt werden.  
  
-   **Benutzerdefinierte Enumeratoren**. Unterstützen die Iteration durch eine Reihe von Objekt- oder Wertformaten, die derzeit nicht unterstützt werden.  
  
-   **Benutzerdefinierte Datenflusskomponenten**. Können als Quellen, Transformationen oder Ziele konfiguriert werden.  
  
 Diese benutzerdefinierte Entwicklung wird durch das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Objektmodell mit Basisklassen vereinfacht, die ein konsistentes und zuverlässiges Framework für Ihre benutzerdefinierte Implementierung bieten.  
  
 Wenn Sie die benutzerdefinierte Funktionalität nicht in mehreren Paketen wiederverwenden müssen, bieten Ihnen der Skripttask und die Skriptkomponente die komplette Leistung einer verwalteten Programmiersprache, bei der erheblich weniger Infrastrukturcode geschrieben werden muss. Weitere Informationen finden Sie unter [Vergleichen von Skriptlösungen und benutzerdefinierten Objekten](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md).  
  
## <a name="steps-in-developing-a-custom-object-for-integration-services"></a>Schritte zur Entwicklung eines benutzerdefinierten Objekts für Integration Services  
 Wenn Sie ein benutzerdefiniertes Objekt zur Verwendung in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] entwickeln, erstellen Sie eine Klassenbibliothek (eine DLL), die zur Entwurfszeit und zur Laufzeit vom SSIS-Designer und von der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Laufzeit geladen wird. Die wichtigsten Methoden, die Sie implementieren müssen, sind nicht die Methoden, die aus Ihrem eigenen Code aufgerufen werden, sondern die Methoden, die von der Laufzeit zu entsprechenden Zeiten aufgerufen werden, um die Komponenten zu initialisieren und zu überprüfen und ihre Funktionalität aufzurufen.  
  
 Nachfolgend sind die Schritte aufgeführt, die Sie bei der Entwicklung eines benutzerdefinierten Objekts befolgen müssen:  
  
1.  Erstellen Sie in Ihrer bevorzugten verwalteten Programmiersprache ein neues Projekt des Typs „Klassenbibliothek“.  
  
2.  Dieses sollte von der entsprechenden Basisklasse erben, wie in der folgenden Tabelle dargestellt.  
  
3.  Übernehmen Sie das entsprechende Attribut für die neue Klasse, wie in der folgenden Tabelle dargestellt.  
  
4.  Überschreiben Sie nach Bedarf die Methoden der Basisklasse, und schreiben Sie den Code für die benutzerdefinierte Funktionalität Ihres Objekts.  
  
5.  Erstellen Sie optional eine benutzerdefinierte Benutzeroberfläche für die Komponente. Um die Bereitstellung zu erleichtern, können Sie die Benutzeroberfläche als separates Projekt innerhalb der gleichen Lösung entwickeln und sie als separate Assembly erstellen.  
  
6.  Sie können optional einen Link zu Beispielen und Hilfeinhalt für das benutzerdefinierte Objekt in der **SSIS-Toolbox** anzeigen.  
  
7.  Beachten Sie beim Erstellen, Bereitstellen und Debuggen Ihres neuen benutzerdefinierten Objekts die Beschreibungen in [Erstellen, Bereitstellen und Debuggen von benutzerdefinierten Objekten](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="base-classes-attributes-and-important-methods"></a>Basisklassen, Attribute und wichtige Methoden  
 Die nachfolgende Tabelle bietet eine einfache Übersicht über die meisten wichtigen Elemente im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Objektmodell für die einzelnen Typen von benutzerdefinierten Objekten, die Sie entwickeln können.  
  
|Benutzerdefiniertes Objekt|Basisklasse|attribute|Wichtige Methoden|  
|-------------------|----------------|---------------|-----------------------|  
|Task|<xref:Microsoft.SqlServer.Dts.Runtime.Task>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>|  
|Ziel-Editor für Dimensionsverarbeitung|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>|  
|Protokollanbieter|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>|  
|Enumerator|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>|  
|Datenflusskomponente|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>|<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>|  
  
## <a name="providing-links-to-samples-and-help-content"></a>Bereitstellen von Links zu Beispielen und Hilfeinhalt  
 Verwenden Sie die folgenden Eigenschaften, um einen Link zu Beispielen und Hilfeinhalt für ein benutzerdefiniertes Objekt, das in verwaltetem Code geschrieben wurde, in der **SSIS-Toolbox** anzuzeigen.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpKeyword%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpKeyword%2A>  
  
 Um einen Link zu Beispielen und Hilfeinhalt für ein benutzerdefiniertes Objekt anzuzeigen, das im systemeigenen Code geschrieben wurde, fügen Sie Einträge in der Registrierungsskriptdatei (.rgs) für SamplesTag, HelpKeyword und HelpCollection hinzu. Im Folgenden finden Sie ein Beispiel.  
  
 `val HelpKeyword = s 'sql11.dts.designer.executepackagetask.F1'`  
  
 `val SamplesTag = s 'ExecutePackageTask'`  
  
## <a name="providing-a-custom-user-interface"></a>Bereitstellen einer benutzerdefinierten Benutzeroberfläche  
 Damit Benutzer Ihres benutzerdefinierten Objekts dessen Eigenschaften konfigurieren können, müssen Sie möglicherweise auch eine benutzerdefinierte Benutzeroberfläche entwickeln. In Fällen, in denen eine benutzerdefinierte Benutzeroberfläche nicht ausdrücklich erforderlich ist, können Sie eine solche Oberfläche erstellen, um eine benutzerfreundlichere Oberfläche als den standardmäßigen Editor bereitzustellen.  
  
 In einem benutzerdefinierten Benutzeroberflächenprojekt oder einer entsprechenden Assembly gibt es im Allgemeinen zwei Klassen: eine Klasse, die eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Schnittstelle für Benutzeroberflächen für den speziellen Typ des benutzerdefinierten Objekts implementiert, und das Windows Form, in dem diese angezeigt wird, um Informationen vom Benutzer zu erfassen. Die von Ihnen implementierten Oberflächen weisen nur wenige Methoden auf, und die Entwicklung einer benutzerdefinierten Benutzeroberfläche ist ganz einfach.  
  
> [!NOTE]  
>  Viele [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Protokollanbieter verfügen über eine benutzerdefinierte Benutzeroberfläche, die <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> implementiert und das Textfeld **Konfiguration** durch eine gefilterte Dropdownliste der verfügbaren Verbindungs-Manager ersetzt. Individuelle Benutzeroberflächen für benutzerdefinierte Protokollanbieter werden in dieser Version von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] jedoch nicht implementiert. Das Angeben eines Werts für die <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A>-Eigenschaft von <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> hat keine Auswirkungen.  
  
 Die nachfolgende Tabelle bietet eine einfache Übersicht über die Oberflächen, die Sie implementieren müssen, wenn Sie eine benutzerdefinierte Benutzeroberfläche für die einzelnen Typen eines benutzerdefinierten Objekts entwickeln. Es wird auch erläutert, was dem Benutzer angezeigt wird, wenn Sie keine benutzerdefinierte Oberfläche für Ihr Objekt entwickeln möchten, oder wenn Sie Ihr Objekt nicht mithilfe der **UITypeName**-Eigenschaft in dem Attribut des Objekts mit seiner Benutzeroberfläche verknüpfen. Der leistungsstarke Erweiterte Editor mag für eine Datenflusskomponente zwar zufriedenstellend sein, das Eigenschaftenfenster stellt jedoch eine weniger benutzerfreundliche Lösung für Tasks und Verbindungs-Manager dar. Ohne ein benutzerdefiniertes Formular kann ein benutzerdefinierter ForEach-Enumerator überhaupt nicht konfiguriert werden.  
  
|Benutzerdefiniertes Objekt|Basisklasse für Benutzeroberfläche|Standardmäßiges Bearbeitungsverhalten, wenn keine benutzerdefinierte Benutzeroberfläche bereitgestellt wird|  
|-------------------|-----------------------------------|----------------------------------------------------------------------|  
|Task|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|Nur das Eigenschaftenfenster|  
|Ziel-Editor für Dimensionsverarbeitung|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>|Nur das Eigenschaftenfenster|  
|Protokollanbieter|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI><br /><br /> (Nicht in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] implementiert)|Textfeld in der Spalte **Konfiguration**|  
|Enumerator|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>|Nur das Eigenschaftenfenster. Der Bereich für die Enumeratorkonfiguration des Editors ist leer.|  
|Datenflusskomponente|<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>|Erweiterter Editor|  
  
## <a name="external-resources"></a>Externe Ressourcen  
  
-   Blogeintrag; [Erstellungsprozess für Visual Studio-Projektmappen gibt eine Warnung über die indirekte Abhängigkeit von der .NET Framework-Assembly aufgrund von SSIS-Verweisen zurück](http://go.microsoft.com/fwlink/?LinkId=215662) (auf blogs.msdn.com).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Beibehalten von benutzerdefinierten Objekten](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [Erstellen, Bereitstellen und Debuggen von benutzerdefinierten Objekten](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
  
  
