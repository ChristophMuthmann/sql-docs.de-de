---
title: CSDLBI-Attribute für Berichtsentwurf | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 61ba3a27-790e-43bc-b421-e01bf2fdbda6
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: dc31de2ee816712630ddbd5c953248a9cf73d3d4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="csdlbi-attributes-for-report-design"></a>CSDLBI-Attribute für Berichtsentwurf
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In diesem Abschnitt werden die Attribute in den Erweiterungen für CSDL für Tabellenmodellierung beschrieben, die sich auf den [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]-Abfrageentwurf auswirken.  
  
## <a name="model-attributes"></a>Modellattribute  
 Diese Attribute werden für ein Unterelement eines [EntityContainer](http://msdn.microsoft.com/library/bb399169.aspx) -Elements der CSDL definiert.  
  
|Attributname|Datentyp|Description|  
|--------------------|---------------|-----------------|  
|Culture|Text|Gibt die für Währungsformate verwendete Kultur an. Wenn keine Angabe erfolgt, wird EN-US verwendet.|  
|IsRightToLeft|Boolean|Gibt an, ob die Werte von Textfeldern standardmäßig von rechts nach links gelesen werden sollen.|  
  
## <a name="entity-attributes"></a>Entitätsattribute  
 Diese Attribute werden für ein Unterelement eines EntitySet-Elements oder EntityType-Elements der CSDL definiert.  
  
|Attributname|Datentyp|Description|  
|--------------------|---------------|-----------------|  
|**Verweisname**|Text|Der Bezeichner, der verwendet wird, um in einer DAX-Abfrage auf diese Entität zu verweisen. Wenn kein Bezeichner angegeben wird, wird der Name verwendet.|  
|**Beschriftung**|Text|Der Anzeigename für die Entität.|  
|**Dokumentation**|Text|Beschreibender Text, der Geschäftskunden die Bedeutung der Daten erläutert.|  
|**Hidden**|Boolean|Gibt an, ob die Entität angezeigt werden soll. Der Standardwert ist **false**.|  
|**CollectionCaption**|Text|Der Pluralname für den Verweis auf einen Satz von Instanzen der Entität. Wenn der Name nicht angegeben wird, wird das Caption-Attribut verwendet.|  
|**DisplayKey**|MemberRef[]|Eine sortierte Felderliste, mit der einem Geschäftskunden eine Entitätsinstanz angezeigt wird. Die Verweise können Instanz- und Navigationseigenschaften einschließen. Wenn auf eine Navigationseigenschaft verwiesen wird, wird der **DisplayKey** der Zielentität angezeigt. Wenn der **DisplayKey** -Wert ausgelassen wird, wird das Schlüsselfeld verwendet.|  
|**DefaultImage**|MemberRef|Ein Verweis auf das Feld, das ein Bild enthält, mit dem einem Geschäftskunden visuell eine Entitätsinstanz angezeigt wird. Wenn der Verweis nicht angegeben wird, wird das erste Bildfeld in der Entität verwendet (sofern vorhanden).|  
|**DefaultDetails**|MemberRef[]|Eine sortierte Liste von Feldern, die den Standardsatz der Detailinformationen darstellt, die einem Geschäftsbenutzer zu einer Entitätsinstanz angezeigt werden. Wenn die Liste nicht angegeben wird, werden die ersten fünf Felder in der Entität verwendet, wobei die Felder ausgeschlossen werden, auf die bereits von **Key**, **DisplayKey**oder **DefaultImage**verwiesen wird.|  
|**SortProperties**|MemberRef[]|Eine sortierte Liste von Feldern, nach denen die Entitätsinstanzen normalerweise sortiert werden. Wenn Sie einen Sortiervorgang in diesen Feldern ausführen, wird die für jedes Feld angegebene **SortDirection** verwendet. Wenn die Felderliste nicht angegeben wird, werden die **DisplayKey** -Felder verwendet.|  
|**DefaultMeasure**|MemberRef|Ein Verweis auf ein im Modell definiertes Measure oder auf ein numerisches Feld mit einer standardmäßigen Aggregatfunktion, mit dem angegeben wird, dass das Measure oder Feld für mehrere Instanzen der Entität als Standarddarstellung verwendet werden soll. Wenn der Verweis nicht angegeben wird, wird eine Anzahl der Entitätsinstanzen verwendet.|  
|**DefaultLocation**|MemberRef|Ein Verweis auf ein Feld, dessen Wert den einer Entitätsinstanz zugeordneten Standardort darstellt. Wenn der Verweis nicht angegeben wird, wird das erste Ortfeld in der Entität verwendet (sofern vorhanden).|  
  
## <a name="field-attributes"></a>Feldattribute  
 Diese Attribute werden für ein Unterelement einer CSDL-Eigenschaft oder eines [NavigationProperty](http://msdn.microsoft.com/library/bb387104.aspx) -Elements definiert.  
  
|Attributname|Datentyp|Description|  
|--------------------|---------------|-----------------|  
|**Verweisname**|Text|Der Bezeichner, der verwendet wird, um in einer DAX-Abfrage auf diese Entität zu verweisen. Wenn der Bezeichner nicht angegeben wird, wird der Feldname verwendet.|  
|**Beschriftung**|Text|Der Anzeigename für die Entität. Wenn der Name nicht angegeben wird, wird der **ReferenceName** des Felds verwendet.|  
|**Dokumentation**|Text|Beschreibender Text, der Geschäftskunden die Bedeutung des Felds erläutert.|  
|**Hidden**|Boolean|Gibt an, ob das Feld angezeigt werden soll. Der Standard ist **false**und bedeutet, dass das Feld angezeigt wird.|  
|**DisplayFolder**|Text|Der Name (vollständiger Pfad) des Ordners, in dem das Feld angezeigt wird. Wenn der Name nicht angegeben wird, wird das Feld am Modellstamm angezeigt.|  
|**ContextualNameRule**|Enum|Ein Wert, der angibt, ob und wie der Eigenschaftsname auf Grundlage des Kontexts geändert werden sollte, in dem er verwendet wird. Mögliche Werte:  **None**,  **Role**,  **Merge**.|  
|**Ausrichtung**|Enum|Ein Wert, der angibt, wie die Feldwerte in einer Tabellenpräsentation ausgerichtet werden sollten. Mögliche Werte **Default**, **Center**, **Left**, **Right**. Wenn der Wert nicht angegeben wird, wird die Ausrichtung durch den Standardwert auf Grundlage des Datentyps des Felds bestimmt.|  
|**FormatString**|Text|Eine .NET-Formatzeichenfolge, die angibt, wie der Wert des Felds standardmäßig formatiert werden sollte. Wenn die Zeichenfolge nicht angegeben wird, wird das folgende Format angenommen:<br /><br /> Datetime - Felder: regionales kurzes Datum oder "d"<br /><br /> -Gleitkommafelder und ganzzahlige Felder mit einer standardaggregatfunktion: regionale Zahl oder "n"<br /><br /> -Ganze Zahlen ohne standardaggregatfunktion: regionale Dezimalzahl oder "d"<br /><br /> Für alle anderen Feldtypen ist keine Formatzeichenfolge gültig.|  
|**Einheiten**|Text|Das Symbol, das für Feldwerte zur Darstellung von Einheiten übernommen wird. Wenn das Symbol nicht angegeben wird, werden die Einheiten als unbekannt angenommen.|  
|**Breite**|Integer|Die bevorzugte Breite in Zeichen, die zum Anzeigen der Werte des Felds in einer Tabellenpräsentation reserviert werden sollen. Wenn die Breite nicht angegeben wird, wird eine Standardbreite angenommen, die auf dem Datentyp des Felds basiert.|  
|**SortDirection**|Enum|Ein Wert, der angibt, wie die Feldwerte normalerweise sortiert werden. Mögliche Werte: **Default**, **Ascending**, **Descending**. Wenn der Wert nicht angegeben wird, wird mit dem Standardwert eine Sortierrichtung auf Grundlage des Datentyps des Felds zugewiesen.|  
|**IsRightToLeft**|Boolean|Gibt an, ob das Feld Text enthält, der von rechts nach links gelesen werden soll. Wenn der Wert nicht angegeben wird, wird die Modelleinstellung verwendet.|  
|**OrderBy**|MemberRef|Ein Verweis auf ein anderes Feld im Modell, mit dem die Sortierreihenfolge für die Werte des Felds definiert wird. Die Werte für die zwei Felder müssen über eine 1:1-Zuordnung verfügen, da das Sortierverhalten andernfalls nicht definiert wird. Wenn die Werte nicht angegeben werden, wird das Feld auf Grundlage seines eigenen Werts sortiert.|  
|**Inhalt**|Enum|Eine Enumeration, die den Untertyp oder den Inhalt des Felds beschreibt. Wenn die Enumeration nicht angegeben wird, wird kein bestimmter Untertyp angenommen, sofern der Datentyp des Felds nicht "Binary" ist. In diesem Fall wird als Datentyp "Image" angenommen. Eine vollständige Liste der unterstützten Inhaltstypen finden Sie in der AMO-Dokumentation.|  
|**DefaultAggregateFunction**|Enum|Ein Wert, der die Standardfunktion angibt (sofern vorhanden), mit der normalerweise das Feld aggregiert wird. Mögliche Werte: **None**, **Sum**, **Average**, **Count**, **Min**, **Max**. Wenn die Werte nicht angegeben werden, wird für numerische Felder **Sum** angenommen bzw. für alle anderen Felder **None** .|  
|**IsSimpleMeasure**|Boolean|Gibt an, ob ein Measure lediglich ein einfaches Aggregat eines numerischen Feldes ist. Solche Aggregate können nach Bedarf in der Abfrage problemlos definiert werden. Daher sollten sie von der Modelldefinition ausgenommen werden, um die Leistung zu verbessern. Wenn die Werte nicht angegeben werden, wird **false** angenommen.|  
|**KPI**<br /><br /> **KpiGoal**<br /><br /> **KpiStatus**|Unterelement|Gibt an, dass das Measureelement als KPI verwendet werden soll. Das KPI-Unterelement verwendet das KpiGoal-Element und das KpiStauts-Element, um das zugeordnete Anzeigebild zu definieren und Zielbereiche festzulegen.|  
  
  
