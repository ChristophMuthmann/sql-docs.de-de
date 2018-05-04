---
title: XML for Analysis (XMLA)-Referenz | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XML for Analysis, reference
- XMLA, reference
ms.assetid: 88045e05-ce47-4e28-999b-7f9c74af9faf
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 296d0ea9c77530151c4ae159968896b00dc40a3a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xml-for-analysis--xmla-reference"></a>XML for Analysis (XMLA)-Referenz
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet die XML for Analysis (XMLA)-Protokoll zum Verarbeiten aller Kommunikation zwischen Clientanwendungen und einer Analysis Services-Instanz an. Die Erstellung von Anforderungen und Decodierung von Antworten in anderen Clientbibliotheken, z. B. ADOMD.NET und AMO, erfolgt auf elementarster Ebene in XMLA und dient als Zwischenstufe für eine Analysis Services-Instanz, die ausschließlich XMLA verwendet.  
  
 Um die Ermittlung und Bearbeitung von Daten in multidimensionalen und tabellarischen Format zu unterstützen, die XMLA-Spezifikation definiert zwei allgemein verfügbare Methoden [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) und [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md), und ein die Auflistung von XML-Elemente und Datentypen. Da XML eine lose verbundene Client- und Server-Architektur ermöglicht, wickeln beide Methoden eingehende und ausgehende Informationen im XML-Format ab. Analysis Services ist mit der XMLA 1.1-Spezifikation -Spezifikation, erweitert diese Datendefinitions- und Bearbeitungsfunktionen zusätzliche Verarbeitungskapazität, implementiert als Anmerkungen auf Einbeziehung jedoch die **Discover** und **Execute** Methoden. Die erweiterte XML-Syntax wird als Analysis Services Scripting Language (ASSL) bezeichnet. ASSL baut auf der XMLA-Spezifikation auf, ohne diese zu verletzen. Die XMLA-Interoperabilität ist unabhängig davon gewährleistet, ob lediglich XMLA verwendet oder ob XMLA und ASSL kombiniert werden.  
  
 Als Programmierer können Sie XMLA als befehlsorientierte Benutzerschnittstelle verwenden, wenn für eine Lösung Standardprotokolle, wie XML, SOAP und HTTP, erforderlich sein sollten. Programmierer und Administratoren können XMLA auch auf einer Ad-hoc-Basis verwenden, um Informationen vom Server abzurufen oder Befehle auszuführen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[XML-Elemente & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)|Beschreibt Elemente in der XMLA-Spezifikation.|  
|[XML-Datentypen &#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)|Beschreibt Datentypen in der XMLA-Spezifikation.|  
|[XML for Analysis-Kompatibilität &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)|Beschreibt den Grad der Kompatibilität mit der XMLA 1.1-Spezifikation.|  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
 [Entwickeln mit Analysis Services Scripting Language & #40; ASSL & #41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
  
 [XML for Analysis-Schemarowsets](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 [Entwickeln mit ADOMD.NET](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
 [Entwickeln mit Analysis Management Objects & #40; AMO & #41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zur Microsoft OLAP-Architektur](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
