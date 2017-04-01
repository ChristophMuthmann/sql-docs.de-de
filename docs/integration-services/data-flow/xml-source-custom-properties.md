---
title: "Benutzerdefinierte Eigenschaften der XML-Quelle | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Benutzerdefinierte Eigenschaften der XML-Quelle
  Die XML-Quelle verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften der XML-Quelle beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftsname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Der zum Zugreifen auf die XML-Daten verwendete Modus.|  
|UseInlineSchema|Boolean|Ein Wert, der angibt, ob eine Inlineschemadefinition innerhalb der XML-Quelle verwendet werden soll. Der Standardwert dieser Eigenschaft ist **False**.|  
|XMLData|String|Die Datei oder die Variablen, aus der bzw. denen die XML-Daten abgerufen werden sollen.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
|XMLSchemaDefinition|String|Der Pfad und der Dateiname der Schemadefinitionsdatei (.xsd).<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabe der XML-Quelle. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftsname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|String|Ein Wert, der das der Ausgabe zugeordnete Rowset identifiziert.|  
  
 Die Ausgabespalten der XML-Quelle verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## Siehe auch  
 [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
  