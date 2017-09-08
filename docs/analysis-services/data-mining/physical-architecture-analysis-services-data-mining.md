---
title: "Physische Architektur (Analysis Services – Datamining) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- server architecture [Analysis Services]
- architecture [Analysis Services]
ms.assetid: 25eeecf0-6e85-4527-b94d-5503d27edaed
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b1e79889b8023a94d6f7bbc8d3e9f4ca75c5273
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="physical-architecture-analysis-services---data-mining"></a>Physische Architektur (Analysis Services &ndash; Data Mining)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet sowohl Server- als auch Clientkomponenten zum Bereitstellen von Data Mining-Funktionen für Business Intelligence-Anwendungen:  
  
-   Die Serverkomponente wird als Microsoft Windows-Dienst implementiert. Sie können mehrere Instanzen auf dem gleichen Computer verwenden, wobei jede Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] als separate Instanzen des Windows-Diensts implementiert.  
  
-   Clients kommunizieren mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mithilfe des öffentlichen Standards für XMLA (XML for Analysis). Hierbei handelt es sich um ein SOAP-basiertes Protokoll für die Ausgabe von Befehlen und den Empfang von Antworten in Form eines Webdiensts. Clientobjektmodelle werden ebenfalls über XMLA bereitgestellt. Auf diese Modelle kann sowohl ein verwalteter Anbieter (ADOMD.NET) als auch ein eigener OLE DB-Anbieter zugreifen.  
  
-   Abfragebefehle können mithilfe von DMX (Data Mining Extensions), einer speziellen Abfragesprache für Data Mining nach Industriestandard, ausgegeben werden. ASSL (Analysis Services Scripting Language) kann außerdem zum Verwalten von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankobjekten verwendet werden.  
  
## <a name="architectural-diagram"></a>Architekturdiagramm  
 Eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz wird als eigenständiger Dienst ausgeführt, und die Kommunikation mit dem Dienst erfolgt in XMLA (XML for Analysis) über HTTP oder TCP.  
  
 AMO ist eine Ebene zwischen der Benutzeranwendung und der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz, die Zugriff auf [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verwaltungsobjekte bietet. AMO ist eine Klassenbibliothek, die Befehle von Clientanwendungen entgegennimmt und diese Befehle in XMLA-Nachrichten für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz übersetzt. AMO stellt Objekte der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz für die Endbenutzerumgebung als Klassen dar, wobei Methodenmember Befehle ausführen und Eigenschaftenmember die Daten für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte speichern.  
  
 Die folgende Abbildung stellt die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Komponentenarchitektur dar, einschließlich der Dienste in der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz und der Benutzerkomponenten, die mit der Instanz zusammenarbeiten.  
  
 Diese Abbildung zeigt, dass nur mit dem XMLA (XML for Analysis)-Listener entweder über HTTP oder TCP auf die Instanz zugegriffen werden kann.  
  
> [!WARNING]  
>  DSO wurde als veraltet markiert. Sie sollten DSO daher nicht zum Entwickeln von Lösungen verwenden.  
  
 ![Analysis Services-System-Architekturdiagramm](../../analysis-services/data-mining/media/analysisservicessystemarchitecture.gif "Analysis Services-System-Architekturdiagramm")  
  
## <a name="server-configuration"></a>Serverkonfiguration  
 Eine Serverinstanz kann mehrere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken unterstützen, wobei jede über eine eigene Instanz des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Diensts verfügt, der Clientanforderungen beantwortet und Objekte verarbeitet.  
  
 Wenn Sie sowohl tabellarischen Modelle als auch Data Mining-Modelle und/oder mehrdimensionale Modelle verwenden möchten, müssen Sie separate Instanzen installieren. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt die parallele Installation von Instanzen, die im tabellarischen Modus ausgeführt werden (der das xVelocity-Modul für Datenanalyse im Arbeitsspeicher (VertiPaq) verwendet), sowie Instanzen, die in einer der konventionellen OLAP-, MOLAP- oder ROLAP-Konfigurationen ausgeführt werden. Weitere Informationen finden Sie unter [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Die gesamte Kommunikation zwischen einem Client und dem Analysis Services-Server verwendet XMLA. Hierbei handelt es sich um ein plattform- und sprachenunabhängiges Protokoll. Wenn eine Anforderung von einem Client eingeht, wird von Analysis Services bestimmt, ob die Anforderung sich auf OLAP oder Data Mining bezieht, und die Anforderung wird entsprechend weitergeleitet. Weitere Informationen finden Sie unter [OLAP-Modulserverkomponenten](../../analysis-services/multidimensional-models/olap-physical/olap-engine-server-components.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Logische Architektur &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/logical-architecture-analysis-services-data-mining.md)  
  
  
