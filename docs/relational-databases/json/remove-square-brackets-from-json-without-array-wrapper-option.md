---
title: Entfernen von rechteckigen Klammern von JSON-Ausgabe mit der Option WITHOUT_ARRAY_WRAPPER | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WITHOUT_ARRAY_WRAPPER
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea60d5a74c680e9c2aba571a76815f77913da471
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>Entfernen von rechteckigen Klammern von JSON-Ausgabe mit der Option WITHOUT_ARRAY_WRAPPER
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Geben Sie zum Entfernen der rechteckigen Klammern, die die JSON-Ausgabe der **FOR JSON** -Klausel standardmäßig umgeben, die Option **WITHOUT_ARRAY_WRAPPER** an. Verwenden Sie diese Option, um ein einzelnes JSON-Objekt als Ausgabe anstelle eines Arrays zu generieren.  
  
 Wenn Sie diese Option nicht angeben, wird die JSON-Ausgabe in eckige Klammern eingeschlossen.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Tabelle zeigt die Ausgabe der **FOR JSON** -Klausel mit und ohne Option **WITHOUT_ARRAY_WRAPPER** an.  
  
 **Abfrage**  
  
```tsql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 **Result** with the **WITHOUT_ARRAY_WRAPPER** option  
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 **Result** without the **WITHOUT_ARRAY_WRAPPER** option  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  
  
 Hier finden Sie ein weiteres Beispiel für eine **FOR JSON** -Klausel mit und ohne Option **WITHOUT_ARRAY_WRAPPER** an.  
  
 **Abfrage**  
  
```tsql  
SELECT TOP 1 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 **Result** with the **WITHOUT_ARRAY_WRAPPER** option  
  
```json  
{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 **Result** without the **WITHOUT_ARRAY_WRAPPER** option  
  
```json  
[{
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  
  
## <a name="see-also"></a>Siehe auch  
 [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

