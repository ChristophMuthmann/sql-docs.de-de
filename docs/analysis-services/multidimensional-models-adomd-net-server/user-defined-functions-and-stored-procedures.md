---
title: Benutzerdefinierte Funktionen und gespeicherten Prozeduren | Microsoft Docs
ms.custom: 
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
- stored procedures [ADOMD.NET]
- ADOMD.NET, user defined functions
- user defined functions [ADOMD.NET]
- ADOMD.NET, UDFs
- ADOMD.NET, stored procedures
ms.assetid: 07e8aa47-37d4-4bbc-8bff-49e422d12897
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 1c49bb0f4994883f7bee1accf8c6d983b31b657f
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="user-defined-functions-and-stored-procedures"></a>Benutzerdefinierte Funktionen und gespeicherte Prozeduren
  Mit ADOMD.NET-Serverobjekten können Sie erstellen eine benutzerdefinierte Funktion (UDF) oder gespeicherte Prozeduren für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , die Metadaten und Daten vom Server interagieren. Diese prozessinternen Methoden werden durch Multidimensional Expressions (MDX)- oder Data Mining Extensions (DMX)-Anweisungen aufgerufen, um zusätzliche Funktionen bereitzustellen, die nicht den Wartezeiten eines Netzwerks unterworfen sind.  
  
## <a name="udf-examples"></a>UDF-Beispiele  
 Eine benutzerdefinierte Funktion (UDF) ist eine Methode, die im Zusammenhang mit einer MDX- oder DMX-Anweisung aufgerufen wird, eine beliebige Anzahl an Parametern unterstützt und jede Art von Daten zurückgeben kann.  
  
 Eine mit MDX erstellte benutzerdefinierte Funktion ist mit einer für DMX erstellten vergleichbar. Der Hauptunterschied besteht darin, dass bestimmte Eigenschaften des <xref:Microsoft.AnalysisServices.AdomdServer.Context>-Objekts, wie zum Beispiel die Eigenschaften <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentCube%2A> und <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentMiningModel%2A>, nur für die eine oder die andere Skriptsprache verfügbar sind.  
  
 Die folgenden Beispiele zeigen, wie man mit einer benutzerdefinierten Funktion eine Knotenbeschreibung zurückgibt, Tupeln filtert und einen Filter auf ein Tupel anwendet.  
  
### <a name="returning-a-node-description"></a>Zurückgeben einer Knotenbeschreibung  
 Im folgenden Beispiel wird eine benutzerdefinierte Funktion erstellt, mit der die Knotenbeschreibung für einen bestimmten Knoten zurückgegeben wird. Die benutzerdefinierte Funktion verwendet den derzeitigen Kontext, in dem sie ausgeführt wird, und ruft den Knoten mithilfe einer DMX FROM-Klausel aus dem aktuellen Miningmodell ab.  
  
```  
public string GetNodeDescription(string nodeUniqueName)  
{  
   return Context.CurrentMiningModel.GetNodeFromUniqueName(nodeUniqueName).Description;  
}  
```  
  
 Nach der Bereitstellung kann das vorherige UDF-Beispiel durch folgenden DMX-Ausdruck, der den wahrscheinlichsten Vorhersageknoten abruft, aufgerufen werden. Die Beschreibung enthält Informationen, in denen die Bedingungen beschrieben werden, die den Vorhersageknoten bilden.  
  
```  
select Cluster(), SampleAssembly.GetNodeDescription( PredictNodeId(Cluster()) ) FROM [Customer Clusters]  
```  
  
### <a name="returning-tuples"></a>Zurückgeben von Tupeln  
 Im folgenden Beispiel werden mit einem Satz und einer Rückgabezahl Tupeln nach dem Zufallsprinzip aus dem Satz abgerufen, wodurch schließlich eine Teilmenge zurückgegeben wird:  
  
```  
public Set RandomSample(Set set, int returnCount)  
{  
   //Return the original set if there are fewer tuples  
   //in the set than the number requested.  
   if (set.Tuples.Count <= returnCount)  
      return set;  
  
   System.Random r = new System.Random();  
   SetBuilder returnSet = new SetBuilder();  
  
   //Retrieve random tuples until the return set is filled.  
   int i = set.Tuples.Count;  
   foreach (Tuple t in set.Tuples)  
   {  
      if (r.Next(i) < returnCount)  
      {  
         returnCount--;  
         returnSet.Add(t);  
      }  
      i--;  
      //Stop the loop if we have enough tuples.  
      if (returnCount == 0)  
         break;  
   }  
   return returnSet.ToSet();  
}  
```  
  
 Das vorherige Beispiel wird in folgendem MDX-Beispiel aufgerufen. In diesem Beispiel MDX fünf zufällige Bundesstaaten oder Provinzen aus abgerufen werden die **Adventure Works** Datenbank.  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
### <a name="applying-a-filter-to-a-tuple"></a>Anwenden eines Filters auf ein Tupel  
 In folgendem Beispiel wird eine benutzerdefinierte Funktion definiert, mit der in einem Satz unter Verwendung des Expression-Objekts ein Filter auf jedes Tupel in dem Satz angewendet wird. Alle Tupel, die dem Filter entsprechen, werden einem zurückgegebenen Satz hinzugefügt.  
  
 [!code-cs[Adomd.NetServer#FilterSet](../../analysis-services/multidimensional-models-adomd-net-server/codesnippet/csharp/user-defined-functions-a_1.cs)]  
  
 Das vorangegangene Beispiel wird in folgendem MDX-Beispiel aufgerufen, bei dem der Satz auf mit 'A' beginnende Städte gefiltert wird.  
  
```  
Select Measures.Members on Rows,  
SampleAssembly.FilterSet([Customer].[Customer Geography].[City], "[Customer].[Customer Geography].[City].CurrentMember.Name < 'B'") on Columns  
From [Adventure Works]  
```  
  
## <a name="stored-procedure-example"></a>Beispiel für gespeicherte Prozeduren  
 In folgendem Beispiel verwendet eine MDX-basierte, gespeicherte Prozedur AMO, um bei Bedarf Partitionen für Internet Sales zu erstellen.  
  
 [!code-cs[Adomd.NetServer#CreateInternetSalesMeasureGroupPartitions](../../analysis-services/multidimensional-models-adomd-net-server/codesnippet/csharp/user-defined-functions-a_2.cs)]  
  
  

