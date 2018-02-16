---
title: Entwickeln mit Analysis Management Objects (AMO) | Microsoft Docs
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, programming
- AMO, programming
ms.assetid: 91354fc9-22da-4724-b97f-3b1e7b0e69d3
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4a44da0b795bcb7e8ed05510d8caf0178bb789e5
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="developing-with-analysis-management-objects-amo"></a>Entwickeln mit Analysis Management Objects (AMO)
Analysis Management Objects (AMO) ist die vollständige Bibliothek von Objekten, die eine Anwendung zum Verwalten einer laufenden Instanz von ermöglicht [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].

In diesem Abschnitt werden die AMO-Konzepte erläutert, wobei schwerpunktmäßig auf die Hauptobjekte und darauf, wie und wann diese verwendet werden und wie sie miteinander in Beziehung stehen, eingegangen wird. Weitere Informationen über bestimmte Objekte oder Klassen finden Sie unter:

- ["Microsoft.AnalysisServices" Namespace](http://msdn.microsoft.com/library/microsoft.analysisservices.aspx), Referenzdokumentation
- [Analysis Services Management Objects (AMO)](http://www.bing.com/search?q=Analysis+Services+Management+Objects+%28AMO%29), als eine allgemeine Bing.com-Suche.


 **Neu in SQLServer 2016**

AMO wird in SQL Server 2016 in mehreren Assemblys umgestaltet. Generische Klassen, z. B. werden die Server, Datenbank und Rollen in der **"Microsoft.AnalysisServices.Core"** Namespace. Multidimensional-spezifische APIs verbleiben im ["Microsoft.AnalysisServices" Namespace](https://msdn.microsoft.com/library/ms146720.aspx).

Benutzerdefinierte Skripts und Anwendungen, die auf früheren Versionen von AMO geschrieben werden ohne weitere Änderungen funktionieren weiterhin. Werden Sie Skripts oder Anwendungen, die auf SQL Server 2016 speziell haben oder wenn Sie eine benutzerdefinierte Lösung neu erstellen müssen, jedoch sicher, dass die neue Assembly und den Namespace zu Ihrem Projekt hinzugefügt.

## <a name="see-also"></a>Siehe auch
[Entwickeln mit Analysis Services Scripting Language &#40; ASSL &#41; ](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md) 
 [Entwickeln mit XMLA in Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)
