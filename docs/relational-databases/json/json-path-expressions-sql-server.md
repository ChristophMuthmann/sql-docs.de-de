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
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 829f7d57569e55eed5bc50634c5a9baad6f7d8ee
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="json-path-expressions-sql-server"></a>JSON-Pfadausdrücke (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Verwenden Sie JSON-Pfade, um auf die Eigenschaften der JSON-Objekte zu verweisen. JSON-Pfade verwenden eine Syntax, die der von Javascript ähnlich ist.  
  
 Sie müssen einen Pfadausdruck angeben, wenn Sie die folgenden Funktionen aufrufen.  
  
-   Wenn Sie **OPENJSON** aufrufen, um eine relationale Sicht der JSON-Daten zu erstellen. Weitere Informationen finden Sie unter [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
-   Wenn Sie **JSON_VALUE** aufrufen, um einen Wert aus JSON-Text zu extrahieren. Weitere Informationen finden Sie unter [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
-   Wenn Sie **JSON_QUERY** aufrufen, um ein JSON-Objekt oder ein -Array zu extrahieren. Weitere Informationen finden Sie unter [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
-   Wenn Sie **JSON_MODIFY** aufrufen, um den Werte einer Eigenschaft in einer JSON-Zeichenfolge zu aktualisieren. Weitere Informationen finden Sie unter [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  

## <a name="parts-of-a-path-expression"></a>Teile eines Pfadausdrucks
 Ein Pfadausdruck hat zwei Komponenten.  
  
1.  Der optionale [PATH-Modus](#PATHMODE), **lax** oder **strict**.  
  
2.  Der [Pfad](#PATH) selbst.  
  
##  <a name="PATHMODE"></a> Path mode  
 Am Anfang des Pfadausdrucks können Sie optional den „path mode“ deklarieren, indem Sie das Schlüsselwort **lax** oder **strict**angeben. Der Standardwert ist **lax**.  
  
-   Im Modus **lax** geben die Funktionen leere Werte zurück, falls der Pfadausdruck einen Fehler enthält. Falls Sie beispielsweise den Wert **$.name**anfordern und der JSON-Text keinen **name** -Schlüssel enthält, gibt die Funktion NULL zurück.  
  
-   Im Modus **strict** lösen die Funktionen Fehler aus, falls der Pfadausdruck einen Fehler enthält.  
  
##  <a name="PATH"></a> Path  
 Nach der optionalen Deklaration des „path mode“ geben Sie den Pfad selbst an.  
  
-   Das Dollarzeichen (`$`) stellt das Kontextelement dar.  
  
-   Der Eigenschaftspfad ist ein Satz an Pfadschritten. Pfadschritte können die folgenden Elemente und Operatoren enthalten.  
  
    -   Schlüsselnamen. Beispielsweise `$.name` und `$."first name"`. Umschließen Sie den Namen des Schlüssels mit Anführungszeichen, falls er mit einem Dollarzeichen beginnt, oder Sonderzeichen wie z.B. Leerzeichen enthält.   
  
    -   Array-Elemente. Beispiel: `$.product[3]`. Arrays sind nullbasiert.  
  
    -   Der Punktoperator (`.`) zeigt einen Objektmember an.  
  
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
 Falls der JSON-Text doppelte Eigenschaften enthält – beispielsweise zwei Schlüssel mit dem gleichen Namen auf der gleichen Stufe – geben die Funktionen JSON_VALUE und JSON_QUERY den ersten Wert zurück, der dem Pfad entspricht. Verwenden Sie OPENJSON, wie im folgenden Beispiel gezeigt, um ein JSON-Objekt zu analysieren, das doppelte Schlüssel enthält.  
  
```tsql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  
  
## <a name="see-also"></a>Siehe auch  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  

