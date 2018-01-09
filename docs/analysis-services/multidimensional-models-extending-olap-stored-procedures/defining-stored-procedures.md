---
title: Definieren von gespeicherten Prozeduren | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- stored procedures [Analysis Services]
- OLAP [Analysis Services], stored procedures
- external routines [Analysis Services]
- stored procedures [Analysis Services], about stored procedures
ms.assetid: f9c57d91-f60f-4f0e-8f7f-d87f4ba97b7c
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: af5d0ffc0b7aaa1b03ca4166d59667692566b036
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="defining-stored-procedures"></a>Definieren von gespeicherten Prozeduren
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Können Sie gespeicherte Prozeduren aufrufen, externe Routinen über [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Sie können den Aufruf von externen Routinen über eine gespeicherte Prozedur in jeder beliebigen CLR-Sprache (Common Language Runtime) schreiben, z. B. C, C++, C#, Visual Basic oder Visual Basic .NET. Eine gespeicherte Prozedur kann einmal erstellt werden und dann in zahlreichen Kontexten aufgerufen werden, z. B. von anderen gespeicherten Prozeduren, berechneten Measures oder Clientanwendungen. Gespeicherte Prozeduren vereinfachen die Entwicklung und Implementierung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbanken, da gemeinsamer Code nur einmal entwickelt werden muss und an einem einzelnen Ort gespeichert werden kann. Mit gespeicherten Prozeduren kann Anwendungen Geschäftsfunktionalität hinzugefügt werden, die von der systemeigenen Funktionalität von MDX nicht bereitgestellt wird.  
  
 Dieser Abschnitt enthält die Informationen, die zum Verständnis, Entwurf und zur Implementierung von gespeicherten Prozeduren erforderlich sind.  
  
|Thema|Description|  
|-----------|-----------------|  
|[Entwerfen gespeicherter Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/designing-stored-procedures.md)|Beschreibt das Entwerfen von Assemblys zum Verwenden mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Erstellen gespeicherter Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)|Beschreibt das Erstellen von Assemblys für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Aufrufen gespeicherter Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/calling-stored-procedures.md)|Stellt Informationen zum Verwenden von Assemblys in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bereit.|  
|[Zugreifen auf den Abfragekontext in gespeicherten Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/accessing-query-context-in-stored-procedures.md)|Beschreibt das Zugreifen auf Informationen zum Gültigkeitsbereich und Kontext mit Assemblys.|  
|[Festlegen der Sicherheit für gespeicherte Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)|Beschreibt das Konfigurieren der Sicherheit für Assemblys in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[Debuggen gespeicherter Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md)|Beschreibt das Debuggen von Assemblys in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
  
## <a name="see-also"></a>Siehe auch  
 [Verwaltung von mehrdimensionalen Modellassemblys](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
