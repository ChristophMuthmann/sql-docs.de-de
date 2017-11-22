---
title: "KPIs (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0524602-5239-45a7-8c44-2477302a3637
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9c3c91a755b50ffc1dc51d305589f17322584854
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="kpis"></a>KPIs (Key Performance Indicators)
  Ein *KPI* (Key Performance Indicator) wird in einem Tabellenmodell verwendet, um die Leistung eines durch ein *Basismeasure* definierten Werts im Vergleich zu einem *Zielwert* zu messen, der ebenfalls durch ein Measure oder einen absoluten Wert definiert wird. Dieses Thema bietet Entwicklern von tabellarischen Modellen einen grundlegenden Überblick der in einem Tabellenmodell verwendeten KPIs.  
  
##  <a name="bkmk_benefits"></a> Vorteile  
 Key Performance Indicator (KPI) ist ein Begriff aus der Wirtschaft, der eine quantifizierbare Maßeinheit zur Messung der Umsetzung von Geschäftszielen darstellt. KPIs werden im Lauf der Zeit häufig ausgewertet. Die Vertriebsabteilung eines Unternehmens könnte KPIs beispielsweise verwenden, um den monatlichen Bruttogewinn mit dem vorausgesagten Bruttogewinn zu vergleichen. Die Buchhaltung könnte die monatlichen Ausgaben und Einnahmen gegenüberstellen, um eine Kostenauswertung vorzunehmen, und die Personalabteilung könnte den Quartalsumsatz pro Mitarbeiter ermitteln. Beides sind Beispiele für KPIs. Um eine schnelle und genaue Verlaufsübersicht ihrer Geschäftserfolge zu erhalten und Trends zu erkennen, greifen Fachanwender oft auf KPIs zurück, die in geschäftlichen Kennzahlensystemen gruppiert werden.  
  
 Ein KPI in einem Tabellenmodell enthält:  
  
 **Basiswert**  
 Ein Basiswert wird durch ein Measure definiert, das zu einem Wert aufgelöst wird. Dieser Wert, kann z. B. ein Aggregat tatsächlicher Umsatzzahlen oder ein berechnetes Measure wie der Ertrag für einen bestimmten Zeitraum sein.  
  
 **Zielwert**  
 Ein Zielwert wird entweder durch ein Measure definiert, das zu einem Wert aufgelöst wird, oder durch einen absoluten Wert. Ein Zielwert könnte beispielsweise der Betrag sein, um den die Führungskräfte einer Organisation die Verkaufszahlen oder Gewinne steigern möchten.  
  
 **Statusschwellenwerte**  
 Ein Statusschwellenwert wird durch den Bereich zwischen einem niedrigen und hohen Schwellenwert oder durch einen festen Wert definiert. Der Statusschwellenwert wird anhand einer Grafik dargestellt, damit Benutzer problemlos den Status des Basiswerts im Vergleich zum Zielwert ermitteln können.  
  
##  <a name="bkmk_example"></a> Beispiel  
 Der Vertriebsleiter von Adventure Works möchte eine PivotTable erstellen, in der schnell angezeigt wird, ob Vertriebsmitarbeiter ihre Umsatzvorgaben in einem bestimmten Zeitraum (Jahr) erfüllen. Für jeden Vertriebsmitarbeiter sollen in der PivotTable die tatsächlichen Verkaufszahlen (in Dollar), die Umsatzvorgabe (in Dollar) und eine einfache Statusgrafik angezeigt werden, die Aufschluss darüber gibt, ob der Vertriebsmitarbeiter unter oder über dieser Vorgabe liegt bzw. diese genau erfüllt. Zudem möchte der Vertriebsleiter die Daten nach Jahr unterteilen.  
  
 Mit Unterstützung eines Kollegen, der für die Entwicklung von BI-Lösungen zuständig ist, fügt der Vertriebsleiter dem tabellarischen AdventureWorks-Modell einen "Sales KPI" hinzu. Der Vertriebsleiter verwendet dann Excel eine Verbindung mit dem tabellarischen Adventure Works-Modell als Datenquelle, und erstellen Sie eine PivotTable mit den Feldern (Measures und KPI) und Slicern, um zu analysieren, und zwar unabhängig davon, ob die Vertriebsmannschaft ihre Vorgaben erfüllt.  
  
 Im Modell wird ein Measure für die Spalte "SalesAmount" in der Tabelle "FactResellerSales" erstellt, das die tatsächlichen Vertriebszahlen für jeden Vertriebsmitarbeiter in Dollar angibt. Durch dieses Measure wird der Basiswert des KPIs definiert.  
  
 Das Sales-Measure wird anhand der folgenden Formel erstellt:  
  
