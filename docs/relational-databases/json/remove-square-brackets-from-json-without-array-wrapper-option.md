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
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: bf0d7645df22c9a7540650e3c7f2ca2d0db8e1cc
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>Entfernen von rechteckigen Klammern von JSON-Ausgabe mit der Option WITHOUT_ARRAY_WRAPPER
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Geben Sie zum standardmäßigen Entfernen der rechteckigen Klammern, die die JSON-Ausgabe der **FOR JSON** -Klausel umgeben, die Option **WITHOUT_ARRAY_WRAPPER** an. Verwenden Sie diese Option mit einem einzeiligen Resultat, um ein einzelnes JSON-Objekt als Ausgabe anstelle eines Arrays mit einem einzelnen Element zu generieren.

Wenn Sie diese Option mit einem mehrzeiligen Resultat verwenden, ist die resultierende Ausgabe aufgrund von mehreren Elementen und fehlenden eckigen Klammern in keinem gültigen JSON-Format.  
  
## <a name="example-single-row-result"></a>Beispiel (einzeiliges Resultat)  
Die folgende Tabelle zeigt die Ausgabe der **FOR JSON** -Klausel mit und ohne Option **WITHOUT_ARRAY_WRAPPER** an.  
  
 **Abfrage**  
  
```sql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 **Ergebnis** with the **WITHOUT_ARRAY_WRAPPER** -Option  
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 **Ergebnis** (Standard) ohne die **WITHOUT_ARRAY_WRAPPER**-Option  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  

## <a name="example-multiple-row-result"></a>Beispiel (mehrzeiliges Resultat)
Hier finden Sie ein weiteres Beispiel für eine **FOR JSON** -Klausel mit und ohne Option **WITHOUT_ARRAY_WRAPPER** an. In diesem Beispiel wird ein mehrzeiliges Resultat erzeugt. Die Ausgabe ist wegen mehrerer Elemente und fehlenden eckigen Klammern kein gültiges JSON.
  
 **Abfrage**  
  
```sql  
SELECT TOP 3 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 **Ergebnis** with the **WITHOUT_ARRAY_WRAPPER** -Option  
  
```json  
{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 **Ergebnis** (Standard) ohne die **WITHOUT_ARRAY_WRAPPER**-Option  
  
```json  
[{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Viele spezifische Lösungen, Anwendungsfälle und Empfehlungen finden Sie in SQL Server und in der Azure SQL-Daten im [Blogbeitrag über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) von Jovan Popovic, Program Manager bei Microsoft.
  
## <a name="see-also"></a>Siehe auch  
 [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

