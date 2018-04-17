---
title: Zwischenspeichern von Vorlagen, XSL und Schemas (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5290641e6f7de49419e7a36ebc9e04abca75e1b5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>Zwischenspeichern von Vorlagen, XSL und Schemas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um die Leistung zu verbessern, unterstützt [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 das Zwischenspeichern von Vorlagen, XSL und Schemas.  
  
 Alle Schemas, Vorlagen und XSL-Dateien (außer den Dateien von einem http://- oder ftp://-Speicherort) werden zwischengespeichert. Die zwischengespeicherten Dateien bleiben im Arbeitsspeicher, während der Prozess ausgeführt wird. Wenn der Prozess beendet wird, geht der gesamte Cacheinhalt verloren. Wenn Sie nur einen Prozess pro Abfrage ausführen, ist der Vorteil der Zwischenspeicherung möglicherweise nicht erkennbar.  
  
 Die Themen in diesem Abschnitt liefern weitere Informationen über das Zwischenspeichern:  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Zwischenspeichern von Vorlagen &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)  
 Beschreibt einen Registrierungsschlüssel zum Zwischenspeichern von Vorlagen und stellt ihn bereit.  
  
 [XSL-Zwischenspeichern & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
 Beschreibt einen Registrierungsschlüssel zum Zwischenspeichern von XSL und stellt ihn bereit.  
  
 [Das Zwischenspeichern von Schemas & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
 Erläutert Probleme der parallelen Installation in SQLXML, die beim Zwischenspeichern von Schemas auftreten können, und stellt Registrierungsschlüssel für das Zwischenspeichern von Schemas bereit.  
  
  