```  
Sales:=Sum(FactResellerSales[SalesAmount])  
```  
  
 In der Spalte "SalesAmountQuota" der Tabelle "FactSalesQuota" sind die Umsatzvorgaben für jeden Mitarbeiter definiert. Die Werte in dieser Spalte dienen als Zielmeasure (Wert) im KPI.  
  
 Das Measure "SalesAmountQuota" wird anhand der folgenden Formel erstellt:  
  
```  
Target SalesAmountQuota:=Sum(FactSalesQuota[SalesAmountQuota])  
```  
  
> [!NOTE]  
>  Es besteht eine Beziehung zwischen der Spalte "EmployeeKey" in der Tabelle "FactSalesQuota" und der Spalte "EmployeeKey" in der Tabelle "DimEmployees". Diese Beziehung ist erforderlich, damit jeder Vertriebsmitarbeiter aus der Tabelle "DimEmployee" in der Tabelle "FactSalesQuota" dargestellt werden kann.  
  
 Nachdem die Measures nun erstellt wurden, um als Basis- und Zielwert des KPIs zu fungieren, wird das Sales-Measure zu einem neuen Sales-KPI erweitert. Im "Sales KPI" ist das Measure "Target SalesAmountQuota" als Zielwert definiert. Der Statusschwellenwert wird als Bereich von Prozentzahlen definiert, wobei 100 % der Zielvorgabe entsprechen. Das würde bedeuten, dass die durch das Sales-Measure definierten tatsächlichen Verkaufszahlen die Vorgaben erfüllen, die im Measure "Target SalesAmountQuota" definiert sind. Zum Definieren der niedrigen und hohen Prozentwerte wird die Statusleiste verwendet, und es wird ein Grafiktyp ausgewählt.  
  
 Der Vertriebsleiter kann jetzt eine PivotTable erstellen, indem er den Basiswert, Zielwert und den Status des KPIs dem Feld Werte hinzufügt. Die Spalte "Employees" wird dem Feld "RowLabel" hinzugefügt, und die Spalte "CalendarYear" wird als Slicer verwendet.  
  
 Der Vertriebsleiter kann die tatsächlichen Umsatzzahlen, die Vertriebsvorgaben und den Status jedes Vertriebsmitarbeiters jetzt nach Jahr unterteilen. So lassen sich Vertriebstrends über Jahre analysieren, um zu ermitteln, ob die Vertriebsvorgaben für einen Vertriebsmitarbeiter angepasst werden müssen.  
  
##  <a name="bkmk_create"></a> Create and edit KPIs  
 Zum Erstellen von KPIs im Modell-Designer verwenden Sie das Dialogfeld Key Performance Indicator. Da KPIs einem Measure zugeordnet werden müssen, erstellen Sie einen KPI, indem Sie ein Measure erweitern, das einen Basiswert ergibt, und dann entweder ein Measure erstellen, das einen Zielwert ergibt, oder einen absoluten Wert eingeben. Nachdem Basismeasure (Wert) und Zielwert definiert wurden, können Sie die Parameter für den Statusschwellenwert zwischen dem Basis- und Zielwert definieren. Der Status wird in einem grafischen Format mit auswählbaren Symbolen, Balken, Diagrammen oder Farben angezeigt. Anschließend können Basiswert, Zielwert und Status einem Bericht oder einer PivotTable als Werte hinzugefügt werden, die für andere Datenfelder in Slices aufgeteilt werden können.  
  
 Um das Dialogfeld **Key Performance Indicator**im Measureraster für eine Tabelle anzuzeigen, klicken Sie mit der rechten Maustaste auf ein Measure, das als Basiswert dient, und klicken Sie dann auf KPI erstellen. Nachdem ein Measure als Basiswert zu einem KPI erweitert wurde, wird im Measureraster neben dem Measurenamen ein Symbol angezeigt, das angibt, dass das Measure einem KPI zugeordnet ist.  
  
##  <a name="bkmk_related_tasks"></a> Verwandte Aufgaben  
  
|Thema|Description|  
|-----------|-----------------|  
|[Erstellen und Verwalten von KPIs](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)|Beschreibt das Erstellen eines KPIs mit einem Basismeasure, einem Zielmeasure und Statusschwellenwerten.|  
  
## <a name="see-also"></a>Siehe auch  
 [Measures](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Perspektiven](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)  
  
  
