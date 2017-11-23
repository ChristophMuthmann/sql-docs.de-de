---
title: "Unregelmäßige Hierarchien | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ragged hierarchies [Analysis Services]
ms.assetid: e40a5788-7ede-4b0f-93ab-46ca33d0cace
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: df06dbfc368310427d1359f78de557c910b94af9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="user-defined-hierarchies---ragged-hierarchies"></a>Benutzerdefinierte Hierarchien - unregelmäßige Hierarchien
  Eine unregelmäßige Hierarchie ist eine benutzerdefinierte Hierarchie, die über eine ungerade Anzahl von Ebenen verfügt. Typische Beispiele dafür sind ein Organigramm, bei dem einer hochrangigen Führungskraft sowohl Abteilungsleiter als auch Nicht-Abteilungsleiter unterstellt sind, oder geografische Hierarchien aus Ländern, Regionen und Städten, bei denen einige Städte keinen übergeordneten Bundesstaat bzw. keine übergeordnete Provinz aufweisen, z. B. Washington D. C., Vatikanstadt oder Neu-Delhi.  
  
 Bei den meisten Hierarchien in einer Dimension besitzt jede Ebene dieselbe Anzahl von übergeordneten Elementen wie jedes andere Element auf derselben Ebene. Eine unregelmäßige Hierarchie unterscheidet sich in der Hinsicht, dass sich das logisch übergeordnete Element mindestens eines Elements nicht auf der Ebene unmittelbar über dem betreffenden Element befindet. Ist dies der Fall, verzweigt die Hierarchie auf unterschiedliche Ebenen mit verschiedenen Drilldownpfaden. Daher können Drilldownpfade in einer Clientanwendung unnötig kompliziert werden.  
  
 Die Fähigkeit, unregelmäßige Hierarchien zu verarbeiten, ist bei Clientanwendungen unterschiedlich gut ausgeprägt. Wenn ein Modell unregelmäßige Hierarchien aufweist, bedarf es einiger zusätzlicher Schritte, um das erwartete Renderingverhalten zu erreichen.  
  
 Überprüfen Sie zunächst, auf welche Weise der Drilldownpfad von der Clientanwendung verwaltet wird. Beispielsweise wiederholt Excel die übergeordneten Namen als Platzhalter für fehlende Werte. Um dieses Verhalten zu reproduzieren, erstellen Sie im mehrdimensionalen Adventure Works-Modell mithilfe der Sales Territory-Dimension eine PivotTable. In einer PivotTable, die über die Sales Territory-Attribute Group, Country und Region verfügt, werden die Länder ohne einen Regionswert mit einem Platzhalter angezeigt. In diesem Fall sind dies die wiederholten (übergeordneten) Ländernamen. Dieses Verhalten wird von der Verbindungszeichenfolgen-Eigenschaft MDX Compatibility=1 abgeleitet, die innerhalb von Excel unveränderlich ist. Wenn das gewünschte Drilldownverhalten im Client nicht standardmäßig implementiert ist, können Sie Eigenschaften im Modell festlegen, um mindestens einige Verhaltensweisen zu ändern.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Methoden zum Ändern der Drilldownnavigation in einer unregelmäßigen Hierarchie](#bkmk_approach)  
  
-   [Festlegen von "HideMemberIf" zum Ausblenden von Elementen in einer regulären Hierarchie](#bkmk_Hide)  
  
-   [Festlegen der MDX-Kompatibilität, um zu bestimmen, wie Platzhalter in Clientanwendungen dargestellt werden](#bkmk_Mdx)  
  
##  <a name="bkmk_approach"></a> Methoden zum Ändern der Drilldownnavigation in einer unregelmäßigen Hierarchie  
 Eine unregelmäßige Hierarchie wird zu einem Problem, wenn die Drilldownnavigation unerwartete Werte zurückgibt oder als wenig benutzerfreundlich empfunden wird. Die folgenden Optionen stehen Ihnen zur Verfügung, um Navigationsprobleme aufgrund unregelmäßiger Hierarchien zu beheben:  
  
-   Verwenden Sie eine reguläre Hierarchie, wobei Sie jedoch für jede Ebene die **HideMemberIf** -Eigenschaft festlegen. Dadurch geben Sie an, ob eine fehlende Ebene für den Benutzer sichtbar gemacht wird. Wenn Sie **HideMemberIf**festlegen, sollten Sie auch **MDXCompatibility** für die Verbindungszeichenfolge festlegen, um das standardmäßige Navigationsverhalten zu überschreiben. Anweisungen zum Festlegen dieser Eigenschaften finden Sie in diesem Thema.  
  
-   Erstellen Sie eine Über-/Unterordnungshierarchie, von der die Ebenenelemente explizit verwaltet werden. Eine grafische Darstellung dieser Methode finden Sie im Blogbeitrag [Ragged Hierarchy in SSAS](http://dwbi1.wordpress.com/2011/03/30/ragged-hierarchy-in-ssas/)(Unregelmäßige SSAS-Hierarchie). Weitere Informationen finden Sie in der Onlinedokumentation unter [Über- und untergeordnete Dimensionen](../../analysis-services/multidimensional-models/parent-child-dimension.md). Die Erstellung einer Über-/Unterordnungshierarchie hat den Nachteil, dass Sie pro Dimension nur eine solche Hierarchie erstellen können. Darüber hinaus treten in der Regel Leistungsprobleme auf, wenn Sie Aggregationen für Zwischenelemente berechnen.  
  
 Wenn die Dimension mehr als eine unregelmäßige Hierarchie enthält, sollten Sie die erste Methode verwenden, also **HideMemberIf**festlegen. BI-Entwickler, die bereits praktische Erfahrungen mit unregelmäßigen Hierarchien gesammelt haben, würden sogar zusätzliche Änderungen in den physischen Datentabellen befürworten und getrennte Tabellen für jede Ebene erstellen. Ausführliche Informationen zu diesem Verfahren finden Sie im Blog von Martin Mason [Financial Cube–Part 1a–Ragged Hierarchies](http://martinmason.wordpress.com/2012/03/03/the-ssas-financial-cubepart-1aragged-hierarchies-cont/) (Finanzcube, Teil 1a, Unregelmäßige Hierarchien).  
  
##  <a name="bkmk_Hide"></a> Festlegen von "HideMemberIf" zum Ausblenden von Elementen in einer regulären Hierarchie  
 In der Tabelle einer unregelmäßigen Dimension können logisch fehlende Elemente auf verschiedene Weise dargestellt werden. Die Tabellenzellen können NULL-Werte oder leere Zeichenfolgen enthalten. Sie können jedoch auch denselben Wert wie das übergeordnete Objekt enthalten, der in diesem Fall als Platzhalter dient. Die Darstellung von Platzhaltern wird vom Platzhalterstatus der untergeordneten Elemente gemäß der **HideMemberIf** -Eigenschaft und der **MDX Compatibility** -Verbindungszeichenfolgen-Eigenschaft für die Clientanwendung festgelegt.  
  
 Bei Clientanwendungen, die die Anzeige unregelmäßiger Hierarchien unterstützen, können Sie diese Eigenschaften verwenden, um logisch fehlende Elemente auszublenden.  
  
1.  Doppelklicken Sie in SSDT auf eine Dimension, um sie im Dimensions-Designer zu öffnen. Auf der ersten Registerkarte Dimensionsstruktur werden die Attributhierarchien im Bereich Hierarchien angezeigt.  
  
2.  Klicken Sie mit der rechten Maustaste auf ein Element innerhalb der Hierarchie, und wählen Sie **Eigenschaften**aus. Legen Sie **HideMemberIf** auf einen der unten beschriebenen Werte fest.  
  
    |HideMemberIf-Einstellung|Description|  
    |--------------------------|-----------------|  
    |**Never**|Ebenenelemente werden nie ausgeblendet. Dies ist der Standardwert.|  
    |**OnlyChildWithNoName**|Ein Ebenenelement wird ausgeblendet, wenn es das einzige untergeordnete Element eines übergeordneten Elements und der Name NULL oder eine leere Zeichenfolge ist.|  
    |**OnlyChildWithParentName**|Ein Ebenenelement wird ausgeblendet, wenn es das einzige untergeordnete Element eines übergeordneten Elements ist und sein Name dem des übergeordneten Elements entspricht.|  
    |**NoName**|Ein Ebenenelement wird ausgeblendet, wenn sein Name leer ist.|  
    |**ParentName**|Ein Ebenenelement wird ausgeblendet, wenn sein Name dem seines übergeordneten Elements entspricht.|  
  
##  <a name="bkmk_Mdx"></a> Festlegen der MDX-Kompatibilität, um zu bestimmen, wie Platzhalter in Clientanwendungen dargestellt werden  
 Nachdem Sie **HideMemberIf** für eine Hierarchieebene festgelegt haben, sollten Sie auch die **MDX Compatibility** -Eigenschaft in der von der Clientanwendung gesendeten Verbindungszeichenfolge festlegen. Die **MDX Compatibility** -Einstellung bestimmt, ob **HideMemberIf** verwendet wird.  
  
|Einstellung für die MDX-Kompatibilität|Description|Verwendung|  
|-------------------------------|-----------------|-----------|  
|**1**|Zeigt einen Platzhalterwert an.|Dies ist der von Excel, SSDT und SSMS verwendete Standardwert. Er weist den Server an, beim Drilldown auf leere Ebenen einer unregelmäßigen Hierarchie Platzhalterwerte zurückzugeben. Wenn Sie auf den Platzhalterwert klicken, können Sie einen Drilldown bis auf die untergeordneten Knoten (des Blatts) ausführen.<br /><br /> Die Verbindungszeichenfolge zur Verbindung mit Analysis Services ist im Besitz von Excel, und **MDX Compatibility** wird bei jeder neuen Verbindung grundsätzlich auf 1 festgelegt. Bei diesem Verhalten wird die Abwärtskompatibilität beibehalten.|  
|**2**|Blendet einen Platzhalterwert (entweder ein NULL-Wert oder ein Duplikat der übergeordneten Ebene) aus, wobei andere Ebenen und Knoten mit relevanten Werten jedoch eingeblendet bleiben.|**MDX Compatibility**= 2 ist in der Regel die bevorzugte Einstellung für unregelmäßige Hierarchien. Diese Einstellung kann von einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht und einigen Clientanwendungen von Drittanbietern beibehalten werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von benutzerdefinierten Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)   
 [Benutzerhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Über-und untergeordneten Dimensionen](../../analysis-services/multidimensional-models/parent-child-dimension.md)   
 [Verbindungszeichenfolgen-Eigenschaften &#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)  
  
  
