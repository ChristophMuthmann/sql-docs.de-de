---
title: Das &lt;xsd:redefine&gt;-Element | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: acb4011d190445476a0fedfc70557cfcb5e36af5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="the-ltxsdredefinegt-element"></a>Das &lt;xsd:redefine&gt;-Element
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Das W3C XSD **redefine**-Element stellt Unterstützung zum Neudefinieren von Schemakomponenten zur Verfügung. Die Unterstützung dieser Direktive kann jedoch die Leistung beeinträchtigen und erfordert außerdem, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Instanzen des **xml** -Datentyps erneut überprüft werden, die mit dem neu definierten Schema verknüpft sind. Deshalb unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dieses Element nicht. XML-Schemas, die das **\<xsd:redefine>**-Element enthalten, werden vom Server zurückgewiesen.  
  
 Gehen Sie zum Aktualisieren des Schemas oder seiner Komponenten stattdessen folgendermaßen vor:  
  
1.  Erstellen Sie eine neue XML-Schemaauflistung mit den geänderten Schemakomponenten.  
  
2.  Ändern Sie alle **xml** -Datentypen (XML DT), welche die neu zu definierende XML-Schemaauflistung verwenden so ab, dass sie stattdessen die neue XML-Schemaauflistung verwenden. Hierzu verwenden Sie die ALTER COLUMN-Option des ALTER TABLE-Befehls, um den Spaltentyp zu ändern, oder Sie ändern die für Variablen oder Parameter geltenden Einschränkungen der XML-Schemaauflistung.  
  
3.  Löschen Sie die alte Version der XML-Schemaauflistung.  
  
## <a name="see-also"></a>Siehe auch  
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
