---
title: "Hinzufügen eines Stammknotens zur JSON-Ausgabe mithilfe der ROOT-Option (SQL Server) | Microsoft-Dokumentation"
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
- ROOT (FOR JSON)
ms.assetid: b9afa74a-f59f-483e-a178-42be2e9882c9
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 58948fd1977e2094b1469ab92ac1debf0e7f4b2e
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="add-a-root-node-to-json-output-with-the-root-option-sql-server"></a>Hinzufügen eines Stammknotens zur JSON-Ausgabe mithilfe der ROOT-Option (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Um der JSON-Ausgabe der **FOR JSON** -Klausel ein einzelnes Element der obersten Ebene hinzuzufügen, geben Sie die **ROOT** -Option an.  
  
 Wenn Sie die **ROOT** -Option nicht angeben, ist in der JSON-Ausgabe kein Stammelement enthalten.  
  
## <a name="examples"></a>Beispiele  
 Die folgende Tabelle zeigt die Ausgabe der **FOR JSON** -Klausel mit und ohne die **ROOT** -Option.  
  
 Bei den Beispielen in der folgenden Tabelle wird angenommen, dass das optionale *RootName* -Argument leer ist. Wenn Sie einen Namen für das Stammelement angeben, ersetzt dieser Wert den **root** -Wert in den Beispielen.  
  
 Ohne die Option **ROOT**  
  
```json  
{  
   <<json properties>>  
}  
```  
  
```json  
[  
   <<json array elements>>  
]  
```  
  
 Mit der **ROOT** -Option  
  
```json  
{   
  "root": {  
   <<json properties>>  
 }  
}  
```  
  
```json  
{   
  "root": [  
   << json array elements >>  
  ]  
}  
```  
  
 Hier ist ein weiteres Beispiel für eine **FOR JSON** -Klausel mit der **ROOT** -Option. Dieses Beispiel gibt einen Wert für das optionale *RootName* -Argument an.  
  
 **Abfrage**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH, ROOT('info')
```  
  
 **Ergebnis**  
  
```json  
{
    "info": [{
        "Id": 1,
        "FirstName": "Ken",
        "LastName": "Sánchez",
        "Info": {
            "MiddleName": "J"
        }
    }, {
        "Id": 2,
        "FirstName": "Terri",
        "LastName": "Duffy",
        "Info": {
            "MiddleName": "Lee"
        }
    }, {
        "Id": 3,
        "FirstName": "Roberto",
        "LastName": "Tamburello"
    }, {
        "Id": 4,
        "FirstName": "Rob",
        "LastName": "Walters"
    }, {
        "Id": 5,
        "FirstName": "Gail",
        "LastName": "Erickson",
        "Info": {
            "Title": "Ms.",
            "MiddleName": "A"
        }
    }]
}
```  
  
 **Ergebnis (ohne ROOT)**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Viele spezifische Lösungen, Anwendungsfälle und Empfehlungen finden Sie in SQL Server und in der Azure SQL-Daten im [Blogbeitrag über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) von Jovan Popovic, Program Manager bei Microsoft.
 
## <a name="see-also"></a>Siehe auch  
 [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

