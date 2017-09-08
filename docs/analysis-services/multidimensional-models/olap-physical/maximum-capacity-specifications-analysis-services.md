---
title: "Spezifikationen der maximalen Kapazität (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
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
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cb411a22638d709e633504675bd91dbcfa835810
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="maximum-capacity-specifications-analysis-services"></a>Spezifikationen der maximalen Kapazität (Analysis Services)
  Die folgenden Tabellen geben die maximalen Größe und Anzahl verschiedener in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Komponenten definierter Objekte unter unterschiedlichen Serverbereitstellungsmodi an.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Mehrdimensionale und Datamining (DeploymentMode = 0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode = 1)](#bkmk_sharepoint)  
  
 [Tabellarisch (DeploymentMode = 2)](#bkmk_vertipaq)  
  
##  <a name="bkmk_OLAP"></a>Mehrdimensionale und Datamining (DeploymentMode = 0)  
 Der MOLAP-Speichermodus, der sowohl Daten als auch Metadaten speichert, verfügt über zusätzliche physische Grenzen für Dateigrößen. Zeichenfolgenspeicherdateien weisen standardmäßig eine maximale Größe von 4 GB auf. Wenn Sie größere Dateien für Zeichenfolgenspeicher benötigen, können Sie eine andere Zeichenfolgenspeicherarchitektur angeben. Weitere Informationen finden Sie unter [Zeichenfolgenspeicher für Dimensionen und Partitionen konfigurieren](../../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md).  
  
|Objekt|Maximale Größe/Anzahl|  
|------------|----------------------------|  
|Datenbank in einer Instanz|2^31-1 = 2,147,483,647|  
|Dimensionen in einer Datenbank|2^31-1 = 2,147,483,647|  
|Attribute in einer Dimension|2^31-1 = 2,147,483,647|  
|Elemente in einem Dimensionsattribut|2^31-1 = 2,147,483,647|  
|Benutzerdefinierte Hierarchien in einer Dimension|2^31-1 = 2,147,483,647|  
|Ebenen in einer benutzerdefinierten Hierarchie|2^31-1 = 2,147,483,647|  
|Cubes in einer Datenbank|2^31-1 = 2,147,483,647|  
|Measuregruppen in einem Cube|2^31-1 = 2,147,483,647|  
|Measures in einer Measuregruppe|2^31-1 = 2,147,483,647|  
|Berechnungen in einem Cube|2^31-1 = 2,147,483,647|  
|KPIs in einem Cube|2^31-1 = 2,147,483,647|  
|Aktionen in einem Cube|2^31-1 = 2,147,483,647|  
|Partitionen in einem Cube|2^31-1 = 2,147,483,647|  
|Übersetzungen in einem Cube|2^31-1 = 2,147,483,647|  
|Aggregationen in einer Partition|2^31-1 = 2,147,483,647|  
|Von einer Abfrage zurückgegebene Zellen|2^31-1 = 2,147,483,647|  
|Datensatzgröße in der Quellabfrage|64 KB|  
|Die Länge von Objektnamen|100 Zeichen|  
|Maximale Anzahl unterschiedlicher Statusangaben in einer Attributspalte eines Data Mining-Modells|2^31-1 = 2,147,483,647|  
|Maximale Anzahl berücksichtigter Attribute (Funktionsauswahl)|2^31-1 = 2,147,483,647|  
  
 Weitere Informationen zu objektbenennungsrichtlinien finden Sie unter [ASSL-Objekte und-Objekteigenschaften](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
 Weitere Informationen zu datenquellenbegrenzungen für online analytical Processing (OLAP) und Datamining finden Sie unter [unterstützte Datenquellen &#40; SSAS – mehrdimensional &#41; ](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md), [Unterstützte Datenquellen &#40; SSAS – mehrdimensional &#41; ](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md), und [ASSL-Objekte und-Objekteigenschaften](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
##  <a name="bkmk_sharepoint"></a>SharePoint (DeploymentMode = 1)  
  
|Objekt|Maximale Größe/Anzahl|  
|------------|----------------------------|  
|Datenbank in einer Instanz|2^31-1 = 2,147,483,647|  
|Tabellen in einer Datenbank|2^31-1 = 2,147,483,647|  
|Spalten in einer Tabelle|2^31-1 = 2,147,483,647<br /><br /> **Warnung:** Gesamtanzahl der Spalten in einer Tabelle hängt von der Gesamtzahl von Measures und berechneten Spalten derselben Tabelle zugeordnet sind.<br /><br /> Die maximale Anzahl von 'Spalten + Measures + berechnete Spalten' für eine Tabelle ist 2^31-1 = 2,147,483,647|  
|Zeilen in einer Tabelle|Unbegrenzt<br /><br /> **Warnung:** mit der Einschränkung, dass keine einzelne Spalte nicht mehr als 1.999.999.997 unterschiedliche Werte enthalten kann.|  
|Hierarchien in einer Tabelle|2^31-1 = 2,147,483,647|  
|Ebenen in einer Hierarchie|2^31-1 = 2,147,483,647|  
|Beziehungen|2^31-1 = 2,147,483,647|  
|Schlüsselspalten in einer Tabelle|2^31-1 = 2,147,483,647|  
|Measures in einer Tabelle|2^31-1 = 2,147,483,647<br /><br /> **Warnung:** Gesamtzahl von Measures in einer Tabelle hängt von der Gesamtanzahl der Spalten und berechneten Spalten derselben Tabelle zugeordnet sind.<br /><br /> Die maximale Anzahl von 'Spalten + Measures + berechnete Spalten' für eine Tabelle ist 2^31-1 = 2,147,483,647|  
|Berechnete Spalten in einer Tabelle|2^31-1 = 2,147,483,647<br /><br /> **Warnung:** Gesamtzahl der berechneten Spalten in einer Tabelle hängt von der Gesamtanzahl der Spalten und Measures, die der gleichen Tabelle zugeordnet sind.<br /><br /> Die maximale Anzahl von 'Spalten + Measures + berechnete Spalten' für eine Tabelle ist 2^31-1 = 2,147,483,647|  
|Von einer Abfrage zurückgegebene Zellen|2^31-1 = 2,147,483,647|  
|Datensatzgröße in der Quellabfrage|64 KB|  
|Die Länge von Objektnamen|100 Zeichen|  
  
##  <a name="bkmk_vertipaq"></a>Tabellarisch (DeploymentMode = 2)  
Im folgenden werden die theoretischen Grenzwerte. Leistung wird am niedrigere Zahlen verringert werden.   

|Objekt|Maximale Größe/Anzahl|  
|------------|----------------------------|  
|Datenbank in einer Instanz|16,000|  
|Kombinierte Anzahl von Tabellen und Spalten in einer Datenbank|16,000|  
|Zeilen in einer Tabelle|Unbegrenzt<br /><br /> **Warnung:** mit der Einschränkung, dass eine einzelne Spalte in der Tabelle nicht mehr als 1.999.999.997 unterschiedliche Werte haben kann.|  
|Hierarchien in einer Tabelle|15,999|  
|Ebenen in einer Hierarchie|15,999|  
|Beziehungen|8.000|  
|Schlüsselspalten in alle Tabelle|15,999|  
|Measures in einem Tabellen|2^31-1 = 2,147,483,647|  
|Von einer Abfrage zurückgegebene Zellen|2^31-1 = 2,147,483,647|  
|Datensatzgröße in der Quellabfrage|64 KB|  
|Die Länge von Objektnamen|512 Zeichen lang sein|  
  
## <a name="see-also"></a>Siehe auch  
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Allgemeine Eigenschaften](../../../analysis-services/server-properties/general-properties.md)  
  
  

