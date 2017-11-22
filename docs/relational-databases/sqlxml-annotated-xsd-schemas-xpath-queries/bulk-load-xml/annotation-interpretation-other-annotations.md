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
ms.technology: dbe-xml
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
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c66f2bb5bb89e2d8ac46fb8e6d20a8c79a49b27
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="annotation-interpretation---other-annotations"></a>Interpretation von Anmerkungen - andere Anmerkungen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Zusätzlich zu den in den vorherigen Themen in diesem Abschnitt beschriebenen Anmerkungen interpretiert XML-Massenladen diese anderen Anmerkungen folgendermaßen:  
  
 **SQL: ID-Präfix**  
 Wenn das Schema Präfixe für die XML-Daten festlegt, entfernt XML-Massenladen die Präfixe, bevor die Daten an Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gesendet werden.  
  
 **SQL: use-Cdata**  
 XML-Massenladen liest der Text, der in den CDATA gespeichert ist, Abschnitte und sendet sie an [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **SQL: URL-codieren**  
 XML-Massenladen unterstützt diese Anmerkung nicht. Eine in der XML-Dateneingabe angegebene URL wird beispielsweise von XML-Massenladen an diesem Speicherort nicht gelesen, sodass sie in der Datenbank gespeichert werden kann.  
  
 **SQL: is-Mapping-Schema**  
 XML-Massenladen unterstützt weder diese Anmerkung noch **sql:id**.  
  
> [!NOTE]  
>  XML-Massenladen unterstützt keine Inlinezuordnungsschemas.  
  
 **SQL: Key-Felder**  
 XML-Massenladen ignoriert stets diese Anmerkung.  
  
## <a name="see-also"></a>Siehe auch  
 [Interpretation von Anmerkungen &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
  
  
