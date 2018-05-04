---
title: Datenquellen in mehrdimensionalen Modellen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9d438cbd6bdbcd77e6f00cf8baea770fb0e16fad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-sources-in-multidimensional-models"></a>Datenquellen in mehrdimensionalen Modellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Alle Daten, die Sie importieren oder in ein mehrdimensionales Modell laden, stammen aus einer externen Datenquelle. In der Regel stammen Quelldaten aus einem Data Warehouse, das für Berichtszwecke entworfen wurde, sie können jedoch auch aus einer beliebigen relationalen Datenbank stammen, auf die direkt oder indirekt über einen Mittler zugegriffen wird, z. B. ein [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paket.  
  
 Die direkte Verbindung mit einer externen Datenquelle wird von einem **Datenquellenobjekt** in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] angegeben. Neben dem physischen Speicherort gibt ein Datenquellenobjekt die Verbindungszeichenfolge, den Datenanbieter, die Anmeldeinformationen und weitere Eigenschaften an, die das Verbindungsverhalten steuern.  
  
 Die vom Datenquellenobjekt bereitgestellten Informationen werden während der folgenden Vorgänge verwendet:  
  
-   Abrufen von Schemainformationen und anderen Metadaten, die zum Generieren von Datenquellensichten in einem Modell verwendet werden.  
  
-   Abfragen oder Laden von Daten in ein Modell während der Verarbeitung.  
  
-   Ausführen von Abfragen für mehrdimensionale oder Data Mining-Modelle, die den ROLAP-Speichermodus verwenden  
  
-   Lesen oder Schreiben in Remotepartitionen  
  
-   Herstellen einer Verbindung mit verknüpften Objekten sowie Synchronisieren von Ziel zu Quelle  
  
-   Ausführen von Rückschreibevorgängen, die in einer relationalen Datenbank gespeicherte Faktentabellendaten aktualisieren  
  
 Wenn Sie ein mehrdimensionales Modell komplett neu erstellen, beginnen Sie, indem Sie das Datenquellenobjekt erstellen, und verwenden dieses dann zum Generieren des nächsten Objekts, einer **Datenquellensicht**. Die Datenquellensicht bildet die Datenabstraktionsebene im Modell. Sie wird in der Regel nach dem Datenquellenobjekt erstellt, wobei das Schema der Quelldatenbank als Grundlage verwendet wird. Sie können jedoch auch andere Möglichkeiten zum Erstellen eines Modells wählen, u. a. den Beginn mit Cubes und Dimensionen oder das Generieren des Schemas, das Ihren Entwurf am besten unterstützt.  
  
 Unabhängig davon, wie Sie das Modell erstellen, benötigt jedes mindestens ein Datenquellenobjekt, das eine Verbindung mit den Quelldaten angibt. Sie können in einem einzelnen Modell mehrere Datenquellenobjekte erstellen, um Daten aus verschiedenen Quellen zu verwenden oder die Verbindungseigenschaften für bestimmte Objekte zu variieren.  
  
 Datenquellenobjekte können unabhängig von anderen Objekten im Modell verwaltet werden. Wenn Sie eine Datenquelle erstellt haben, können Sie deren Eigenschaften später ändern und dann das Modell vorverarbeiten, um sicherzustellen, dass die Daten ordnungsgemäß abgerufen werden.  
  
## <a name="related-topics-and-tasks"></a>Verwandte Themen und Tasks  
  
|Thema|Description|  
|-----------|-----------------|  
|[Unterstützte Datenquellen &#40;SSAS – Mehrdimensional&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)|Beschreibt die Datenquellentypen, die in einem tabellarischen Modell verwendet werden können.|  
|[Erstellen einer Datenquelle & #40; SSAS – mehrdimensional & #41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)|Erklärt, wie einem mehrdimensionalen Modell ein Datenquellenobjekt hinzugefügt wird.|  
|[Löschen einer Datenquelle im Projektmappen-Explorer & #40; SSAS – mehrdimensional & #41;](../../analysis-services/multidimensional-models/delete-a-data-source-in-solution-explorer-ssas-multidimensional.md)|Verwenden Sie diese Vorgehensweise, um ein Datenquellenobjekt aus einem mehrdimensionalen Modell zu löschen.|  
|[Festlegen von Datenquelleneigenschaften & #40; SSAS – mehrdimensional & #41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)|Beschreibt jede Eigenschaft und erläutert deren Festlegung.|  
|[Festlegen von Identitätswechseloptionen & #40; SSAS – mehrdimensional & #41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)|Erklärt, wie die Optionen im Dialogfeld "Identitätswechselinformationen" konfiguriert werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankobjekte & #40; Analysis Services – mehrdimensionale Daten & #41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Logische Architektur & #40; Analysis Services – mehrdimensionale Daten & #41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Datenquellen und Bindungen & #40; SSAS – mehrdimensional & #41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
