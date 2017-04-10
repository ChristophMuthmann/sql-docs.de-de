---
title: "Einschlie&#223;en von Nullwerten in die JSON-Ausgabe mit der Option INCLUDE_NULL_VALUES (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "INCLUDE_NULL_VALUES (FOR JSON)"
ms.assetid: 06873768-3778-4ed8-a1db-61758726bda0
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 13
---
# Einschlie&#223;en von Nullwerten in die JSON-Ausgabe mit der Option INCLUDE_NULL_VALUES (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Geben Sie die Option **INCLUDE_NULL_VALUES** an, um NULL-Werte in die JSON-Ausgabe einer **FOR JSON**-Klausel einzuschließen.  
  
 Wenn Sie die Option **INCLUDE_NULL_VALUES** nicht angeben, enthält die JSON-Ausgabe in den Abfrageergebnissen keine Eigenschaften für NULL-Werte.  
  
## Beispiele  
 Die folgende Tabelle zeigt die Ausgabe der **FOR JSON**-Klausel mit und ohne die Option **INCLUDE_NULL_VALUES** an.  
  
|Ohne die Option **INCLUDE_NULL_VALUES**|Mit der Option **INCLUDE_NULL_VALUES**|  
|--------------------------------------------------|-----------------------------------------------|  
|`{    "name": "John",    "surname": "Doe" }`|`{    "name": "John",    "surname": "Doe",    "age": null,    "phone": null }`|  
  
 Hier ist ein weiteres Beispiel für eine **FOR JSON**-Klausel mit der Option **INCLUDE_NULL_VALUES**.  
  
 **Abfrage**  
  
```tsql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO, INCLUDE_NULL_VALUES  
```  
  
 **Ergebnis**  
  
```json  
[   
   {"name": "John",  "surname": null },  
   {"name": "Jane",  "surname": "Doe"}  
]  
```  
  
## Siehe auch  
 [FOR-Klausel &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)  
  
  