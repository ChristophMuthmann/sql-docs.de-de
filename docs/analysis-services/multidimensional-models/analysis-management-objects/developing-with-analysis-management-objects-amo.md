---
title: Entwickeln mit Analysis Management Objects (AMO) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, programming
- AMO, programming
ms.assetid: 91354fc9-22da-4724-b97f-3b1e7b0e69d3
caps.latest.revision: 47
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f746ed6c0ad7dc9c0702282f7a508d44cca7f8be
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

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

