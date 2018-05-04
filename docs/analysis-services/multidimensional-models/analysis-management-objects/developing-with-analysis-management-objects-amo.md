---
title: Entwickeln mit Analysis Management Objects (AMO) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: edd91a0d4608f03dd622ef2b25820d10f9b4f455
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
[Entwickeln mit Analysis Services Scripting Language &#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)
[Entwickeln mit XMLA in Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)
