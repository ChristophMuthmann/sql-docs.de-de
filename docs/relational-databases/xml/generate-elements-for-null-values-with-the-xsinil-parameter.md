---
title: "Generieren von NULL-Werten mithilfe des XSINIL-Parameters | Microsoft Docs"
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
  - "FOR XML-Klausel, NULL-Werte"
  - "NULL-Werte [SQL Server], XML"
  - "ELEMENTS-Direktive"
  - "XSINIL-Parameter"
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Generieren von NULL-Werten mithilfe des XSINIL-Parameters
  Von der **ELEMENTS** -Direktive wird XML konstruiert, in der jede Spalte zu einem Element im XML-Code zugeordnet wird. Wenn der Spaltenwert NULL ist, wird kein Element hinzugefügt. Durch Angeben des optionalen Parameters **XSINIL** für die ELEMENTS-Direktive können Sie anfordern, dass auch für den NULL-Wert ein Element erstellt wird. In diesem Fall wird für ein Element das **xsi:nil** -Attribut, das auf TRUE festgelegt ist, für jeden NULL-Spaltenwert zurückgegeben.  
  
## Siehe auch  
 [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  