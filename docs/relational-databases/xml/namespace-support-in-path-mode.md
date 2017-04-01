---
title: "Namespaceunterst&#252;tzung im PATH-Modus | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "PATH FOR XML-Modus, Namespace-Unterstützung"
  - "Namespaces [XML in SQL Server]"
ms.assetid: 5f128ea2-0ceb-4b23-bce7-c8b3fd615466
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# Namespaceunterst&#252;tzung im PATH-Modus
  Die Unterstützung von Namespaces im PATH-Modus wird durch den Einsatz von WITH NAMESPACES bereitgestellt. Beispielsweise zeigt die folgende Abfrage die Syntax von WITH NAMESPACES, um einen Namespace ("a:") zu deklarieren, der in der nachfolgenden SELECT-Anweisung verwendet werden kann:  
  
```  
WITH XMLNAMESPACES('a' as a)  
SELECT 1 as 'a:b'  
FOR XML PATH  
```  
  
## Beispiele  
 Diese Beispiele veranschaulichen die Verwendung des PATH-Modus beim Generieren von XML-Code aus einer SELECT-Abfrage. Viele dieser Abfragen beziehen sich auf die XML-Dokumente mit den Fahrradfertigungsanweisungen, die in der Instructions-Spalte der ProductModel-Tabelle gespeichert sind.  
  
## Siehe auch  
 [Verwenden des PATH-Modus mit FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  