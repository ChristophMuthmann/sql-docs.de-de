---
title: Schema-Sicherheitsüberlegungen (SQLXML 4.0) versehen | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- mapping schema [SQLXML], security
- annotated XDR schemas, security
- XDR schemas [SQLXML], security
- annotations [SQLXML]
- annotated XSD schemas, security
- SQLXML, annotated XSD schemas
- SQLXML, annotated XDR schemas
- security [SQLXML], annotated schemas
- XSD schemas [SQLXML], security
ms.assetid: 7d7e44dc-b6d3-4e0f-95c7-8f99930c94f2
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7940c1288c6bd802750d6c0cb3b76db46d85d3c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>Überlegungen zur Sicherheit von Schemas mit Anmerkungen (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Im Folgenden werden Sicherheitsrichtlinien zur Verwendung von Schemas mit Anmerkungen gegeben:  
  
-   Vermeiden Sie die Verwendung der Standardzuordnung in den Zuordnungsschemas. Die Standardzuordnung macht die Datenbankinformationen (Tabellen- und Spaltennamen) im resultierenden XML-Dokument verfügbar, da standardmäßig die Elementnamen den Tabellennamen und die Attributnamen den Spaltennamen zugeordnet werden. Daher hat jeder Benutzer, der das XML-Dokument einsehen kann, auch Zugriff auf die Tabellen- und Spalteninformationen in der Datenbank, was ein mögliches Sicherheitsrisiko bedeutet. Geben Sie daher willkürlich gewählte Element- und Attributnamen im Schema an, und verwenden Sie Anmerkungen zur expliziten Zuordnung derselben zu den Tabellen und Spalten. Auf diese Weise wird das Sicherheitsrisiko vermieden. Weitere Informationen zur Verwendung der standardzuordnung, bei der Erstellung von XSD-Schemas finden Sie unter [standardmäßige Zuordnung von XSD-Elementen und-Attributen zu Tabellen und Spalten &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md).  
  
-   Die mithilfe von Anmerkungen angegebene explizite Zuordnung macht die Datenbankinformationen (wie Tabellennamen und Spaltennamen) verfügbar. Daher werden Sie es möglicherweise vorziehen, diese Schemas nicht öffentlich verfügbar zu machen.  
  
-   Bestimmte Abfragen wie solche mit Zuordnungsschema mit Rekursion angegeben (angegeben mit **Max-Depth** Anmerkung, die auf einen höheren Wert festgelegt) kann länger dauern. Sie können optional eine Timeoutgrenze angeben, durch den Befehlstimeout-Eigenschaft (in Sekunden) festlegen. Beispiel:  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [XSD-Schemas mit Anmerkungen in SQLXML 4.0](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
