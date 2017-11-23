---
title: "Ändern der Eigenschaften in einer Datenquellensicht (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
helpviewer_keywords:
- friendly names [Analysis Services]
- names [Analysis Services], data source views
- viewing tables
- displaying tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 4ccdabea-9c4d-460d-ba78-d23068143696
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fa1e0fa67c2a9dca58b4cfcff33407994810baa5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="change-properties-in-a-data-source-view-analysis-services"></a>Ändern von Eigenschaften in einer Datenquellensicht (Analysis Services)
  Nachdem Sie eine Datenquellensicht mithilfe des Datenquellensicht-Assistenten definiert und der Datenquellensicht Tabellen, Sichten, benannte Berechnungen und benannte Abfrage hinzugefügt haben, kann es gewünscht sein, Eigenschaften zu ändern, die Folgendes betreffen:  
  
-   Übereinstimmungskriterien für Datenquellensichten  
  
-   Erweiterte Optionen für Datenquellensichten  
  
-   Objektnamen  
  
-   Objektmetadaten  
  
 Sie können zudem von der Datenquelle abgerufene Objektmetadaten anzeigen, die Sie nicht ändern können.  
  
## <a name="viewing-or-changing-data-source-view-properties"></a>Anzeigen oder Ändern der Eigenschaften von Datenquellensichten  
 Eigenschaften einer Datenquellensicht werden, anders als eine Beschreibung der Datenquellensicht, vom Datenquellensicht-Assistenten festgelegt, wenn Sie die Datenquellensicht erstmalig definieren. In der folgenden Tabelle sind die Eigenschaften einer Datenquellensicht aufgeführt und beschrieben.  
  
> [!NOTE]  
>  Im Eigenschaftenbereich werden Eigenschaften sowohl für die DSV-Datei als auch für das DSV-Objekt angezeigt. Um die Eigenschaften des Objekts anzuzeigen, doppelklicken Sie im Projektmappen-Explorer darauf. Die Eigenschaften werden aktualisiert und entsprechen daraufhin den Eigenschaften in der folgenden Tabelle.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|Datenquelle|Gibt die Datenquelle innerhalb der Datenquellensicht an, deren Eigenschaften Sie anzeigen.|  
|Description|Gibt eine Beschreibung der Datenquellensicht an.|  
|Name|Gibt den Namen der Datenquellensicht an, der im Projektmappen-Explorer oder in der Analysis Services-Datenbank angezeigt wird. Sie können den Namen der Datenquellensicht hier oder im Projektmappen-Explorer ändern.|  
|NameMatchingCriteria|Die Namensübereinstimmungskriterien für die Datenquelle. Die Standardeinstellung ist (Keine), wenn Primärschlüssel/Fremdschlüssel-Beziehungen vom Datenquellensicht-Assistenten ermittelt wurden. Unabhängig davon, ob diese Eigenschaft vom Datenquellensicht-Assistenten festgelegt wurde, können Sie hier einen Wert angeben. Wenn Datenbankbeziehungen vorhanden sind und Sie Namensübereinstimmungskriterien angeben, werden beide Einstellungen verwendet, um auf Beziehungen zwischen vorhandenen Tabellen und neu hinzugefügten Tabellen zu schließen.|  
|RetrieveRelationships|Gibt an, ob Beziehungen aus der Datenbank abgerufen werden. Der Standardwert lautet "True".|  
|SchemaRestriction|Gibt ggf. die Einschränkungen für die Schemas an, die aus einer Datenquelle abgerufen werden. Standardmäßig sind keine Schemaeinschränkungen vorhanden.|  
  
## <a name="viewing-or-changing-datatable-properties"></a>Anzeigen oder Ändern von DataTable-Eigenschaften  
 **DataTable** -Eigenschaften sind die Eigenschaften von Tabellen, Sichten und benannten Abfragen in einer Datenquellensicht. Die Eigenschaften werden festgelegt, wenn der Datenquellensicht eines dieser Objekte hinzugefügt wird. In der folgenden Tabelle sind die Eigenschaften von **DataTable** -Objekten in einer Datenquellensicht aufgeführt und beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|AllowChangesDuringGeneration|Gibt an, ob der Schemagenerierungs-Assistent berechtigt ist, eine Datenquellensicht-Tabelle während der erneuten Generierung zu überschreiben. Diese Eigenschaft ist nur für Tabellen vorhanden, die ursprünglich vom Schemagenerierungs-Assistenten generiert wurden. Weitere Informationen finden Sie unter [Grundlegendes zur inkrementellen Generierung](../../analysis-services/multidimensional-models/understanding-incremental-generation.md).|  
