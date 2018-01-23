---
title: "Analysis Services-Dokumentation für Entwickler | Microsoft Docs"
ms.custom: 
ms.date: 03/24/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- multidimensional data [Analysis Services], developer's guide
- developer's guide [Analysis Services - multidimensional data]
ms.assetid: 0a6eda76-1c5e-487e-9c8b-1feb09f1a34c
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 69f16ef4141ca467063a84bf2305ccbe6d8f8996
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2018
---
# <a name="analysis-services-developer-documentation"></a>Entwicklerhandbuch (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

In Analysis Services fast jedes Objekt und die Arbeitslast programmierbaren und häufig mehr als ein Ansatz zur Auswahl vorhanden ist.  Optionen umfassen das Schreiben von verwaltetem Code, Skript oder einen offenen Standards wie XMLA und MSOLAP verwenden, wenn Ihre Lösung nicht infrage mithilfe von .NET Framework.

## <a name="what-you-can-accomplish-in-code"></a>Was können Sie im Code erreichen.
Typische Programmierszenarien enthalten Server und die Bereitstellung, Verwaltung, Modell und Datenbankerstellung und Datenzugriff von benutzerdefinierten Anwendungen und Berichte, die Analysis Services-Daten nutzen. In all diesen Szenarien ist eine feste Architektur und Objekt Definition Hierarchie, mit klar verständlichen Vorgängen, die Datendefinition, Verarbeitung und abfragearbeitsauslastungen erstrecken.

Obwohl Objekte und Arbeitslasten programmierbaren sind, sind sie nicht erweiterbar. Insbesondere benutzerdefinierte Daten von Bändern, die Abrufen von Daten aus nicht unterstützten Datenquellen, anpassen oder ersetzen Formel oder Storage Engine kann nicht erstellt werden, noch können Sie neue Typen von Objektmetadaten auf einem Server, eine Datenbank oder ein Modell erstellen.

Weitere Details auf dem letzten Punkt zum Erstellen von neuen Objekttypen: während Sie eine neue Art von Objekt erstellen können, können Sie erstellen, berechnete Objekte, die von Ausdrücken oder Code zur Laufzeit erstellt. Nicht alle Elemente in Ihrem Modell muss vordefiniert und eine vorhandene Datenstruktur zugeordnet werden. Darüber hinaus können Sie das Schema mit Anmerkungen in AMO Übergabe von objektspezifischen Informationen zu Ihrer Clientanwendung erweitern.

## <a name="choose-a-platform-or-approach-to-development"></a>Wählen Sie eine Plattform oder der Vorgehensweise bei der Entwicklung
Analysis Services bietet viele Methoden zum Anpassen einer Lösung mithilfe von Code, aber die meisten Entwickler verwenden die verwalteten APIs oder das Skript.

