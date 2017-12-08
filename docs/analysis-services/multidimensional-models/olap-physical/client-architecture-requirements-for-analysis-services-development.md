---
title: "Anforderungen an die Clientarchitektur für Analysis Services-Entwicklung | Microsoft Docs"
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
- local mining models [Analysis Services]
- Analysis Services, architecture
- providers [Analysis Services]
- data pumps [Analysis Services]
- client architecture [Analysis Services]
- local cubes [Analysis Services]
ms.assetid: 03a8eb6b-159f-4a0a-afbe-06a2424b6090
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b15bbb83f989f53ef8e8b959771f5bd7fa568a12
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="client-architecture-requirements-for-analysis-services-development"></a>Anforderungen an die Clientarchitektur für die Analysis Services-Entwicklung
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] unterstützt eine thin Client-Architektur. Die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Berechnungsmodul ist vollständig serverbasiert, sodass alle Abfragen auf dem Server aufgelöst werden. Daher ist für jede Abfrage nur ein Roundtrip zwischen dem Client und dem Server erforderlich, was zu skalierbarer Leistung führt, wenn die Komplexität der Abfragen zunimmt.  
  
 Das native Protokoll für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ist XMLA (XML for Analysis). [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] stellt mehrere Datenzugriffsschnittstellen für Clientanwendungen zur Verfügung. Diese Komponenten verwenden jedoch alle XMLA für die Kommunikation mit einer Instanz von [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Zusammen mit [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] werden mehrere unterschiedliche Anbieter zur Verfügung gestellt, um unterschiedliche Programmiersprachen zu unterstützen. Ein Anbieter kommuniziert mit einem Server mit [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], indem XMLA in SOAP-Paketen über TCP/IP oder durch Internetinformationsdienste (Internet Information Services, IIS) über HTTP gesendet und empfangen wird. Eine HTTP-Verbindung verwendet ein von IIS instanziiertes COM-Objekt, das als Datapump bezeichnet wird und als Datenleitung für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Daten fungiert. Die im HTTP-Datenstrom enthaltenen zugrunde liegenden Daten werden von der Datapump nicht untersucht, und auch die zugrunde liegenden Datenstrukturen stehen für Code in der Datenbibliothek selbst nicht zur Verfügung.  
  
 ![Logische Clientarchitektur für Analysis Services](../../../analysis-services/multidimensional-models/olap-physical/media/as-clientarch9.gif "logische Clientarchitektur für Analysis Services")  
  
 Win32-Clientanwendungen können mithilfe von OLE DB für OLAP-Schnittstellen oder mithilfe des Microsoft® ActiveX® Data Objects-Objektmodells (ADO) für COM-Automatisierungssprachen (Component Object Model) wie Microsoft Visual Basic® Verbindungen zu einem Server mit [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] herstellen. Mit .NET-Sprachen codierte Anwendungen können [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] an einen Server mithilfe von ADOMD.NET verbunden werden.  
  
 Vorhandene Anwendungen können ohne Änderungen mit [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] kommunizieren, indem dazu einer der [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Anbieter verwendet wird.  
  
|Programmiersprache|Datenzugriffsschnittstelle|  
|--------------------------|---------------------------|  
|C++|OLE DB für OLAP (OLE DB for OLAP)|  
|Visual Basic 6|ADO MD|  
|.NET-Sprachen|ADO MD.NET|  
|Alle Sprachen, die SOAP unterstützen|XML für Analysis|  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] verfügt über eine Webarchitektur mit einer vollständig skalierbaren mittleren Ebene, die sowohl in kleineren als auch in großen Organisationen bereitgestellt werden kann. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] stellt umfassende Unterstützung auf mittlerer Ebene für Webdienste zur Verfügung. ASP-Anwendungen werden von OLE DB für OLAP und ADO MD unterstützt, ASP.NET-Anwendungen werden von ADOMD.NET unterstützt. Die mittlere Ebene ist für viele gleichzeitige Benutzern skalierbar, wie die folgende Abbildung veranschaulicht.  
  
 ![Logisches Diagramm für die Architektur der mittleren Ebene](../../../analysis-services/multidimensional-models/olap-physical/media/as-midtierarch9.gif "logisches Diagramm für die Architektur der mittleren Ebene")  
  
 Sowohl Clientanwendungen als auch Anwendungen der mittleren Ebene können direkt ohne Verwendung eines Anbieters mit [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] kommunizieren. Clientanwendungen und Anwendungen der mittleren Ebene können XMLA in SOAP-Paketen über TCP/IP, HTTP oder HTTPS senden. Der Client kann mithilfe jeder Sprache codiert werden, die SOAP unterstützt. In diesem Fall kann die Kommunikation am einfachsten mithilfe von HTTP über Internetinformationsdienste verwaltet werden, obwohl eine direkte Verbindung zum Server mithilfe von TCP/IP ebenfalls codiert werden kann. Die ist die minimal mögliche Clientlösung für [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="analysis-services-in-tabular-or-sharepoint-mode"></a>Analysis Services im tabellarischen oder SharePoint-Modus  
 In [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], der Server gestartet werden, im xVelocity Datenanalyse im Arbeitsspeicher (VertiPaq) Modulmodus für tabellarische Datenbanken und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Arbeitsmappen, die auf einer SharePoint-Website veröffentlicht wurden.  
  
 [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] und [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] sind die einzigen Clientumgebungen, die zum Erstellen und Abfragen von Datenbanken im Arbeitsspeicher unterstützt werden und den SharePoint- bzw. den tabellarischen Modus verwenden. Der eingebettete [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Datenbank, die Sie erstellen, indem Sie mit Excel und [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Tools ist in der Excel-Arbeitsmappe enthalten und wird als Teil der Excel-XLSX-Datei gespeichert.  
  
 Eine [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Arbeitsmappe kann Daten verwenden, die in einem herkömmlichen Cube gespeichert werden, wenn Sie die Cubedaten in die Arbeitsmappe importieren. Sie können auch Daten aus einer anderen [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Arbeitsmappe importieren, wenn diese zu einer SharePoint-Website veröffentlicht wurde.  
  
> [!NOTE]  
>  Wenn Sie einen Cube als Datenquelle für eine [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]-Arbeitsmappe verwenden, werden die Daten, die Sie vom Cube erhalten, als MDX-Abfrage definiert; die Daten werden jedoch als vereinfachte Momentaufnahme importiert. Sie können mit den Daten nicht interaktiv arbeiten oder die Daten vom Cube aktualisieren.  
  
 Weitere Informationen zum Verwenden eines SSAS-Cubes als Datenquelle finden Sie unter der [Power Pivot für Excel](http://go.microsoft.com/fwlink/?LinkId=164234).  
  
### <a name="interfaces-for-power-pivot-client"></a>Schnittstellen für PowerPivot-Client  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]interagiert mit dem xVelocity Datenanalyse im Arbeitsspeicher (VertiPaq) Modul innerhalb der Arbeitsmappe mithilfe der bestehenden Schnittstellen und Sprachen für Analysis Services: AMO und ADOMD.NET und MDX und XMLA. Innerhalb des Add-Ins werden Measures durch eine Formelsprache wie Excel, Data Analysis Expressions (DAX), ähnlich definiert. DAX-Ausdrücke werden innerhalb der XMLA-Meldungen eingebettet, die an den prozessinternen Server gesendet werden.  
  
### <a name="providers"></a>Anbieter  
 Kommunikation zwischen [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] und Excel verwendet den MSOLAP-OLEDB-Anbieter (Version 11.0). Innerhalb des MSOLAP-Anbieters gibt es vier verschiedene Module oder Transporte, das zum Senden von Meldungen zwischen Client und Server verwendet werden können.  
  
 **TCP/IP** für normale Client / Server-Verbindungen verwendet.  
  
 **HTTP** für HTTP-Verbindungen über den SSAS-datapumpdienst oder durch einen Aufruf an den SharePoint verwendet [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Web Service (WS) Komponente.  
  
 **INPROC** für Verbindungen zum prozessinternen Modul verwendet.  
  
 **Kanal** reserviert für die Kommunikation mit dem [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] -Systemdienst in der SharePoint-Farm.  
  
## <a name="see-also"></a>Siehe auch  
 [OLAP-Modulserverkomponenten](../../../analysis-services/multidimensional-models/olap-physical/olap-engine-server-components.md)  
  
  