|DataSource|Gibt die Datenquelle für das Objekt an. Sie können diese Eigenschaft nicht bearbeiten.|  
|Description|Gibt die Beschreibung für die Tabelle, die Sicht oder die benannte Abfrage an. Wenn für die zugrunde liegende Datenquellentabelle oder -sicht eine Beschreibung als erweiterte Eigenschaft gespeichert wurde, wird dieser Wert angezeigt. Sie können diese Eigenschaft bearbeiten.|  
|FriendlyName|Gibt einen Namen für die Tabelle oder die Sicht an, der für Benutzer leichter verständlich oder aussagekräftiger im Hinblick auf den Themenbereich ist. Standardmäßig ist die **FriendlyName** -Eigenschaft einer Tabelle oder einer Sicht mit der **Name** -Eigenschaft der Tabelle oder der Sicht identisch. Die **FriendlyName** -Eigenschaft wird von OLAP- und Data Mining-Objekten verwendet, wenn Objektnamen basierend auf Tabellen oder Sichten definiert werden. Sie können diese Eigenschaft bearbeiten.|  
|Name|Gibt den Namen der zugrunde liegenden Tabelle oder Sicht oder den Namen der benannten Abfrage an. Die **Name** -Eigenschaft wird von OLAP- und Data Mining-Objekten verwendet, wenn Objektnamen basierend auf benannten Abfragen definiert werden. Diese Eigenschaft kann nur bei benannten Abfragen bearbeitet werden.|  
|QueryDefinition|Gibt die Definition der benannten Abfrage an. Diese Eigenschaft kann nur auf benannte Abfragen angewendet werden; ein direktes Bearbeiten ist nicht möglich. Zum Bearbeiten dieser Eigenschaft müssen Sie die benannte Abfrage selbst bearbeiten.|  
|Schema|Gibt das Datenbankschema an, das auf die Tabelle, die Sicht oder die benannte Abfrage angewendet wird. Diese Eigenschaft kann nicht bearbeitet werden.|  
|TableType|Gibt den Tabellentyp für die Tabelle, die Sicht oder die benannte Abfrage an. Diese Eigenschaft kann nicht bearbeitet werden.|  
  
## <a name="viewing-or-changing-datacolumn-properties"></a>Anzeigen oder Ändern von DataColumn-Eigenschaften  
 **DataColumn** -Eigenschaften sind die Eigenschaften von Spalten in Tabellen, Sichten und benannten Abfragen in einer Datenquellensicht. Diese Eigenschaften werden festgelegt, wenn eines dieser Objekte entweder aus der zugrunde liegenden Tabelle oder Sicht, aus einer benannten Abfrage oder gemäß Definition durch eine benannte Berechnung der Datenquellensicht hinzugefügt wird. In der folgenden Tabelle sind die Eigenschaften von **DataColumn** -Objekten in einer Datenquellensicht aufgeführt und beschrieben.  
  
|Eigenschaft|Description|  
|--------------|-----------------|  
|AllowNull|Gibt die Eigenschaft, die die NULL-Zulässigkeit der Spalte definiert, basierend auf der Spalte in der zugrunde liegenden Tabelle, Sicht oder benannten Abfrage an. Diese Eigenschaft kann nicht bearbeitet werden.|  
|DataType|Gibt den Datentyp der Spalte basierend auf der Spalte in der zugrunde liegenden Tabelle, Sicht oder benannten Abfrage an. Diese Eigenschaft kann nicht direkt bearbeitet werden. Wenn Sie jedoch den Datentyp einer Spalte aus einer Tabelle oder Sicht ändern müssen, können Sie die Tabelle durch eine benannte Abfrage ersetzen, die die Spalte in den gewünschten Datentyp konvertiert.|  
|DateTimeMode|Gibt das Datumsserialisierungsformat für **DateTime** -Spalten an. Der Standardwert ist **UnspecifiedLocal**. Diese Eigenschaft kann bearbeitet werden.|  
|Description|Gibt die Beschreibung für die Spalte an. Wenn für die zugrunde liegende Datenbankspalte eine Beschreibung als erweiterte Eigenschaft gespeichert wurde, wird dieser Wert angezeigt. Sie können diese Eigenschaft bearbeiten.|  
|FriendlyName|Gibt den Namen für eine Spalte aus einer Tabelle oder Sicht an, der für Benutzer leichter verständlich oder aussagekräftiger im Hinblick auf den Themenbereich ist. Standardmäßig ist die **FriendlyName** -Eigenschaft einer Spalte aus einer Tabelle oder Sicht mit der **Name** -Eigenschaft der Spalte identisch. Die **FriendlyName** -Eigenschaft wird von OLAP- und Data Mining-Objekten verwendet, wenn Attribute basierend auf Spalten aus Tabellen oder Sichten definiert werden. Sie können diese Eigenschaft bearbeiten.|  
|Länge|Gibt die maximale Länge der Spalte basierend auf den Daten in der Spalte in der zugrunde liegenden Tabelle oder Sicht an.|  
|Name|Gibt den Namen der zugrunde liegenden Spalte oder den Namen der benannten Berechnung an. Die **Name** -Eigenschaft wird von OLAP- und Data Mining-Objekten verwendet, wenn Attribute basierend auf benannten Berechnungen definiert werden. Diese Eigenschaft kann nur bei benannten Berechnungen bearbeitet werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellensichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Verwenden von Diagrammen im Datenquellensicht-Designer &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  
