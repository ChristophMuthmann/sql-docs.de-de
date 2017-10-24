---
title: DISCOVER_DATASOURCES-Rowset | Microsoft Docs
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
apiname:
- DISCOVER_DATASOURCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_DATASOURCES rowset
ms.assetid: f3ff26ab-a447-416b-ba54-1716df2283de
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9c91d5b1d3e0fb7ec972e47079a1bf36d8f9b87
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="discoverdatasources-rowset"></a>DISCOVER_DATASOURCES-Rowset
  Gibt eine Liste der XMLA-Anbieterdatenquellen (XML for Analysis) zurück, die auf dem Server oder dem Webdienst verfügbar sind. Die veröffentlichten Datenquellen werden von einer URL des Anwendungswebservers zurückgegeben. Der Client kann eine Verbindung mit einer der Datenquellen in der Liste herstellen.  
  
 Beim Aufrufen der [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode mit der **DISCOVER_DATASOURCES** Enumerationswert in der [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) Element, das **Discover** Methode gibt die **DISCOVER_DATASOURCES** Rowset.  
  
 **Gilt für:** tabellarische und mehrdimensionale Modelle  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Der Client wählt eine Datenquelle durch Festlegen der **DataSourceInfo** Eigenschaft in der [Eigenschaften](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md) Element, das zusammen mit gesendet wird die [Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md) Element durch das [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode. Ein Client sollte nicht den Inhalt des Erstellen der **DataSourceInfo** Eigenschaft, um an den Server gesendet. Der Client sollte stattdessen verwenden die **Discover** Methode, um die Datenquellen zu ermitteln, die der Anbieter unterstützt. Der Client sendet dann den gleichen Wert für die **DataSourceInfo** Eigenschaft, die sie aus der **DISCOVER_DATASOURCES** Rowset.  
  
 Die **DISCOVER_DATASOURCES** Rowset enthält die folgenden Spalten.  
  
|Spaltenname|Typindikator|Einschränkung|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**Datenquellenname**|**DBTYPE_WSTR**|ja|Der Name der Datenquelle, z. B. **Adventure Works**.|  
|**DataSourceDescription**|**DBTYPE_WSTR**||Die vom Verleger eingegebene Beschreibung der Datenquelle.<br /><br /> Kann **NULL**zurückgeben.|  
|**URL**|**DBTYPE_WSTR**|ja|Der eindeutige Pfad, der angibt, wo die XMLA-Methoden (XML for Analysis) für diese Datenquelle aufgerufen werden.<br /><br /> Kann **NULL**zurückgeben.|  
|**DataSourceInfo**|**DBTYPE_WSTR**||Eine Zeichenfolge, die alle zusätzlichen Informationen enthält, die erforderlich sind, um eine Verbindung mit der Datenquelle herzustellen.<br /><br /> Kann **NULL**zurückgeben.|  
|**ProviderName**|**DBTYPE_WSTR**|ja|Der Name des Anbieters für die Datenquelle.<br /><br /> Beispiel:`"MSOLAP"`<br /><br /> Kann **NULL**zurückgeben.|  
|**ProviderType**|**DBTYPE_WSTR**|ja|Die vom Anbieter unterstützten Datentypen. Dieses Array kann einen oder mehrere der folgenden Typen enthalten:<br /><br /> **MDP**: multidimensionaler Datenanbieter.<br /><br /> **TDP**: tabellarischer Datenanbieter.<br /><br /> **DMP**: Datamining-Anbieter (implementiert die OLE für DB für Data Mining-Spezifikation).|  
|**AuthenticationMode**|**DBTYPE_WSTR**|ja|Eine Spezifikation, die angibt, welchen Typ des Sicherheitsmodus die Datenquelle verwendet. Folgende Werte sind möglich:<br /><br /> **Nicht authentifizierte**: keine Benutzer-ID oder ungültiges Kennwort gesendet werden muss.<br /><br /> **Authentifizierte**: Benutzer-ID und Kennwort in den für die Verbindung mit der Datenquelle erforderlichen Informationen enthalten sein müssen.<br /><br /> **Integrierte**: die Datenquelle verwendet die zugrundeliegende Sicherheit, um zu bestimmen, Autorisierung, z. B. integrierte Sicherheit von bereitgestellten [!INCLUDE[msCoName](../../../includes/msconame-md.md)] (Internet Information Services, IIS).|  
  
 Dieses Schemarowset ist nicht sortiert.  
  
> [!IMPORTANT]  
>  Die **DISCOVER_DATASOURCES** Rowset kann nicht mithilfe von DMV-Abfragen und die SELECT-Befehlssyntax abgefragt werden. Allerdings die **DISCOVER_DATASOURCES** Rowset kann abgefragt werden, mithilfe von <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|Wert|  
|--------------|-----------|  
|GUID|06c03d41-f66d-49f3-b1b8-987f7af4cf18|  
|ADOMDNAME|DataSources|  
  
## <a name="see-also"></a>Siehe auch  
 [XML for Analysis-Schemarowsets](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