- Verwaltete APIs enthalten [AMO und TOM](http://msdn.microsoft.com/library/mt436122.aspx) für Datendefinitions- und administrative Tasks und [ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) für die Unterstützung von Abfragen im Clientcode. In SQL Server 2016 ist AMO aktualisiert, um die neuen tabellarischen Metadaten für Modelle erstellt oder ein Upgrade auf Kompatibilitätsgrad 1200 oder höher verwenden.

- Skripts kann häufig die gleichen Ergebnisse wie eine ausführbare Programmdatei, möglicherweise weniger Arbeit erreichen.

  - Sie können PowerShell-Skript mithilfe von Analysis Services PowerShell-Komponenten, die AMO-Typen direkt aufrufen schreiben. In PowerShell verwenden können Sie auch erstellen und ASSL/XMLA oder TMSL (im JSON-Format)-Skript ausführen.

  - ASSL und TMSL sind Skriptsprachen, die angeben, dass Objekte in verwendet ermitteln und -Vorgänge ausführen. Welche Art von Skript, die Sie verwenden, hängt davon ab der zugrunde liegenden Server-, Datenbank- oder Modell.

  - Tabellarische Modelle oder Datenbanken mit Kompatibilitätsgrad 1200 oder höher verwenden, die tabellarische Tabular Model Scripting Language (TMSL), die im JSON-Format ist.

  - Verwenden Analysis Services Scripting Language (ASSL), also die Analysis Services-Erweiterung der offene Standard XMLA, mehrdimensionale und tabellarische Modelle Kompatibilitätsgrade 1050-1103.

  - Sie können ASSL oder TMSL-Skripts in Management Studio generieren. Sie können auch **Code anzeigen** in SQL Server Data Tools, um die Modelldefinition in ASSL oder TMSL anzuzeigen.

- Obwohl es möglich, eine Lösung basierend auf den offenen Standards von XMLA oder MDX zu erstellen ist, ist es sehr selten dazu. Es ist keine Dokumentation als XMLA und MDX-Verweis um, und die meisten Community und support-Forum zu zeichnet von Erfahrungen mit .NET oder systemeigenen (MSOLAP)-Technologien.

## <a name="programming-in-analysis-services"></a>In Analysis Services-Programmierung
[Programmieren von Data Mining](../analysis-services/data-mining-programming.md) beschreibt die Herangehensweisen, die zum Erstellen von Lösungen, die Datamining-Objekte enthalten.

[Mehrdimensionale Programmiermodell](../analysis-services/multidimensional-models/multidimensional-model-programming.md) beschreibt die Entwicklungsaufgaben und Herangehensweisen zum Integrieren mehrdimensionaler Modellobjekte in eine benutzerdefinierte Lösung.

[Tabellarische Programmiermodell für die Kompatibilität auf 1200 und höher](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**neu in SQL Server 2016**.  Fasst die Schnittstellen und Sprachen für Installationsskripts für die Arbeit mit tabellarischen 1200 und höher Modelle programmgesteuert verwendet.

[Tabellarische Programmiermodell für Kompatibilität Ebenen 1050 bis 1103](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md) diese Dokumentation ist für Entwickler, die tabellarische Modelle mit niedrigeren Kompatibilitätsgraden unterstützen vorgesehen. Es beschreibt die CSDL-Erweiterungen, die ein tabellarisches Modell im XML-Syntax zu definieren. Darüber hinaus Informationen zur Syntax und tabellarischen Modell Objektdefinitionen.

[Analysis Services Management Objects (AMO)](https://msdn.microsoft.com/library/mt436122.aspx) Referenzdokumentation für Entwickler für den verwalteten Datenanbieter, Analysis Services Management Objects (AMO) für Datendefinitions- und Verwaltung, einschließlich der Verarbeitung durch.

[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) Referenzdokumentation für Entwickler für den verwalteten Anbieter ADOMD.NET für den programmgesteuerten Daten Zugriff als auch das abfragearbeitsauslastungen verwendet.

[Analysis Services-Schemarowsets](../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md) beschreibt die Schemarowsets, die Informationen zu Serverstatus, Servervorgängen und Datenbankobjekten liefern.

[XML for Analysis &#40; XMLA &#41; Verweis](../analysis-services/xmla/xml-for-analysis-xmla-reference.md) beschreibt XMLA-Konzepte, die Ihnen helfen zu verstehen, wie XMLA zu Ihrer benutzerdefinierten Projektmappe beitragen. Darüber hinaus wird der Grad der Kompatibilität mit der XMLA 1.1-Spezifikation beschrieben.

[Analysis Services Scripting Language &#40; ASSL XMLA &#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md) Beschreibt die ASSL-Erweiterungen für XMLA. ASSL stellt eine Datendefinitions- und Datenbearbeitungssprache für mehrdimensionale Analysis Services-Modelle bereit und ist eine Ergänzung der XMLA-Spezifikation.

[Tabular Model Scripting Language &#40; TMSL &#41; Verweis](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) TMSL ist ein JSON-Darstellung des tabellarischen Modelle mit Kompatibilitätsgrad 1200 oder höher. Objektdefinitionen basieren auf tabellarischen Metadaten-Konstrukte, wie Tabelle, Spalte und Beziehung anstatt mehrdimensionale Metadaten, die möglicherweise nicht vertraut, wenn Sie im tabellarischen Modus mit Analysis Services-Daten modellieren vertraut sind.

[Referenz zu Analysis Services PowerShell](../analysis-services/powershell/analysis-services-powershell-reference.md) dokumentiert den-Cmdlets für administrative Funktionen sowie die allgemeine verwendet **Invoke-ASCmd** -Cmdlet, das Skripts oder einer Abfrage als Eingabe akzeptiert.

## <a name="see-also"></a>Siehe auch
[Technische Referenz &#40; SSAS &#41; ](../analysis-services/powershell/technical-reference-ssas.md) 
 [Abfrage- und Expression-Sprachreferenz &#40; Analysis Services &#41;](http://msdn.microsoft.com/library/gg492188.aspx)
