---
title: ADOMD.NET-serverobjektarchitektur | Microsoft Docs
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
- ADOMD.NET, object model
- object model [ADOMD.NET]
ms.assetid: bdc81de9-b390-4654-b62a-cd6c0c9ca10d
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8f0cae374f2670228bbced569d81e87b34a350d2
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="adomdnet-server-object-architecture"></a>ADOMD.NET-Serverobjektarchitektur
  Die ADOMD.NET-Serverobjekte sind Hilfsobjekte, die zum Erstellen von benutzerdefinierten Funktionen (UDFs) oder in gespeicherten Prozeduren verwendet werden können [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Verwenden der **Microsoft.AnalysisServices.AdomdServer** Namespace (und diese Objekte), muss eine Referenz auf msmgdsrv.dll zum Projekt der benutzerdefinierten Funktion oder gespeicherten Prozedur hinzugefügt werden.  
  
 ![Zeigt die objektbeziehungen im ADOMD.NET-Server](../../analysis-services/multidimensional-models-adomd-net-server/media/adomdnetserverobjectmodel.gif "zeigt die objektbeziehungen im ADOMD.NET-Server")  
ADOMD.NET-Objektmodell  
  
 Die Interaktion mit der ADOMD.NET-Objekthierarchie beginnt normalerweise mit einem oder mehreren der Objekte auf der obersten Ebene, wie in der folgenden Tabelle erläutert.  
  
|Aktion|Verwenden Sie dieses Objekt|  
|--------|---------------------|  
|Auswerten von MDX-Ausdrücken (Multidimensional Expressions)|<xref:Microsoft.AnalysisServices.AdomdServer.Expression><br /> Das <xref:Microsoft.AnalysisServices.AdomdServer.Expression>-Objekt stellt eine Möglichkeit bereit, einen MDX-Ausdruck auszuführen und diesen Ausdruck unter einem bestimmten Tupel auszuwerten.|  
|Bereitstellen von Unterstützung für die Ausführung von MDX-Funktionen ohne Erstellung der vollständigen MDX-Anweisung|<xref:Microsoft.AnalysisServices.AdomdServer.MDX><br /> Das <xref:Microsoft.AnalysisServices.AdomdServer.MDX>-Objekt ist zweckmäßig für den Aufruf von vordefinierten MDX-Funktionen ohne die Verwendung des <xref:Microsoft.AnalysisServices.AdomdServer.Expression>-Objekts. Weitere Funktionen für das <xref:Microsoft.AnalysisServices.AdomdServer.MDX>-Objekt werden voraussichtlich in zukünftigen Versionen verfügbar sein.|  
|Darstellen des aktuellen Ausführungskontexts für die UDF|<xref:Microsoft.AnalysisServices.AdomdServer.Context><br /> Das <xref:Microsoft.AnalysisServices.AdomdServer.Context>-Objekt macht Informationen verfügbar wie den aktuellen Cube oder das Miningmodell sowie zahlreiche Metadatensammlungen. Eine Schlüsselverwendung des <xref:Microsoft.AnalysisServices.AdomdServer.Context>-Objekts ist die <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy.CurrentMember%2A>-Eigenschaft des <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy>-Objekts. Diese Schlüsselverwendung ermöglicht dem Autor der UDF oder der gespeicherten Prozedur, Entscheidungen auf der Grundlage des Elements einer bestimmten Dimension zu treffen, auf das sich die Abfrage bezieht.|  
|Erstellen von Sätzen und Tupeln|<xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder>, <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder><br /> <xref:Microsoft.AnalysisServices.AdomdServer.SetBuilder> bietet eine Möglichkeit, unveränderliche Sätze zu erstellen, und <xref:Microsoft.AnalysisServices.AdomdServer.TupleBuilder> bietet eine Möglichkeit, unveränderliche Tupel zu erstellen.|  
|Unterstützung von impliziter Konvertierung und Umwandlung unter den sechs grundlegenden Typen der MDX-Sprache|<xref:Microsoft.AnalysisServices.AdomdServer.MDXValue><br /> Das <xref:Microsoft.AnalysisServices.AdomdServer.MDXValue>-Objekt ermöglicht implizite Konvertierung und Umwandlung unter den folgenden Typen:<br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Hierarchy><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Level><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Member><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Tuple><br /><br /> <xref:Microsoft.AnalysisServices.AdomdServer.Set><br /><br /> Skalare oder Werttypen|  
  
## <a name="see-also"></a>Siehe auch  
 [ADOMD.NET-Serverprogrammierung](../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
