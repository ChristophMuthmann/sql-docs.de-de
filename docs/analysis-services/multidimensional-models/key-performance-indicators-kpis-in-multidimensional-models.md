---
title: Key Performance Indicators (KPIs) in mehrdimensionalen Modellen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing Key Performance Indicators
- Key Performance Indicators [Analysis Services]
- KPIs [Analysis Services]
- OLAP objects [Analysis Services], performance indicators
- weights [Analysis Services]
- displaying Key Performance Indicators
- parent KPIs [Analysis Services]
- child KPIs
ms.assetid: 73aee2da-da30-44f1-829c-0a4c078a7768
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 166c09d9d8b2c767767ffda7914f8d465af43829
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="key-performance-indicators-kpis-in-multidimensional-models"></a>Leistungskennzahlen (Key Performance Indicators, KPIs) in mehrdimensionalen Modellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Ein Key Performance Indicator (KPI) ist eine quantifizierbare Maßeinheit zur Geschäftserfolges Wirtschaft.  
  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]stellt ein KPI eine Auflistung von Berechnungen dar, die mit einer Measuregruppe in einem Cube verknüpft sind, die zur Auswertung der Geschäftserfolge verwendet werden. In der Regel sind diese Berechnungen eine Kombination aus MDX-Ausdrücken (Multidimensional Expressions) und berechneten Elementen. KPIs enthalten außerdem Metadaten, aus denen hervorgeht, wie Clientanwendungen die Berechnungsergebnisse des KPIs anzeigen sollen.  
  
 Ein KPI verarbeitet Informationen über eine Auflistung von Zielen, die im Cube aufgezeichnete eigentliche Leistungsformel sowie Messungen, um den Leistungstrend und -status anzuzeigen. AMO wird verwendet, um die Formeln und andere Definitionen über die Werte eines KPIs zu definieren. Von der Clientanwendung wird eine Abfrageschnittstelle wie ADOMD.NET verwendet, um die KPI-Werte abzurufen und für die Endbenutzer bereitzustellen. Weitere Informationen finden Sie unter [Entwickeln mit ADOMD.NET](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
 Aus den grundlegenden Informationen, dem Ziel, dem erreichten Istwert, einem Statuswert, einem Trendwert und einem Ordner, in dem der KPI angezeigt wird, wird ein einfaches <xref:Microsoft.AnalysisServices.Kpi> -Objekt erstellt. Zu den grundlegenden Informationen gehören der Name und die Beschreibung des KPIs. Das Ziel ist ein MDX-Ausdruck, der eine Zahl ergibt. Der Istwert ist ein MDX-Ausdruck, der eine Zahl ergibt. Der Status- und Trendwert sind MDX-Ausdrücke, die eine Zahl ergeben. Der Ordner ist ein vorgeschlagener Speicherort, in dem der KPI für den Client dargestellt wird.  
  
 Key Performance Indicator (KPI) ist ein Begriff aus der Wirtschaft, der eine quantifizierbare Maßeinheit zur Ermittlung des Geschäftserfolges darstellt. KPIs werden im Lauf der Zeit häufig ausgewertet. So verwendet z. B. die Vertriebsabteilung eines Unternehmens den monatlichen Bruttogewinn als KPI, während die Personalabteilung desselben Unternehmens den vierteljährlichen Umsatz pro Mitarbeiter als KPI verwendet. Beides sind Beispiele für KPIs. Um eine schnelle und genaue Verlaufsübersicht ihrer Geschäftserfolge zu erhalten, greifen Führungskräfte oft auf KPIs zurück, die in geschäftlichen Kennzahlensystemen gruppiert werden.  
  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]stellt ein KPI eine Auflistung von Berechnungen dar, die mit einer Measuregruppe in einem Cube verknüpft sind, die zur Auswertung der Geschäftserfolge verwendet werden. In der Regel sind diese Berechnungen eine Kombination aus MDX-Ausdrücken (Multidimensional Expressions) und berechneten Elementen. KPIs enthalten außerdem Metadaten, aus denen hervorgeht, wie Clientanwendungen die Berechnungsergebnisse eines KPI anzeigen sollen.  
  
 Zu den wichtigsten Vorteilen von KPIs in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zählt, dass sie serverbasiert sind und von verschiedenen Clientanwendungen verwendet werden können. Serverbasierte KPIs stellen eine einzelne Version im Gegensatz zu separaten Versionen in separaten Clientanwendungen dar. Die Durchführung der manchmal komplexen Berechnungen auf dem Server statt auf jedem Clientcomputer kann Leistungsvorteile bieten.  
  
## <a name="common-kpi-terms"></a>Häufig verwendete KPI-Begriffe  
 In der folgenden Tabelle werden die Definitionen für häufig verwendete KPI-Begriffe in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]bereitgestellt.  
  
