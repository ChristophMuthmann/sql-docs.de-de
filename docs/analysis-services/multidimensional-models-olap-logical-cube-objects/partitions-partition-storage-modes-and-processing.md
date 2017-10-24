---
title: Partition Speichermodi und Verarbeitung | Microsoft Docs
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
- storage [Analysis Services], partitions
- hybrid OLAP
- data storage [Analysis Services]
- relational OLAP
- multidimensional OLAP
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- HOLAP
- MOLAP
- ROLAP
ms.assetid: 86d17547-a0b6-47ac-876c-d7a5b15ac327
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d94daaeb72996f418f7f1b30dd8a8b4d76e9a5c6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="partitions---partition-storage-modes-and-processing"></a>Partitionen – Partition Speichermodi und Verarbeitung
  Der Speichermodus einer Partition wirkt sich auf die Abfrage- und Verarbeitungsleistung, die Speicheranforderungen und die Speicherorte der Partition, der übergeordneten Measuregruppe und des übergeordneten Cubes aus. Die Entscheidung für einen Speichermodus wirkt sich zudem auf die Verarbeitungsmöglichkeiten aus.  
  
 Für eine Partition kann einer von drei grundlegenden Speichermodi verwendet werden:  
  
-   Mehrdimensionale OLAP (MOLAP)  
  
-   Relationale OLAP (ROLAP)  
  
-   Hybride OLAP (HOLAP)  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt alle drei grundlegenden Speichermodi. Zudem wird die proaktive Zwischenspeicherung unterstützt. Damit können die Merkmale der ROLAP-Speicherung und der MOLAP-Speicherung sowohl für die Unmittelbarkeit der Daten als auch für die Abfrageleistung kombiniert werden. Weitere Informationen finden Sie unter [Proaktives Zwischenspeichern &#40;Partitionen&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="molap"></a>MOLAP  
 Der Speichermodus MOLAP bewirkt, dass die Aggregationen der Partition sowie eine Kopie der zugehörigen Quelldaten in einer mehrdimensionalen Struktur in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gespeichert werden, wenn die Partition verarbeitet wird. Diese MOLAP-Struktur ist stark optimiert, um die Abfrageleistung zu maximieren. Als Speicherort kann der Computer, auf dem die Partition definiert wurde, oder ein anderer Computer mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwendet werden. Da sich eine Kopie der Quelldaten in der mehrdimensionalen Struktur befindet, können Abfragen aufgelöst werden, ohne auf die Quelldaten der Partition zuzugreifen. Durch das Verwenden von Aggregationen können die Antwortzeiten für Abfragen erheblich verbessert werden. Die Daten in der MOLAP-Struktur der Partition sind nur so aktuell wie am Datum, an dem die letzte Verarbeitung der Partition erfolgte.  
  
 Da sich die Quelldaten ändern, müssen Objekte mit MOLAP-Speicherung regelmäßig verarbeitet werden, um diese Änderungen aufzunehmen und sie den Benutzern zur Verfügung zu stellen. Durch die Verarbeitung werden die Daten in der MOLAP-Struktur entweder vollständig oder inkrementell aktualisiert. Die Zeit zwischen zwei Verarbeitungsvorgängen bewirkt eine Latenzzeit, während derer Daten in OLAP-Objekten möglicherweise nicht mit den Quelldaten übereinstimmen. Sie können Objekte mit MOLAP-Speicherung inkrementell oder vollständig aktualisieren, ohne die Partition oder den Cube offline schalten zu müssen. In bestimmten Situationen kann es jedoch erforderlich sein, einen Cube offline zu schalten, um bestimmte Strukturänderungen an OLAP-Objekten zu verarbeiten. Sie können die zum Aktualisieren der MOLAP-Speicherung erforderliche Ausfallzeit minimieren, indem Sie Cubes auf einem Stagingserver aktualisieren und verarbeiten und die verarbeiteten Objekte mithilfe der Datenbanksynchronisierung auf den Produktionsserver kopieren. Sie können auch die proaktive Zwischenspeicherung verwenden, um die Latenzzeit zu minimieren und die Verfügbarkeit zu optimieren und dabei gleichzeitig die Leistungsvorteile der MOLAP-Speicherung weiter zu nutzen. Weitere Informationen finden Sie unter [proaktives Zwischenspeichern &#40; Partitionen &#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md), [Analysis Services-Datenbanken synchronisieren](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md), und [Verarbeiten eines mehrdimensionalen Modells &#40; Analysis Services &#41; ](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="rolap"></a>ROLAP  
 Der Speichermodus ROLAP bewirkt, dass die Aggregationen der Partition in indizierten Sichten in der relationalen Datenbank gespeichert werden, die in den Quelldaten der Partition angegeben wurde. Im Gegensatz zu den MOLAP-Speichermodus ROLAP bewirkt nicht, eine Kopie der Quelldaten in gespeichert werden die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datenordner. Wenn Ergebnisse nicht aus dem Abfragecache übernommen werden können, werden Abfragen stattdessen mithilfe der indizierten Sichten in der Datenquelle beantwortet. Beim ROLAP-Speicher erfolgt die Beantwortung von Abfragen i. A. langsamer als bei Verwendung der Speichermodi MOLAP oder HOLAP. Auch die Verarbeitungszeit ist bei ROLAP üblicherweise länger. ROLAP ermöglicht den Benutzern jedoch das Anzeigen von Daten in Echtzeit und kann dazu beitragen, Speicherplatz zu sparen, wenn Sie mit großen Datasets arbeiten, die nur unregelmäßig abgefragt werden, z. B. mit reinen Vergangenheitsdaten.  
  
> [!NOTE]  
>  Bei Verwendung von ROLAP [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gelegten fehlerhafte Informationen bezüglich des unbekannten Elements, wenn ein Join mit einer GROUP BY-Klausel kombiniert wird. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]entfernt relationale Integritätsfehler anstatt den unbekannten Elementwert zurückzugeben.  
  
 Wenn eine Partition den Speichermodus ROLAP verwendet und die zugehörigen Quelldaten in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gespeichert sind, erstellt [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] indizierte Sichten, die Aggregationen der Partition enthalten. Wenn [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] keine indizierten Sichten erstellen werden keine Aggregationstabellen erstellt. Obwohl die Sitzungsanforderungen für das Erstellen indizierter Sichten im [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durch [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] behandelt werden, müssen für das Erstellen indizierter Sichten für Aggregationen durch [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die folgenden Bedingungen durch die ROLAP-Partition und die Tabellen im zugehörigen Schema erfüllt sein:  
  
-   Die Partition darf keine Measures enthalten, die die Aggregatfunktionen **Min** oder **Max** verwenden.  
  
-   Jede Tabelle im Schema der ROLAP-Partition darf nur einmal verwendet werden. Das Schema darf beispielsweise nicht [dbo].[address] AS "Customer Address" und [dbo].[address] AS "SalesRep Address" enthalten.  
  
-   Jede Tabelle muss eine Tabelle sein, keine Sicht.  
  
-   Alle Tabellennamen im Schema der Partition müssen mit dem Besitzernamen gekennzeichnet sein, z. B. [dbo].[customer].  
  
-   Alle Tabellen im Schema der Partition müssen denselben Besitzer aufweisen. Sie können beispielsweise keine FROM-Klausel verwenden, die auf die Tabellen in [tk].[customer], [john].[store] und [dave].[sales_fact_2004] verweist.  
  
-   Die Quellspalten der Measures der Partition dürfen keine NULL-Werte zulassen.  
  
-   Beim Erstellen aller in der Sicht verwendeten Tabellen müssen die folgenden Optionen auf ON festgelegt sein:  
  
    -   ANSI_NULLS  
  
    -   QUOTED_IDENTIFIER  
  
-   Die Gesamtgröße des Indexschlüssels in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] darf 900 Bytes nicht überschreiten. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]implementiert diese Bedingung basierend auf den Schlüsselspalten fester Länge, wenn die CREATE INDEX-Anweisung verarbeitet wird. Jedoch, wenn der Indexschlüssel Spalten variabler Länge stehen [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] auch implementiert diese Bedingung bei jedem Update der Basistabellen. Da unterschiedliche Aggregationen unterschiedliche Sichtdefinitionen aufweisen, kann die ROLAP-Verarbeitung mithilfe indizierter Sichten je nach Aggregationsentwurf erfolgreich verlaufen oder fehlschlagen.  
  
-   Für die Sitzung, in der die indizierte Sicht erstellt wird, müssen die folgenden Optionen den Wert ON aufweisen: ARITHABORT, CONCAT_NULL_YEILDS_NULL, QUOTED_IDENTIFIER, ANSI_NULLS, ANSI_PADDING und ANSI_WARNING. Diese Einstellung kann in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] vorgenommen werden.  
  
-   Für die Sitzung, in der die indizierte Sicht erstellt wird, muss die folgende Option den Wert OFF aufweisen: NUMERIC_ROUNDABORT. Diese Einstellung kann in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] vorgenommen werden.  
  
