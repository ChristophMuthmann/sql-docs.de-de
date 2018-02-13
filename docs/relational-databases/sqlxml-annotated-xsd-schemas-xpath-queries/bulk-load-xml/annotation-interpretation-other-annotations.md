---
title: Andere Anmerkungen (SQLXML 4.0) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72a8024f46921af6b8e52222c86d89fce1c8dc7b
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="annotation-interpretation---other-annotations"></a>Interpretation von Anmerkungen - andere Anmerkungen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Neben den in den vorherigen Themen in diesem Abschnitt beschriebenen Anmerkungen interpretiert XML-Massenladen diese anderen Anmerkungen folgendermaßen:  
  
 **sql:id-prefix**  
 Wenn das Schema Präfixe für die XML-Daten festlegt, entfernt XML-Massenladen die Präfixe, bevor die Daten an Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gesendet werden.  
  
 **sql:use-cdata**  
 XML-Massenladen liest der Text, der in den CDATA gespeichert ist, Abschnitte und sendet sie an [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **sql:url-encode**  
 XML-Massenladen unterstützt diese Anmerkung nicht. Eine in der XML-Dateneingabe angegebene URL wird beispielsweise von XML-Massenladen an diesem Speicherort nicht gelesen, sodass sie in der Datenbank gespeichert werden kann.  
  
 **sql:is-mapping-schema**  
 XML-Massenladen unterstützt weder diese Anmerkung noch **sql:id**.  
  
> [!NOTE]  
>  XML-Massenladen unterstützt keine Inlinezuordnungsschemas.  
  
 **sql:key-fields**  
 XML-Massenladen ignoriert stets diese Anmerkung.  
  
## <a name="see-also"></a>Siehe auch  
 [Interpretation von Anmerkungen &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
  
  