|Begriff|Definition|  
|----------|----------------|  
|Ziel|Ein numerischer MDX-Ausdruck oder eine Berechnung, der bzw. die den Zielwert des KPI zurückgibt.|  
|Wert|Ein numerischer MDX-Ausdruck, der den Ist-Wert des KPI zurückgibt.|  
|Status|Ein MDX-Ausdruck, der den Status des KPI zu einem bestimmten Zeitpunkt darstellt.<br /><br /> Der MDX-Ausdruck "Status" sollte einen normalisierter Wert zwischen -1 und 1 zurückgeben. Werte, die kleiner oder gleich -1 sind, werden als "ungültig" oder "niedrig" interpretiert. Ein Wert von null (0) wird als "akzeptabel" oder "mittelmäßig" interpretiert. Werte, die größer oder gleich 1 sind, werden als "gut" oder "hoch" interpretiert.<br /><br /> Optional kann eine unbegrenzte Anzahl mit Zwischenwerten zurückgegeben werden, die zum Anzeigen einer beliebigen Anzahl zusätzlicher Status verwendet wird, wenn es die Clientanwendung unterstützt.|  
|Trend|Ein MDX-Ausdruck, der den Wert des KPI im Lauf der Zeit auswertet. Der Trend kann ein beliebiges zeitbasiertes Kriterium sein, das in bestimmten geschäftlichen Zusammenhängen nützlich ist.<br /><br /> Der Trend-MDX-Ausdruck versetzt einen Anwender des Produkts im geschäftlichen Bereich in die Lage, zu ermitteln, ob sich ein KPI im Lauf der Zeit verbessert oder verschlechtert.|  
|Statusindikator|Ein visuelles Element, das einen schnellen Überblick über den Status eines KPI gibt. Die Anzeige des Elements wird durch den Wert des MDX-Ausdrucks bestimmt, der den Status auswertet.|  
|Trendindikator|Ein visuelles Element, das einen schnellen Überblick über den Trend eines KPI gibt. Die Anzeige des Elements wird durch den Wert des MDX-Ausdrucks bestimmt, der den Trend auswertet.|  
|Anzeigeordner|Der Ordner, in dem der KPI für den Benutzer angezeigt wird, wenn er den Cube durchsucht.|  
|Übergeordneter KPI|Ein Verweis auf einen vorhandenen KPI, der den Wert des untergeordneten KPI zur Berechnung des übergeordneten KPI verwendet. Manchmal ist ein einzelner KPI eine Berechnung, die aus den Werten für andere KPIs besteht. Diese Eigenschaft erleichtert das richtige Anzeigen der untergeordneten KPIs unterhalb des übergeordneten KPI in Clientanwendungen.|  
|Aktuelles Zeitelement|Ein MDX-Ausdruck, der das Element zurückgibt, das den zeitlichen Kontext des KPI identifiziert.|  
|Weight|Ein numerischer MDX-Ausdruck, der einem KPI eine relative Bedeutung zuweist. Wenn der KPI einem übergeordneten KPI zugewiesen ist, wird die Gewichtung beim Berechnen des Werts des übergeordneten KPI zum proportionalen Anpassen der Ergebnisse des untergeordneten KPI-Werts verwendet.|  
  
## <a name="parent-kpis"></a>Übergeordnete KPIs  
 Ein Unternehmen kann verschiedene Unternehmensmaßsysteme auf unterschiedlichen Ebenen nachverfolgen. So kann z. B. mit nur zwei oder drei KPIs der Geschäftserfolg für das gesamte Unternehmen bestimmt werden, während diese unternehmensweiten KPIs auf drei oder vier anderen KPIs basieren können, die von den Geschäftsbereichen im gesamten Unternehmen nachverfolgt werden. Außerdem können die Geschäftsbereiche in einem Unternehmen unterschiedliche Statistiken zum Berechnen desselben KPI verwenden, dessen Ergebnisse in den unternehmensweiten KPI umgewandelt werden.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lässt Sie eine Über-/Unterordnungsbeziehung zwischen KPIs definieren. Durch diese Über-/Unterordnungsbeziehung können die Ergebnisse des untergeordneten KPI zum Berechnen des übergeordneten KPI verwendet werden. Clientanwendungen können diese Beziehung auch verwenden, um übergeordnete und untergeordnete KPIs entsprechend anzuzeigen.  
  
## <a name="weights"></a>Gewichtungen  
 Gewichtungen können außerdem untergeordneten KPIs zugeordnet werden. Gewichtungen ermöglichen es [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , beim Berechnen des Werts des übergeordneten KPI die Ergebnisse des untergeordneten KPI proportional anzupassen.  
  
## <a name="retrieving-and-displaying-kpis"></a>Abrufen und Anzeigen von KPIs  
 Die Anzeige von KPIs richtet sich nach der Implementierung der Clientanwendung. Beispielsweise demonstriert das Auswählen von **Browseransicht** auf der Symbolleiste der **KPIs** -Registerkarte des Cube-Designers eine mögliche Clientimplementierung. Dazu gehören die Grafiken, die zum Anzeigen der Status- und Trendindikatoren verwendet werden, die Anzeigeordner, die zum Gruppieren der KPIs verwendet werden, sowie die unter den übergeordneten KPIs angezeigten untergeordneten KPIs.  
  
 MDX-Funktionen können zum Abrufen einzelner Abschnitte (z. B. des Werts oder des Ziels) des KPI sowie in MDX-Ausdrücken, -Anweisungen und -Skripts verwendet werden.  
  
  
