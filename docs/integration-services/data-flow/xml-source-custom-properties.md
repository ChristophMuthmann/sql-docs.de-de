---
title: Benutzerdefinierte Eigenschaften der XML-Quelle | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c37fbff21d10a7eba5ee3f1ce1df55d997379dd2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="xml-source-custom-properties"></a>Benutzerdefinierte Eigenschaften der XML-Quelle
  Die XML-Quelle verfügt sowohl über benutzerdefinierte Eigenschaften als auch über die Eigenschaften, die allen Datenflusskomponenten gemeinsam sind.  
  
 In der folgenden Tabelle werden die benutzerdefinierten Eigenschaften der XML-Quelle beschrieben. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Der zum Zugreifen auf die XML-Daten verwendete Modus.|  
|UseInlineSchema|Boolean|Ein Wert, der angibt, ob eine Inlineschemadefinition innerhalb der XML-Quelle verwendet werden soll. Der Standardwert dieser Eigenschaft ist **False**.|  
|XMLData|Zeichenfolge|Die Datei oder die Variablen, aus der bzw. denen die XML-Daten abgerufen werden sollen.<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
|XMLSchemaDefinition|Zeichenfolge|Der Pfad und der Dateiname der Schemadefinitionsdatei (.xsd).<br /><br /> Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.|  
  
 Die folgende Tabelle beschreibt die benutzerdefinierten Eigenschaften der Ausgabe der XML-Quelle. Alle Eigenschaften weisen Lese-/Schreibzugriff auf.  
  
|Eigenschaftenname|Datentyp|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|Zeichenfolge|Ein Wert, der das der Ausgabe zugeordnete Rowset identifiziert.|  
  
 Die Ausgabespalten der XML-Quelle verfügen nicht über benutzerdefinierte Eigenschaften.  
  
 Weitere Informationen finden Sie unter [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
