---
title: Mit aktiviertem Schreibzugriff Partitionen | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], partitions
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], write-enabled
- partitions [Analysis Services], storage
- writeback [Analysis Services], partitions
- storing data [Analysis Services], partitions
ms.assetid: 46e7683f-03ce-4af2-bd99-a5203733d723
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 87ca933c004d59a8c2e680d79e9d9499700f7e43
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="partitions---write-enabled-partitions"></a>Partitionen - Partitionen mit aktiviertem Schreibzugriff
  Die Daten in einem Cube sind im Allgemeinen schreibgeschützt. In bestimmten Szenarien kann es jedoch erwünscht sein, den Schreibzugriff für eine Partition zu aktivieren. Partitionen mit aktiviertem Schreibzugriff werden verwendet, um Benutzern im geschäftlichen Bereich das Untersuchen von Szenarien zu ermöglichen, indem sie Zellenwerte ändern und die Auswirkungen der Änderungen auf die Cubedaten analysieren. Wenn Sie den Schreibzugriff für eine Partition aktivieren, können Clientanwendungen Änderungen an den Daten in der Partition aufzeichnen. Diese Änderungen, so genannte Rückschreibedaten, werden in einer separaten Tabelle gespeichert und überschreiben keine vorhandenen Daten in einer Measuregruppe. Sie werden jedoch als Teil der Cubedaten in Abfrageergebnisse einbezogen.  
  
 Sie können den Schreibzugriff für einen gesamten Cube oder nur für bestimmte Partitionen im Cube aktivieren. Dimensionen mit aktiviertem Schreibzugriff unterscheiden sich von diesen Partitionen, aber auf ergänzende Weise. Eine Partition mit aktiviertem Schreibzugriff ermöglicht den Benutzern das Update von Partitionszellen, während eine Dimension mit aktiviertem Schreibzugriff den Benutzern das Update von Dimensionselementen ermöglicht. Sie können diese zwei Funktionen auch zusammen verwenden. So muss ein Cube oder eine Partition mit aktiviertem Schreibzugriff keine Dimensionen mit aktiviertem Schreibzugriff enthalten. **Verwandtes Thema:**[Dimensionen mit aktiviertem Schreibzugriff](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
> [!NOTE]  
>  Wenn Sie den Schreibzugriff für einen Cube aktivieren möchten, der eine Microsoft Access-Datenbank als Datenquelle verwendet, sollten Sie in den Datenquellendefinitionen des Cubes, seinen Partitionen oder seinen Dimensionen nicht Microsoft OLE DB-Anbieter für ODBC-Treiber verwenden. Stattdessen können Sie Microsoft Jet 4.0 OLE DB-Anbieter oder eine beliebige Version des Jet Service Pack, die Jet 4.0 OLE beinhaltet, verwenden. Weitere Informationen finden Sie im Microsoft Knowledge Base-Artikel [so erhalten Sie das neueste Servicepack für Microsoft Jet 4.0-Datenbankmodul](http://support.microsoft.com/?kbid=239114).  
  
 Ein Cube kann der Schreibzugriff aktiviert werden nur, wenn alle zugehörigen Measures verwenden die **Summe** Aggregatfunktion. Für verknüpfte Measuregruppen und lokale Cubes kann der Schreibzugriff nicht aktiviert werden.  
  
## <a name="writeback-storage"></a>Rückschreibespeicher  
 Alle von einem Anwender des Produkts im geschäftlichen Bereich vorgenommenen Änderungen werden in der Rückschreibetabelle in Form der Abweichung vom aktuell angezeigten Wert gespeichert. Wenn ein Endbenutzer einen Zellwert von 90 auf 100 erhöht, den Wert ändert z. B. **+ 10** befindet sich in der Rückschreibetabelle, zusammen mit der Uhrzeit der Änderung und Informationen über die Geschäftsbenutzer, die sie vorgenommen hat. Für Clientanwendungen werden die reinen Auswirkungen der gesammelten Änderungen angezeigt. Der ursprüngliche Wert im Cube bleibt erhalten, und in der Rückschreibetabelle wird eine Überwachungsliste der Änderungen aufgezeichnet.  
  
 Änderungen an Blatt- und Nichtblattzellen werden unterschiedlich gehandhabt. Eine Blattzelle stellt eine Schnittstelle zwischen einem Measure und einem Blattelement aus den einzelnen Dimensionen dar, auf die durch die Measuregruppe verwiesen wird. Der Wert einer Blattzelle wird direkt der Faktentabelle entnommen und kann nicht weiter durch einen Drilldown aufgeteilt werden. Wenn für einen Cube oder eine Partition der Schreibzugriff aktiviert wurde, können an einer Blattzelle Änderungen vorgenommen werden. Änderungen an Nichtblattzellen sind nur dann möglich, wenn die Clientanwendung einen Mechanismus bereitstellt, um die Änderungen an die Blattzellen zu verteilen, aus denen sich die Nichtblattzelle zusammensetzt. Dieser so genannte Zuordnungsprozess wird durch die UPDATE CUBE-Anweisung in MDX (Multidimensional Expressions) verwaltet. Business Intelligence-Entwickler können mithilfe der UPDATE CUBE-Anweisung Zuordnungsfunktionen integrieren. Weitere Informationen finden Sie unter [UPDATE CUBE-Anweisung &#40; MDX &#41; ](../../mdx/mdx-data-manipulation-update-cube.md).  
  
> [!IMPORTANT]  
>  Wenn sich die aktualisierten Zellen nicht überlagern, kann mithilfe der **Update Isolation Level** -Eigenschaft der Verbindungszeichenfolge das Leistungsverhalten in Bezug auf UPDATE CUBE verbessert werden. Weitere Informationen finden Sie unter <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.  
  
 Unabhängig davon, ob eine Clientanwendung Änderungen verteilt, die an Nichtblattzellen vorgenommen werden, werden bei jeder Auswertung von Abfragen Änderungen in der Rückschreibetabelle sowohl auf Nichtblatt- als auch auf Blattzellwerte angewendet, sodass Anwender des Produkts im geschäftlichen Bereich die Auswirkungen der Änderungen für den gesamten Cube erkennen können.  
  
 Änderungen, die von Anwendern des Produkts im geschäftlichen Bereich vorgenommen wurden, werden in einer getrennten Rückschreibetabelle aufgezeichnet, mit der Sie wie folgt arbeiten können:  
  
-   Konvertieren einer Partition, um Änderungen dauerhaft in den Cube einzubinden. Durch diese Aktion wird der Schreibzugriff für die Measuregruppe deaktiviert. Sie können einen Filterausdruck angeben, um die Änderungen auszuwählen, die Sie konvertieren möchten.  
  
-   Verwerfen der Änderung, um die Partition in ihrem ursprünglichen Status wiederherzustellen. Durch diesen Vorgang wird der Schreibzugriff für die Partition deaktiviert.  
  
## <a name="security"></a>Sicherheit  
 Ein Anwender des Produkts im geschäftlichen Bereich darf nur dann Änderungen in der Rückschreibetabelle eines Cubes aufzeichnen, wenn er einer Rolle angehört, die über Lese-/Schreibberechtigung für die Zellen des Cubes verfügt. Sie können für jede Rolle steuern, welche Cubezellen aktualisiert werden können. Weitere Informationen finden Sie unter [gewähren, Cube oder modellberechtigungen &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Dimensionen mit aktiviertem Schreibzugriff](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [Aggregationen und Aggregationsentwürfe](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [Partitionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Dimensionen mit aktiviertem Schreibzugriff](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  