## <a name="holap"></a>HOLAP  
 Der Speichermodus HOLAP kombiniert Attribute von MOLAP und ROLAP. Wie bei MOLAP, HOLAP führt die Aggregationen der Partition in einer mehrdimensionalen Struktur in zu speichernde ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz. Die Verwendung von HOLAP führt nicht dazu, dass eine Kopie der Quelldaten gespeichert wird. Bei Abfragen, die lediglich auf zusammengefasste Daten in den Aggregationen einer Partition zugreifen, ist HOLAP das Äquivalent zu MOLAP. Abfragen, die auf Quelldaten zugreifen (wie z. B. bei einem Drilldown auf eine atomare Cubezelle, für die keine Aggregationsdaten vorhanden sind), müssen Daten aus der relationalen Datenbank abrufen, sodass mehr Zeit beansprucht wird, als wenn die Quelldaten in der MOLAP-Struktur gespeichert wären. Beim Speichermodus HOLAP werden Benutzer normalerweise erhebliche Unterschiede bei den Abfragezeiten feststellen, je nachdem, ob die Abfrage anhand das Caches oder mittels Aggregationen aufgelöst werden kann oder ob hierzu die Quelldaten selbst benötigt werden.  
  
 Partitionen mit HOLAP-Speicherung sind kleiner als die vergleichbaren MOLAP-Partitionen, da sie keine Quelldaten enthalten, und antworten schneller als ROLAP-Partitionen auf Abfragen, die zusammengefasste Daten einbeziehen. Der Speichermodus HOLAP eignet sich i. A. für Partitionen in Cubes, die schnelle Abfrageantworten für Zusammenfassungen erfordern, die auf großen Mengen von Quelldaten basieren. Wenn Benutzer jedoch Abfragen generieren, die auf Daten auf Blattebene zugreifen müssen, wie z. B. beim Berechnen des Medians, eignet sich MOLAP i. A. besser.  
  
## <a name="see-also"></a>Siehe auch  
 [Proaktives Zwischenspeichern &#40; Partitionen &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [Synchronisieren von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Partitionen &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  

