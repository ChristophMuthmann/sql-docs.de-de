---
title: Arbeiten mit Schemarowsets in ADOMD.NET | Microsoft Docs
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- metadata [ADOMD.NET]
- retrieving metadata
- schema rowsets [ADOMD.NET]
ms.assetid: 7bf75bf8-f1e1-44f6-ac42-c38a681654cf
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 279cc537776f6c96193026d5f0bccafcbd8f0c8b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="retrieving-metadata---working-with-schema-rowsets"></a>Beim Abrufen der Metadaten - arbeiten mit Schemarowsets
  Wenn Sie mehr als die im ADOMD.NET-Objektmodell vorhandenen Metadaten benötigen, bietet ADOMD.NET die Möglichkeit, den vollständigen Bereich für XMLA-(XML for Analysis-), OLE DB-, OLE DB für OLAP- und OLE DB für Data Mining-Schemarowsets abzurufen:  
  
 **XML for Analysis-Metadaten**  
 Die XML for Analysis-Schemarowsets stellen eine Methode zum Abrufen von Informationen über den Server auf niedriger Ebene bereit. Zu den verfügbaren Informationen gehören die auf dem Server vorhandenen Datenquellen, die durch den Anbieter reservierten Schlüsselwörter, die vom Anbieter unterstützten Literale und vieles mehr. Sie können ein XML for Analysis-Schemarowset verwenden, um alle Schemarowsets zu ermitteln, die vom Anbieter unterstützt werden.  
  
 Weitere Informationen: [XML for Analysis-Schemarowsets](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 **OLE DB metadata**  
 Die OLE DB-Schemarowsets stellen eine Methode nach Industriestandard für das Abrufen von Informationen von diversen Anbietern bereit.  
  
 Weitere Informationen: [OLE DB-Schemarowsets](../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
 **OLAP metadata**  
 Zu den Schemainformationen, die für eine analytische Datenquelle bereitgestellt werden, gehören die über die analytische Datenquelle verfügbaren Datenbanken und Kataloge, Cubes und Miningmodelle in einer Datenbank, für Cubes in der Datenbank bestehende Rollen und vieles mehr.  
  
 Weitere Informationen: [OLE DB für OLAP-Schemarowsets](../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
 **Datamining-Metadaten**  
 Zusätzlich zu OLAP-Metadaten können Data Mining-Metadaten mittels Schemarowsets abgerufen werden. Die verfügbaren Rowsets machen Informationen über die verfügbaren Data Mining-Modelle in der Datenbank, die verfügbaren Mining-Algorithmen, die für den Algorithmus erforderlichen Parameter, Miningstrukturen und vieles mehr verfügbar.  
  
 Weitere Informationen: [Data Mining-Schemarowsets](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 Für jeden dieser verschiedenen Schemarowsets rufen Sie Metadaten vom Rowset durch die Übergabe eines GUID oder XMLA-Namens mit der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>-Methode des <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>-Objekts ab.  
  
## <a name="retrieving-metadata-by-passing-guids"></a>Abrufen von Metadaten durch Übergabe von GUIDS  
 Die <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> Klasse enthält eine Liste von Feldern, die die Schemarowsets, die am häufigsten von Anbietern und analytischen Datenquellen unterstützt darstellen. Um sowohl allgemeine als auch anbieterspezifische Metadaten von einem Anbieter oder einer analytischen Datenquelle abzurufen, verwenden Sie die GUIDs, die als Bestandteil der <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> Objekt mit einer der folgenden Methoden:  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
> [!NOTE]  
>  Der ADOMD.NET-Datenanbieter macht Schemainformationen über eine Funktionalität verfügbar, die Ihr spezifischer Anbieter und die analytische Datenquelle bereitstellen. Jeder Anbieter und jede Datenquelle stellen möglicherweise andere Metadaten bereit.  
  
## <a name="retrieving-metadata-by-passing-xmla-names"></a>Abrufen von Metadaten durch Übergabe von XMLA-Namen  
 Die folgenden Methoden nutzen als Argumente den XMLA-Schemanamen, der identifiziert, welche Schemainformationen zurückzugeben sind, und einen Array von Einschränkungen in diesen zurückgegebenen Spalten:  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
 Jede dieser Methoden gibt eine Instanz eines **DataSet** -Objekts zurück, die mit den Schemainformationen aufgefüllt wird. Das **DataSet** -Objekt stammt aus dem **System.Data** -Namespace der Microsoft .NET Framework-Klassenbibliothek.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden die Funktion GetActions nimmt eine Verbindung, den Cubenamen, eine Koordinate und einen Koordinatentyp, ruft eine [MDSCHEMA_ACTIONS-Rowsets](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md), und gibt die verfügbaren Aktionen auf der ausgewählten Koordinate.  
  
 [!code-cs[Adomd.NetClient#GetActions](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-metadata-work_0_1.cs)]  
  
## <a name="see-also"></a>Siehe auch  
 [Abrufen von Metadaten aus einer analytischen Datenquelle](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  
