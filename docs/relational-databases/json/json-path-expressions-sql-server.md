---
title: "JSON-Pfadausdrücke (SQL Server) | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 44bfd54aa494dd52174eeed8479e14a99d810af3
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="json-path-expressions-sql-server"></a>JSON-Pfadausdrücke (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Verwenden Sie JSON-pfadausdrücke, um die Eigenschaften der JSON-Objekte verweisen.  
  
 Sie müssen einen Pfadausdruck angeben, wenn Sie die folgenden Funktionen aufrufen.  
  
-   Wenn Sie **OPENJSON** aufrufen, um eine relationale Sicht der JSON-Daten zu erstellen. Weitere Informationen finden Sie unter [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
-   Wenn Sie **JSON_VALUE** aufrufen, um einen Wert aus JSON-Text zu extrahieren. Weitere Informationen finden Sie unter [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
-   Wenn Sie **JSON_QUERY** aufrufen, um ein JSON-Objekt oder ein -Array zu extrahieren. Weitere Informationen finden Sie unter [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
-   Wenn Sie **JSON_MODIFY** aufrufen, um den Werte einer Eigenschaft in einer JSON-Zeichenfolge zu aktualisieren. Weitere Informationen finden Sie unter [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  

## <a name="parts-of-a-path-expression"></a>Teile eines Pfadausdrucks
 Ein Pfadausdruck hat zwei Komponenten.  
  
1.  Das optionale [Path-Modus](#PATHMODE), mit dem Wert **lax** oder **strenge**.  
  
2.  Der [Pfad](#PATH) selbst.  

##  <a name="PATHMODE"></a> Path mode  
 Am Anfang des Pfadausdrucks können Sie optional den „path mode“ deklarieren, indem Sie das Schlüsselwort **lax** oder **strict**angeben. Der Standardwert ist **lax**.  
  
-   In **lax** Modus, gibt die Funktion leere Werte an, falls der Pfadausdruck einen Fehler enthält. Angenommen, Sie fordern, dass den Wert **$.name**, und die JSON-Text keine **Namen** Schlüssel, die Funktion gibt null zurück, aber einen Fehler wird nicht ausgelöst.  
  
-   In **strenge** -Modus die Funktion löst einen Fehler, falls der Pfadausdruck einen Fehler enthält.  

Die folgende Abfrage gibt explizit an `lax` Modus in der Path-Ausdruck.

```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{ ... }'

SELECT * FROM OPENJSON(@json, N'lax $.info')
```  
  
##  <a name="PATH"></a> Path  
 Nach der optionalen Deklaration des „path mode“ geben Sie den Pfad selbst an.  
  
-   Das Dollarzeichen (`$`) stellt das Kontextelement dar.  
  
-   Der Eigenschaftspfad ist ein Satz an Pfadschritten. Pfadschritte können die folgenden Elemente und Operatoren enthalten.  
  
    -   Schlüsselnamen. Beispielsweise `$.name` und `$."first name"`. Umschließen Sie den Namen des Schlüssels mit Anführungszeichen, falls er mit einem Dollarzeichen beginnt, oder Sonderzeichen wie z.B. Leerzeichen enthält.   
  
    -   Array-Elemente. Beispiel: `$.product[3]`. Arrays sind nullbasiert.  
  
    -   Der Punktoperator (`.`) zeigt einen Objektmember an. Beispielsweise ist in `$.people[1].surname`, `surname` ist ein untergeordnetes Element des `people`.
  
## <a name="examples"></a>Beispiele  
 Die Beispiele in diesem Abschnitt verweisen auf den folgenden JSON-Text.  
  
```json  
{
    "people": [{
        "name": "John",
        "surname": "Doe"
    }, {
        "name": "Jane",
        "surname": null,
        "active": true
    }]
}
```  
  
 Die folgende Tabelle zeigt einige Beispiele für Pfadausdrücke.  
  
|Pfadausdruck|Wert|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane", "surname": null, "active": true }|  
|$.people[1].surname|NULL|  
|$|{ „people“: [ { „name“: „John“,  „surname“: „Doe“ },<br />   { „name“: „Jane“,  „surname“: null, „active“: true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>Wie integrierte Funktionen doppelte Pfade behandeln  
 Wenn der JSON-Text doppelte Eigenschaften enthält – beispielsweise zwei mit dem gleichen Namen auf der gleichen Ebene Schlüssel – die **JSON_VALUE** und **JSON_QUERY** Funktionen zurückgeben, nur den ersten Wert, der den Pfad entspricht. Verwenden Sie zum Analysieren einer JSON-Objekt, das doppelte Schlüssel enthält, und alle Werte zurückgeben, **OPENJSON**, wie im folgenden Beispiel gezeigt.  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Für viele spezifische Lösungen Fälle und Empfehlungen zu verwenden, finden Sie unter der [Blogeinträge von jovan zur integrierten JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server und Azure SQL-Datenbank von Microsoft Program Manager Jovan Popovic.
  
## <a name="see-also"></a>Siehe auch  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  

