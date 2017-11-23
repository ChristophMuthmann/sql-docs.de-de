---
title: AMO-Konzepte und-Objektmodell | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- AMO, classes
- Analysis Management Objects, classes
- objects [Analysis Management Objects]
- AMO, objects
- classes [AMO]
- AMO
- Analysis Management Objects
- Analysis Management Objects, objects
ms.assetid: 3b0cdf8e-46d5-4dfe-8b2c-233c27e1473e
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4943e1ff3c3c18814993a85bd108bb473e644726
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="amo-concepts-and-object-model"></a>AMO-Konzepte und -Objektmodell
  Dieses Thema enthält eine Definition von Analysis Management Objects (AMO) Beziehung zwischen AMO und anderen Tools und Bibliotheken in der Architektur des [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], und eine begriffserklärung aller wichtigen Objekte in AMO.  
  
 AMO ist eine vollständige Auflistung von Verwaltungsklassen für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], die programmatisch unter dem Namespace von <xref:Microsoft.AnalysisServices> in einer verwalteten Umgebung verwendet werden können. Die Klassen sind in der Datei AnalysisServices.dll, die sich in der Regel Where befindet enthalten die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup installiert die Dateien unter dem Ordner \100\SDK\Assemblies\\. Um die AMO-Klassen zu verwenden, schließen Sie einen Verweis auf diese Assembly in die Projekte ein.  
  
 Mithilfe von AMO können Sie zum Erstellen, ändern und Löschen von Objekten wie Cubes, Dimensionen, Miningstrukturen und [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbanken; für alle diese Objekte können Aktionen können von der Anwendung in .NET Framework ausgeführt werden. Sie können auch die in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Datenbanken gespeicherten Informationen verarbeiten und aktualisieren.  
  
 Mit AMO können Sie die Daten nicht abfragen. Um die Daten abzufragen, verwenden Sie [Entwickeln mit ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [AMO in der Analysis Services-Architektur](#AMOintheAnalysisServicesArchitecture)  
  
 [AMO-Architektur](#AMOArchitecture)  
  
 [Mithilfe von AMO](#bkmk_UsingAMO)  
  
 [Automatisieren von administrativen Tasks mit AMO](#AutomatingAdministrativeTaskswithAMO)  
  
##  <a name="AMOintheAnalysisServicesArchitecture"></a>AMO in der Analysis Services-Architektur  
 Programmbedingt ist AMO nur für die Objektverwaltung bestimmt und nicht zum Abfragen von Daten. Wenn der Benutzer muss Abfrage [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Daten von einer Clientanwendung, die Clientanwendung die zu verwendende [Entwickeln mit ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
##  <a name="AMOArchitecture"></a>AMO-Architektur  
 AMO ist eine vollständige Bibliothek von Klassen zur Verwaltung einer Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] von einer Clientanwendung in verwaltetem Code in .NET Framework, Version 2.0.  
  
 Die AMO-Bibliothek der Klassen wurde als Hierarchie von Klassen entwickelt, wobei bestimmte Klassen vor anderen instanziiert werden müssen, damit Sie sie in Ihrem Code verwenden können. Es gibt auch Erweiterungsklassen, die jederzeit in Ihrem Code instanziiert werden können. Bevor Sie eine Erweiterungsklasse verwenden, werden Sie jedoch wahrscheinlich mindestens eine Hierarchieklasse instanziieren.  
  
 Die folgende Abbildung ist eine Ansicht der AMO-Hierarchie auf hoher Ebene, die die Hauptklassen enthält. Die Abbildung zeigt die Platzierung der Klassen unter ihren Containern und ihren Peers an. Eine <xref:Microsoft.AnalysisServices.Dimension> gehört zu einer <xref:Microsoft.AnalysisServices.Database> und einem <xref:Microsoft.AnalysisServices.Server> und kann zum selben Zeitpunkt erstellt werden wie eine <xref:Microsoft.AnalysisServices.DataSource> und eine <xref:Microsoft.AnalysisServices.MiningStructure>. Bestimmte Peerklassen müssen instanziiert werden, bevor Sie andere verwenden können. Beispielsweise müssen Sie eine Instanz von <xref:Microsoft.AnalysisServices.DataSource> erstellen, bevor Sie eine neue <xref:Microsoft.AnalysisServices.Dimension> oder <xref:Microsoft.AnalysisServices.MiningStructure> hinzufügen können.  
  
 ![AMO-Klassen allgemeiner Überblick](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-highlevelview-majorobjectshighlighted.gif "allgemeiner Überblick der AMO-Klassen")  
  
 Ein *Hauptobjekt* ist eine Klasse, die ein vollständiges Objekt als gesamte Entität und nicht als Teil eines anderen Objekts darstellt. Hauptobjekte schließen <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension> und <xref:Microsoft.AnalysisServices.MiningStructure> ein, da es sich hierbei um eigenständige Entitäten handelt. Jedoch ist ein <xref:Microsoft.AnalysisServices.Level> kein Hauptobjekt, da es ein Bestandteil einer <xref:Microsoft.AnalysisServices.Dimension> ist. Hauptobjekte können von anderen Objekten unabhängig erstellt, gelöscht, modifiziert oder verarbeitet werden. Nebenobjekte sind Objekte, die nur im Rahmen der Erstellung des übergeordneten Hauptobjekts erstellt werden können. Nebenobjekte werden in der Regel im Anschluss an eine Hauptobjekterstellung erstellt. Die Werte für Nebenobjekte sollten zum Zeitpunkt der Erstellung definiert werden, da es keinen standardmäßigen Erstellungsprozess für Nebenobjekte gibt.  
  
 Die folgende Abbildung zeigt die Hauptobjekte an, die ein <xref:Microsoft.AnalysisServices.Server>-Objekt enthält.  
  
 ![Hervorgehobene AMO-Hauptobjekte](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects.gif "hervorgehobene AMO-Hauptobjekte")  
  
 ![Hervorgehobene AMO-Hauptobjekte (2)](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects-02.gif "hervorgehobene AMO-Hauptobjekte (2)")  
  
 Beim Programmieren mit AMO werden für die Zuordnung zwischen Klassen und enthaltenen Klassen Auflistungstypattribute verwendet, etwa <xref:Microsoft.AnalysisServices.Server> und <xref:Microsoft.AnalysisServices.Dimension>. Zum Verwenden einer Instanz einer enthaltenen Klasse müssen Sie zunächst einen Verweis auf ein Auflistungsobjekt erhalten, das die enthaltene Klasse enthält oder enthalten kann. Anschließend müssen Sie das spezifische Objekt in der Auflistung suchen und dann einen Verweis auf das Objekt abrufen, damit Sie damit arbeiten können.  
  
### <a name="amo-classes"></a>AMO-Klassen  
 AMO ist eine Bibliothek von Klassen, die dazu entworfen wurde, eine Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] über eine Clientanwendung zu verwalten. Die AMO-Bibliothek ist eine Gruppe logisch verbundener Objekte, die verwendet werden, um eine spezifische Aufgabe auszuführen. AMO-Klassen können auf folgende Weise kategorisiert werden:  
  
|Klassensatz|Zweck|  
|---------------|-------------|  
|[Grundlegende AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)|Klassen, die erforderlich sind, um einen beliebigen anderen Satz von Klassen verwenden zu können.|  
|[AMO OLAP-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)|Klassen, mit denen Sie die OLAP-Objekte in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verwalten können.|  
|[AMO-Klassen für Data Mining](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)|Klassen, mit denen Sie die Data Mining-Objekte in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verwalten können.|  
|[AMO-Sicherheitsklassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md)|Klassen, mit denen Sie den Zugriff auf andere Objekte steuern und die Sicherheit aufrechterhalten können.|  
|[Andere AMO-Klassen und -Methoden](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)|Klassen und Methoden, die OLAP- oder Data Mining-Administratoren helfen, ihre täglichen Aufgaben auszuführen.|  
  
##  <a name="bkmk_UsingAMO"></a>Mithilfe von AMO  
 AMO ist insbesondere für die Automatisierung wiederkehrender Tasks hilfreich, beispielsweise für das Erstellen neuer Partitionen in einer Measuregruppe basierend auf neuen Daten in der Faktentabelle oder für das erneute Trainieren eines Miningmodells basierend auf neuen Daten. Diese Tasks, die neue Objekte erstellen, werden in der Regel monatlich, wöchentlich oder vierteljährlich ausgeführt. Die neuen Objekte können problemlos, basierend auf den neuen Daten, von der Anwendung benannt werden.  
  
##### <a name="analysis-services-administrators"></a>Analysis Services-Administratoren  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Administratoren können AMO verwenden, um die Verarbeitung von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Datenbanken zu automatisieren. Zum Entwerfen und Bereitstellen von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Datenbanken sollten Sie [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] verwenden.  
  
##### <a name="developers"></a>Entwickler  
 Entwickler können AMO verwenden, um Administratorschnittstellen für angegebene Sätze von Benutzern zu entwickeln. Diese Schnittstellen können den Zugriff auf [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Objekte einschränken und Benutzer auf bestimmte Tasks beschränken. Beispielsweise können Sie mit AMO eine Sicherungsanwendung erstellen, die es einem Benutzer ermöglicht, alle Datenbankobjekte anzuzeigen, eine beliebige Datenbank auszuwählen und sie auf einem der angegebenen Geräte zu sichern.  
  
 Entwickler können auch [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Logik in ihre Anwendungen einbetten. Hierzu können die Entwickler basierend auf Benutzereingaben oder anderen Faktoren Cubes, Dimensionen, Miningstrukturen und Miningmodelle erstellen.  
  
##### <a name="olap-advanced-users"></a>Fortgeschrittene OLAP-Benutzer  
 Bei fortgeschrittenen OLAP-Benutzern handelt es sich für gewöhnlich um Datenanalysten oder andere erfahrene Datenbenutzer, die über fundierte Programmierkenntnisse verfügen und ihre Datenanalyse durch eine verstärkte Verwendung von Datenobjekten verbessern möchten. Für Benutzer, die offline arbeiten müssen, kann AMO bei der Automatisierung des Erstellungsprozesses lokaler Cubes vor der Trennung vom Netzwerk sehr hilfreich sein.  
  
##### <a name="data-mining-advanced-users"></a>Fortgeschrittene Data Mining-Benutzer  
 Für fortgeschrittene Data Mining-Benutzer ist AMO besonders hilfreich, wenn große Modellmengen in regelmäßigen Abständen neu trainiert werden müssen.  
  
##  <a name="AutomatingAdministrativeTaskswithAMO"></a>Automatisieren von administrativen Tasks mit AMO  
 Die meisten wiederkehrenden Tasks können am besten entwickelt, bereitgestellt und verwaltet werden, wenn sie mithilfe von [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] und nicht als Anwendung in einer Sprache Ihrer Wahl entwickelt werden. Jedoch können Sie AMO für wiederkehrende Tasks verwenden, die nicht mit [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] automatisiert werden können. AMO ist auch hilfreich, wenn Sie mithilfe von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] eine spezialisierte Anwendung für Business Intelligence entwickeln möchten.  
  
##### <a name="automatic-object-management"></a>Automatische Objektverwaltung  
 Mit AMO können ganz einfach [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Objekte (beispielsweise <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, Mining-<xref:Microsoft.AnalysisServices.MiningStructure> und <xref:Microsoft.AnalysisServices.MiningModel> oder <xref:Microsoft.AnalysisServices.Role>) basierend auf Benutzereingaben oder neuen Daten erstellt, aktualisiert oder gelöscht werden. AMO eignet sich optimal für Setupanwendungen, die eine entwickelte Lösung eines unabhängigen Softwareanbieters für einen Endkunden bereitstellen müssen. Die Setupanwendung kann verifizieren, dass eine ältere Version vorhanden ist. Darüber hinaus kann sie die Struktur aktualisieren, nicht länger benötigte Objekt entfernen und neue Objekt erstellen. Wenn es keine frühere Version gibt, kann alles neu erstellt werden.  
  
 AMO kann bei der Erstellung neuer Partitionen basierend auf neuen Daten sehr hilfreich sein. Alte Partitionen, die über den Umfang des Projekts hinausgehen, können entfernt werden. Beispielsweise kann bei einer Lösung für Finanzanalysen, die mit den Daten der vergangenen 36 Monate arbeitet, der 37. Monat entfernt werden, sobald Daten für einen neuen Monat empfangen werden. Um die Leistung zu verbessern, können neue Aggregationen basierend auf der Verwendung erstellt und auf die letzten 12 Monate angewendet werden.  
  
##### <a name="automatic-object-processing"></a>Automatische Objektverarbeitung  
 Objektverarbeitung und aktualisierte Verfügbarkeit können erreicht werden, indem AMO zum Antworten auf bestimmte Ereignisse außerhalb des gewöhnlichen Datenflusses und der geplanten Tasks genutzt wird, die von [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] verwendet werden.  
  
##### <a name="automatic-security-management"></a>Automatische Sicherheitsverwaltung  
 Die Sicherheitsverwaltung kann für das Einbeziehen neuer Benutzer für Rollen und Berechtigungen oder für das Entfernen anderer Benutzer nach Überschreitung des angegebenen Zeitraums automatisiert werden. Neue Schnittstellen können erstellt werden, um die Sicherheitsverwaltung für Sicherheitsadministratoren zu vereinfachen. Dieser Vorgang kann einfacher sein als die Verwendung von [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
##### <a name="automatic-backup-management"></a>Automatische Sicherungsverwaltung  
 Die automatische Sicherungsverwaltung kann mithilfe von [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]-Tasks oder durch das Erstellen spezialisierter AMO-Anwendungen, die automatisch ausgeführt werden, vorgenommen werden. Mit AMO können Sie Sicherungsschnittstellen für Operatoren entwickeln, die ihnen bei ihren täglichen Aufgaben helfen.  
  
##### <a name="tasks-amo-is-not-intended-for"></a>Tasks, für die AMO nicht bestimmt ist  
 AMO kann nicht verwendet werden, um die Daten abzufragen. Verwenden Sie zum Abfragen von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Daten, einschließlich Cubes und Miningmodellen, ADOMD.NET in einer Benutzeranwendung. Weitere Informationen finden Sie unter [Entwickeln mit ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
  
