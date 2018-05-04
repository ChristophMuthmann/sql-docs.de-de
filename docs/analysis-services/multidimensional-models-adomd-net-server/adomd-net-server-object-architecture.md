---
title: ADOMD.NET-serverobjektarchitektur | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 85351efb901ca62d8943f7481e8cef57ddcb6b5a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
  
