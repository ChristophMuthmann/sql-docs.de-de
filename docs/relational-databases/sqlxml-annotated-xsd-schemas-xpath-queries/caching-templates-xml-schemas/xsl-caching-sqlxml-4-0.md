---
title: XSL-Zwischenspeichern (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c14703a0156c420d072b28d726400a1331d06477
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="xsl-caching-sqlxml-40"></a>XSL-Zwischenspeichern (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Das Zwischenspeichern von XSL-Stylesheets verbessert die Leistung. Bei der ersten Ausführung bleibt ein XSL-Stylesheet im Arbeitsspeicher, wenn das XSL-Zwischenspeichern auf ON festgelegt wurde. Dies verbessert die Leistung bei der nachfolgenden Verarbeitung. Die Standardeinstellung ist ON.  
  
 Sie können die XSL-Cachegröße festlegen, indem Sie den folgenden Schlüssel in der Registrierung hinzufügen:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 Die XSL-Cachegröße sollte auf Basis des vorhandenen Arbeitsspeichers und der Anzahl der von Ihnen verwendeten XSL-Stylesheets festgelegt werden. Der Standardwert von **XSLCacheSize** lautet 31. Sie können die Cachegröße erhöhen, wenn der XSL-Zugriff langsam erscheint, oder die Cachegröße verringern, wenn der Arbeitsspeicher zu gering ist.  
  
 Für bessere Leistung wird empfohlen, dass Sie **XSLCacheSize** auf einen höheren Wert als die Anzahl der von Ihnen üblicherweise verwendeten XSL-Stylesheets festlegen. Wenn **XSLCacheSize** auf einen niedrigeren Wert als die Anzahl Ihrer XSL-Stylesheets festgelegt ist, sinkt die Leistung mit zunehmender Anzahl von XSL-Stylesheets. Der **XSLCacheSize** kann auf ein Maximum von 128 festgelegt werden.  
  
 Jedes Mal, wenn das zwischengespeicherte XSL-Stylesheet verwendet wird, wird die Änderungszeit der XSL-Datei überprüft, um festzustellen, ob sie aktualisiert werden muss. Das liegt daran, dass die Datenträgerkopie neuer als die Cachekopie ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Zwischenspeichern von Vorlagen & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [Das Zwischenspeichern von Schemas & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
  
  
