---
title: Schema-Zwischenspeichern (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ebb2fd4b7e0b17f81f8e14f3bde60d56e3a60ff3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="schema-caching-sqlxml-40"></a>Zwischenspeichern von Schemas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Bei einer Seite-an-Seite Installation des XML-Codes für Microsoft SQL Server 2000 Web Release 1, Microsoft SQLXML 2.0 und SQLXML 3.0 können Sie explizit die in allen Versionen mit dem folgenden Registrierungsschlüssel Zwischenspeichern von Schemas steuern:  
  
 Web Release 1:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 Weitere Informationen zur Seite-an-Seite-Installation finden Sie unter [Neuigkeiten in SQLXML 4.0 SP1](../../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 Das Zwischenspeichern von Schemas verbessert die Leistung einer XPath-Abfrage deutlich. Wenn eine XPath-Abfrage für ein Zuordnungsschema ausgeführt wird, wird das Schema im Arbeitsspeicher gespeichert und werden die notwendigen Datenstrukturen im Arbeitsspeicher erstellt. Wenn das Zwischenspeichern von Schemas festgelegt ist, bleibt das Schema im Arbeitsspeicher und verbessert dadurch die Leistung für nachfolgende XPath-Abfragen.  
  
 Sie können die Größe des Schemacache durch Hinzufügen des oben angegebenen Schlüssels in der Registrierung hinzufügen.  
  
 Die Schemagröße wird basierend auf dem zur Verfügung stehenden Arbeitsspeicher und der Anzahl von Schemas festgelegt, die Sie verwenden. Die Standardeinstellung **SchemaCacheSize** lautet 31. Wenn Sie festlegen, **SchemaCacheSize** höher mehr Arbeitsspeicher verwendet. Sie können somit die Cachegröße erhöhen, wenn der Schemazugriff langsam erscheint, oder die Cachegröße verringern, wenn der Arbeitsspeicher zu gering ist.  
  
 Aus Leistungsgründen wird empfohlen, dass Sie festlegen, **SchemaCacheSize** höher als die Anzahl der von Ihnen üblicherweise verwendeten Zuordnungsschemas. Die Anzahl von Schemas, wenn erhöhen **SchemaCacheSize** ist kleiner als die Anzahl von Schemas stehen Ihnen, die Leistung beeinträchtigt wird.  
  
> [!NOTE]  
>  Während der Entwicklung empfiehlt es sich, die Schemas nicht zwischenzuspeichern, da Änderungen an den Schemas im Zwischenspeicher erst nach zwei Minuten enthalten sind.  
  
## <a name="see-also"></a>Siehe auch  
 [Zwischenspeichern von Vorlagen & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [XSL-Zwischenspeichern & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
