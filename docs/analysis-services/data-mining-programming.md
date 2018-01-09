---
title: Datamining-Programmierungsverfahren | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016 Preview
helpviewer_keywords: data mining [Analysis Services], developer's guide
ms.assetid: 9fd77b16-0b89-44ce-bcf1-7c04b62499da
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a401073a7bcf0d7e8559c65ab6b05d25bd2a681e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="data-mining-programming"></a>Data Mining-Programmierung
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]Wenn sich die integrierten Tools und Viewer ggf. Folgendes herausstellen [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nicht Ihren Anforderungen entsprechen, Sie können die Effektivität von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] durch codieren eigener Erweiterungen erhöhen. Dabei haben Sie zwei Möglichkeiten:  
  
-   **XMLA**  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]unterstützt XML for Analysis (XMLA) als Protokoll für die Kommunikation mit Clientanwendungen. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] unterstützt zusätzliche Befehle, die die XML for Analysis-Spezifikation erweitern.  
  
     Weil in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] für die Datendefinition, Datenbearbeitung und Datenkontrolle XMLA verwendet, können Sie Miningstrukturen und Miningmodelle mithilfe der in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] bereitgestellten visuellen Tools erstellen und anschließend die erstellten Data Mining-Objekte mithilfe der Data Mining Extensions (DMX)- und Analysis Services Scripting Language (ASSL)-Skripts erweitern.  
  
     Sie können Data Mining-Objekte vollständig in XMLA-Skripts erstellen und ändern und aus Ihren eigenen Anwendungen programmgesteuert Vorhersageabfragen für die Modelle ausführen.  
  
-   **Analysis Management Objects (AMO)**  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] stellt außerdem ein vollständiges Framework bereit, das Data Mining-Drittanbietern die Integration der Data Mining-Objekte in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ermöglicht.  
  
     Sie können Miningstrukturen und Miningmodelle mithilfe von AMO erstellen. Siehe die folgenden Beispiele in CodePlex:  
  
    -   AMO-Browser  
  
         Stellt eine Verbindung mit der angegebenen SSAS-Instanz her und listet alle Serverobjekte und deren Eigenschaften auf, einschließlich Miningstruktur und Miningmodelle.  
  
    -   AMO Simple Sample  
  
         Im AS Simple Sample werden folgende Verfahren behandelt: programmgesteuerter Zugriff auf die meisten Hauptobjekte, Durchsuchen von Metadaten und Zugriff auf Werte in Objekten.  
  
         Das Beispiel veranschaulicht auch, wie Sie eine Data Mining-Struktur und ein Data Mining-Modell erstellen und verarbeiten und wie ein vorhandenes Data Mining-Modell durchsucht wird.  
  
-   **DMX**  
  
     DMX kann verwendet werden, um Befehlsanweisungen, Vorhersageabfragen und Metadatenabfragen zu kapseln und Ergebnisse im Tabellenformat zurückzugeben, vorausgesetzt, Sie haben eine Verbindung mit einem [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]-Server hergestellt.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [OLE DB für Datamining](../analysis-services/data-mining-programming-ole-db.md)  
 Beschreibt Erweiterungen der Spezifikation zur Unterstützung von Data Mining und mehrdimensionalen Daten: neue Schemarowsets und -spalten, Data Mining Extensions (DMX)-Sprache zum Erstellen und Verwalten von Miningstrukturen.  
  
## <a name="related-reference"></a>Verwandter Verweis  
 [Entwickeln mit ADOMD.NET](../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
 Bietet eine Einführung in ADOMD.NET-Client- und Server-Programmierobjekte.  
  
 [Entwickeln mit Analysis Management Objects &#40; AMO &#41;](../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
 Stellt die AMO-Programmierbibliothek vor.  
  
 [Entwickeln mit Analysis Services Scripting Language &#40; ASSL &#41;](../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
 Gibt eine Einführung in XML for Analysis (XMLA) und die zugehörigen Erweiterungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwicklerhandbuch (Analysis Services)](../analysis-services/analysis-services-developer-documentation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Referenz](../dmx/data-mining-extensions-dmx-reference.md)  
  
  
