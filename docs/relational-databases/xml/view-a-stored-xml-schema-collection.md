---
title: "Anzeigen einer gespeicherten XML-Schemaauflistung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Schemaauflistungen [SQL Server], anzeigen"
  - "XML-Schemas [SQL Server], anzeigen"
  - "CREATE XML SCHEMA COLLECTION-Anweisung"
  - "xml_schema_namespace-Funktion"
  - "XML-Schemaauflistungen [SQL Server], anzeigen"
  - "Anzeigen von XML-Schemaauflistungen"
  - "Darstellen von XML-Schemaauflistungen"
ms.assetid: e38031af-22df-4cd9-a14e-e316b822f91b
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Anzeigen einer gespeicherten XML-Schemaauflistung
  Nach dem Importieren einer XML-Schemaauflistung mithilfe von [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md)werden die Schemakomponenten in den Metadaten gespeichert. Mit der systeminternen Funktion [xml_schema_namespace](../Topic/xml_schema_namespace%20\(Transact-SQL\).md) können Sie die XML-Schemaauflistung rekonstruieren. Diese Funktion gibt eine Instanz vom Datentyp **xml** zurück.  
  
 So ruft beispielsweise die folgende Abfrage eine XML-Schemaauflistung (`ProductDescriptionSchemaCollection`) aus dem relationalen Schema 'production' der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank ab.  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection')  
GO  
```  
  
 Wenn nur ein Schema der XML-Schemaauflistung angezeigt werden soll, können Sie eine XQuery-Abfrage für das Ergebnis vom Typ **xml** angeben, das von `xml_schema_namespace` zurückgegeben wird.  
  
```  
SELECT xml_schema_namespace(N'RelationalSchemaName',N'XmlSchemaCollectionName').query('  
/xs:schema[@targetNamespace="TargetNameSpace"]  
')  
GO  
```  
  
 So ruft beispielsweise die folgende Abfrage XML-Schemainformationen zur Produktgarantie und -wartung aus der XML-Schemaauflistung `ProductDescriptionSchemaCollection` ab.  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection').query('  
/xs:schema[@targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"]  
')  
GO  
```  
  
 Sie können auch den optionalen Zielnamespace als dritten Parameter an die `xml_schema_namespace` -Funktion übergeben, um ein bestimmtes Schema aus der Auflistung abzurufen, wie es in der folgenden Abfrage gezeigt wird:  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection', N'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain')  
GO  
```  
  
 Wenn Sie eine XML-Schemaauflistung mithilfe von CREATE XML SCHEMA COLLECTION in der Datenbank erstellen, speichert die Anweisung die Schemakomponenten in den Metadaten. Beachten Sie, dass nur die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpretierbaren Schemakomponenten gespeichert werden. Kommentare, Anmerkungen oder Nicht-XSD-Attribute werden nicht gespeichert. Daher ist das von **xml_schema_namespace** rekonstruierte Schema zwar hinsichtlich seiner Funktionalität mit dem ursprünglichen Schema gleichwertig, sein Erscheinungsbild jedoch nicht unbedingt identisch. Beispielsweise werden Sie die Präfixe des ursprünglichen Schemas nicht wiederfinden. Das von **xml_schema_namespace** zurückgegebene Schema verwendet **t** als Präfix für den Zielnamespace und **ns1**, **ns2** usw. für andere Namespaces.  
  
 Wenn Sie eine identische Kopie des XML-Schemas aufbewahren möchten, sollten Sie das XML-Schema in einer Datei oder in einer Datenbanktabelle in einer Spalte vom Typ **xml** speichern.  
  
 Die [sys.xml_schema_collections](../../relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql.md)-Katalogsicht gibt auch Informationen zu XML-Schemaauflistungen zurück. Zu diesen Informationen gehören der Name der Auflistung, das Erstellungsdatum und der Besitzer der Auflistung.  
  
## Siehe auch  
 [XML-Schemaauflistungen &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  