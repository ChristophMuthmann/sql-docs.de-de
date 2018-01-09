---
title: DISCOVER_CSDL_METADATA-Rowset | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: a2d3cffd-a2c4-411c-b244-9e41ebe30939
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 91fa99b0a5338f705cecff4d1622a2db0a262154
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="discovercsdlmetadata-rowset"></a>DISCOVER_CSDL_METADATA-Rowset
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Gibt Informationen über eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenmodell (tabellarisch oder mehrdimensional), die Definition des Modells im CSDLBI (Conceptual Schema Definition Language mit BI-Anmerkungen)-Format bereitstellt. CSDLBI basiert auf CSDL, einem vom Entity Data Framework verwendeten XML-Schema, das für die Kommunikation zwischen einem [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Server und dem [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] -Client verwendet wird. Die Business Intelligence (BI)-Anmerkungen stellen zusätzliche Metadaten zu Tabellenmodellen und den darin enthaltenen Objekten bereit. Weitere Informationen zu Tabellendatenmodellen finden Sie unter [CSDL-Anmerkungen für Business Intelligence &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md).  
  
 Der Sicherheitskontext des Befehls wirkt sich auf das Rowset aus, das zurückgegeben wird. Leseberechtigungen auf der Analysis Services-Instanz sind erforderlich, um die CSDL-Definition vom Server abzurufen.  
  
 Der Sprachenbezeichner des Clients, der die Rowsetanforderung ausstellt, ist in der Verbindungszeichenfolge für den Befehl enthalten und wirkt sich auf die Sprache aus, die in mehreren Eigenschaften angezeigt wurde, die als Teil des Rowsets zurückgegeben werden.  Informationen zu den Eigenschaften und der Beschreibung, auf die sich der Sprachenbezeichner möglicherweise auswirkt, finden Sie im Abschnitt mit den Hinweisen.  
  
## <a name="rowset-columns"></a>Rowsetspalten  
 Das **DISCOVER_CSDL_METADATA** -Rowset enthält die folgenden Spalten.  
  
|**Spaltenname**|**Typindikator**|**Einschränkung**|**Beschreibung**|  
|---------------------|------------------------|---------------------|---------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|ja|Gibt den Namen der Datenbank an, für die die CSDLBI-Beschreibung angefordert wurde. Bei Auslassung wird die aktuelle Datenbank verwendet.<br /><br /> Diese Einschränkung ist für alle Modelltypen erforderlich.|  
|**PERSPECTIVE_ID**|**DBTYPE_WSTR**|ja|Gibt die ID einer auf dem Modell definierten Perspektive an, die anhand von CATALOG_NAME angegeben wurde.<br /><br /> Eine optionale Einschränkung. Gilt für alle Modelltypen.|  
|**PERSPECTIVE_NAME**|**DBTYPE_WSTR**|ja|Gibt den Namen einer auf dem Modell definierten Perspektive an, die anhand von CATALOG_NAME angegeben wurde.<br /><br /> Diese Einschränkung ist erforderlich, wenn das tabellarische Modell Perspektiven enthält oder wenn eine mehrdimensionale Lösung mehrere Cubes oder Perspektiven enthält.|  
|**METADATEN**|**DBTYPE_WSTR**|nein|Eine Zeichenfolge, die die XML-Definition einer Datenquelle und ihre Eigenschaften enthält, nach dem CSDLBI-Schema.|  
|**CUBE_ID**|**DBTYPE_WSTR**|ja|Ein Zeichenfolgenbezeichner.<br /><br /> Diese Einschränkung ist für mehrdimensionale Datenbanken optional. Wenn mehrere Cubes verfügbar sind und die Einschränkung nicht angegeben wird, wird der Standardcube zurückgegeben.|  
  
## <a name="remarks"></a>Remarks  
 DISCOVER_CSDL_METADATA weist folgende Anforderungen auf:  
  
-   Die DISCOVER-Anforderung schlägt fehl, wenn eine Datenbank nicht mithilfe der CATALOG_NAME-Einschränkung angegeben wird.  
  
-   Für ein tabellarisches Modell ist eine Perspektiven-ID erforderlich, falls mehr als eine Perspektive im Modell vorhanden ist.  
  
-   Für mehrdimensionale Modelle sind sowohl der Katalogname als auch der Name des Cube (Perspektive) erforderlich.  
  
-   Wenn eine Perspektive als Einschränkung angegeben wird, wird das gleiche CSDL-Rowset wie für das Modell zurückgegeben. Allerdings sind alle Objekte, die im Modell, aber nicht in der angegebenen Perspektive enthalten sind, mit **Hidden** = True markiert.  
  
-   Für Tabellen und Spalten gibt die DISCOVER-Anforderung immer einen Wert von der Cubedimension aus. Wenn die Cubedimensionseigenschaft nicht festgelegt ist, gibt die Anforderung den Wert über die Dimension zurück.  
  
-   Die DISCOVER-Anforderung kann keine Measures oder berechnete Spalten zurückgeben, die einen Semantikfehler enthalten.  
  
-   Die DISCOVER-Anforderung gibt keine Informationen für Objekte ohne Eigenschaftswerte zurück. Die DISCOVER-Anforderung gibt auch keine Werte für Attribute zurück, die den Standardwert verwenden.  
  
 Die XML-Zeichenfolge, die im Rowset zurückgegeben wird, enthält möglicherweise die folgenden sprachspezifischen Eigenschaften oder Werte. Wenn Sie z. B. die Rowsetanforderung von einem Client mit der LCID 0403 (katalanisches Spanisch) ausstellen, gibt die Eigenschaft die folgenden Werte für katalanisches Spanisch zurück. Wenn auf dem Server keine Übersetzungen verfügbar sind, wird die Zeichenfolge für die Standardsprache des Servers zurückgegeben.  
  
-   Beschriftung  
  
-   Qualifizierer  
  
-   SortDirection  
  
-   IsRightToLeft  
  
## <a name="example"></a>Beispiel  
 **Tabellarisch**  
  
 Die folgende XMLA-Abfrage gibt die CSDL-Darstellung des tabellarischen AdventureWorks 2012-Modellbeispiels zurück. Jede tabellarische Lösung kann nur ein Modell enthalten; PERSPECTIVE_NAME-Einschränkung kann daher leer gelassen werden. Dieses Modell enthält jedoch mehrere Perspektiven.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>AdventureWorks2012Tabular</CATALOG_NAME>  
                <PERSPECTIVE_NAME>EMPLOYEE</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
</Discover>  
  
```  
  
## <a name="example"></a>Beispiel  
 **Multidimensional**  
  
 Die folgende XMLA-Abfrage gibt die CSDLBI-Darstellungen des Contoso-Vorgangscubes zurück. Die Einschränkung der VERSION ist erforderlich, um eine mehrdimensionale Datenbank abzufragen. Die Contoso Retail-Datenbank enthält zwei Cubes. Daher wird mit der PERSPECTIVE_NAME-Einschränkung auf den Vorgangscube verwiesen.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>Contoso_Retail</CATALOG_NAME>  
                <PERSPECTIVE_NAME>Operation</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
 </Discover>  
  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Verwenden von ADOMD.NET zum Zurückgeben des Rowsets  
 Wenn Sie Metadaten mithilfe von ADOMD.NET und des Schemarowsets abrufen, können Sie entweder die GUID verwenden oder eine Referenz für ein Schemarowsetobjekt in der GetSchemaDataSet-Methode herstellen. Weitere Informationen finden Sie unter [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 Die folgende Tabelle enthält die GUID und die Zeichenfolgenwerte, die dieses Rowset identifizieren.  
  
|Argument|value|  
|--------------|-----------|  
|GUID|3444B255-171E-4cb9-AD98-19E57888A75F|  
|ADOMDNAME|Csdl|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Analysis Services-Schemarowsets](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [CSDL-Anmerkungen für Business Intelligence &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  
