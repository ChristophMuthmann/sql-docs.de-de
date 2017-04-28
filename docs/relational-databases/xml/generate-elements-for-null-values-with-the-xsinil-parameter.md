---
title: Generieren von NULL-Werten mithilfe des XSINIL-Parameters | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8484894ef6b6940952920532273955359f532795
ms.lasthandoff: 04/11/2017

---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>Generieren von NULL-Werten mithilfe des XSINIL-Parameters
  Von der **ELEMENTS** -Direktive wird XML konstruiert, in der jede Spalte zu einem Element im XML-Code zugeordnet wird. Wenn der Spaltenwert NULL ist, wird kein Element hinzugefügt. Durch Angeben des optionalen Parameters **XSINIL** für die ELEMENTS-Direktive können Sie anfordern, dass auch für den NULL-Wert ein Element erstellt wird. In diesem Fall wird für ein Element das **xsi:nil** -Attribut, das auf TRUE festgelegt ist, für jeden NULL-Spaltenwert zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
