---
title: "JSON-Pfadausdrücke (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 67c2ee7f0e40f3630b003732c7c9e3fc8b3e5feb
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="json-path-expressions-sql-server"></a>JSON-Pfadausdrücke (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 Verwenden Sie JSON-Pfadausdrücke, um auf die Eigenschaften der JSON-Objekte zu verweisen.  
  
 Sie müssen einen Pfadausdruck angeben, wenn Sie die folgenden Funktionen aufrufen.  
  
-   Wenn Sie **OPENJSON** aufrufen, um eine relationale Sicht der JSON-Daten zu erstellen. Weitere Informationen finden Sie unter [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
-   Wenn Sie **JSON_VALUE** aufrufen, um einen Wert aus JSON-Text zu extrahieren. Weitere Informationen finden Sie unter [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
-   Wenn Sie **JSON_QUERY** aufrufen, um ein JSON-Objekt oder ein -Array zu extrahieren. Weitere Informationen finden Sie unter [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
-   Wenn Sie **JSON_MODIFY** aufrufen, um den Werte einer Eigenschaft in einer JSON-Zeichenfolge zu aktualisieren. Weitere Informationen finden Sie unter [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  

## <a name="parts-of-a-path-expression"></a>Teile eines Pfadausdrucks
 Ein Pfadausdruck hat zwei Komponenten.  
  
1.  Der optionale [PATH-Modus](#PATHMODE) mit einem Wert von **lax** oder **strict**.  
  
2.  Der [Pfad](#PATH) selbst.  

##  <a name="PATHMODE"></a> Path mode  
 Am Anfang des Pfadausdrucks können Sie optional den „path mode“ deklarieren, indem Sie das Schlüsselwort **lax** oder **strict**angeben. Der Standardwert ist **lax**.  
  
-   Im Modus **lax** gibt die Funktion leere Werte zurück, falls der Pfadausdruck einen Fehler enthält. Falls Sie beispielsweise den Wert **$.name** anfordern und der JSON-Text keinen **name**-Schlüssel enthält, gibt die Funktion NULL zurück, löst jedoch keinen Fehler aus.  
  
-   Im Modus **strict** löst die Funktion einen Fehler aus, wenn der Pfadausdruck einen Fehler enthält.  

Die folgende Abfrage gibt explizit den Modus `lax` im Pfadausdruck an.

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
  
    -   Der Punktoperator (`.`) zeigt einen Objektmember an. Beispielsweise ist `surname` in `$.people[1].surname` ein untergeordnetes Element von `people`.
  
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
  
|Pfadausdruck|value|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane", "surname": null, "active": true }|  
|$.people[1].surname|NULL|  
|$|{ „people“: [ { „name“: „John“,  „surname“: „Doe“ },<br />   { „name“: „Jane“,  „surname“: null, „active“: true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>Wie integrierte Funktionen doppelte Pfade behandeln  
 Falls der JSON-Text doppelte Eigenschaften enthält – beispielsweise zwei Schlüssel mit dem gleichen Namen auf der gleichen Stufe – geben die Funktionen **JSON_VALUE** und **JSON_QUERY** nur den ersten Wert zurück, der dem Pfad entspricht. Verwenden Sie **OPENJSON**, wie im folgenden Beispiel gezeigt, um ein JSON-Objekt zu analysieren, das doppelte Schlüssel enthält, und um alle Werte zurückzugeben.  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Weitere Informationen zu JSON in SQL Server und Azure SQL-Datenbank  
  
### <a name="microsoft-blog-posts"></a>Microsoft-Blogbeiträge  
  
Spezielle Lösungen, Anwendungsfälle und Empfehlungen finden Sie in den [Blogbeiträgen über die integrierte JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL-Server und in Azure SQL-Datenbank.  

### <a name="microsoft-videos"></a>Microsoft-Videos

Eine visuelle Einführung in die JSON-Unterstützung, die in SQL Server und Azure SQL-Datenbank integriert ist, finden Sie in den folgenden Videos:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  
