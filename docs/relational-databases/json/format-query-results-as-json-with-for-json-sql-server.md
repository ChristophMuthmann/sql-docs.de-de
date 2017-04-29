---
title: Formatieren von Abfrageergebnisse als JSON mit FOR JSON (SQL Server) | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c439a76e3e925d00e88adaaefa616e59f8529a40
ms.lasthandoff: 04/11/2017

---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>Formatieren von Abfrageergebnisse als JSON mit FOR JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Formatieren Sie Abfrageergebnisse als JSON, oder exportieren Sie Daten aus SQL Server als JSON, indem Sie die **FOR JSON**-Klausel einer **SELECT**-Anweisung hinzufügen. Verwenden Sie die **FOR JSON**-Klausel, um die Formatierung der JSON-Ausgabe von Clientanwendungen an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu delegieren.
  
 Bei Verwendung der **FOR JSON** -Klausel, können Sie die Struktur der Ausgabe explizit angeben, oder lassen Sie die Struktur der SELECT-Anweisung die Ausgabe bestimmen.  
  
-   Verwenden Sie den **PATH**-Modus mit der **FOR JSON**-Klausel, um die vollständige Kontrolle über das Format der JSON-Ausgabe beizubehalten. Sie können Wrapper-Objekte erstellen und komplexe Eigenschaften schachteln.  
  
-   Verwenden Sie den **AUTO**-Modus mit der **FOR JSON**-Klausel, um die JSON-Ausgabe entsprechend der Struktur der SELECT-Anweisung zu formatieren.  
  
Hier finden Sie ein Beispiel für eine **SELECT**-Anweisung mit der **FOR JSON**-Klausel und deren Ausgabe.
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png "FOR JSON")  
  
## <a name="maintain-control-over-json-output-with-path-mode"></a>Behalten der Kontrolle über die JSON-Ausgabe mit dem PATH-Modus  
Im **PATH** -Modus können Sie die Punktsyntax verwenden, z.B. `'Item.Price'` , um geschachtelte Ausgaben zu formatieren. Im folgenden Beispiel wird auch die Option **ROOT** verwendet, um ein benanntes Stammelement anzugeben.  

Hier ist eine Beispielabfrage, die den **PATH** -Modus mit der **FOR JSON** -Klausel verwendet.
  
 ![Flussdiagramm der FOR JSON-Ausgabe](../../relational-databases/json/media/forjson-example1.png "Diagram of flow of FOR JSON output")  

### <a name="more-info"></a>Weitere Informationen
Weitere Informationen und Beispiele finden Sie unter [Formatieren einer geschachtelten JSON-Ausgabe im PATH-Modus &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).

Weitere Informationen zu Syntax und Verwendung finden Sie unter [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  

## <a name="let-the-select-statement-control-json-output-with-auto-mode"></a>Lassen Sie die SELECT-Anweisung die JSON-Ausgabe im AUTO-Modus kontrollieren  
Im **AUTO** -Modus bestimmt die Struktur der SELECT-Anweisung das Format der JSON-Ausgabe. **Nullwerte** sind standardmäßig nicht in der Ausgabe enthalten. Sie können **INCLUDE_NULL_VALUES** dazu verwenden, dieses Verhalten zu ändern.  

Hier ist eine Beispielabfrage, die den **AUTO** -Modus mit der **FOR JSON** -Klausel verwendet.
 
**Abfrage:**  
  
```tsql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO  
```  
  
 **Ergebnisse**  
  
```json  
[{
    "name": "John"
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```  
### <a name="more-info"></a>Weitere Informationen
Weitere Informationen und Beispiele finden Sie unter [Automatisches Formatieren von JSON-Ausgaben &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).

Weitere Informationen zu Syntax und Verwendung finden Sie unter [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  
  
## <a name="control-other-json-output-options"></a>Steuern der Ausgabe anderer JSON-Ausgabeoptionen  
 Steuern Sie die Ausgabe der **FOR JSON** -Klausel, indem Sie die folgenden Optionen verwenden.  
  
-   Geben Sie die Option **ROOT** an, um der JSON-Ausgabe ein einzelnes Element der obersten Ebene hinzuzufügen. Wenn Sie die Option **ROOT** nicht angeben, besitzt die JSON-Ausgabe kein Stammelement. Weitere Informationen finden Sie unter [Add a Root Node to JSON Output with the ROOT Option &#40;SQL Server&#41; (Hinzufügen eines Stammknotens zur JSON-Ausgabe mithilfe der ROOT-Option (SQL Server))](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
-   Geben Sie die Option **INCLUDE_NULL_VALUES** an, um NULL-Werte in die JSON-Ausgabe einzuschließen. Wenn Sie diese Option nicht angeben, enthält die Ausgabe in den Abfrageergebnissen keine JSON-Eigenschaften für NULL-Werte. Weitere Informationen finden Sie unter[Include Null Values in JSON Output with the INCLUDE_NULL_VALUES Option &#40;SQL Server&#41; (Einschließen von Nullwerten in die JSON-Ausgabe mit der Option INCLUDE_NULL_VALUES (SQL Server))](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).   

-   Geben Sie zum standardmäßigen Entfernen der rechteckigen Klammern, die die JSON-Ausgabe der **FOR JSON** -Klausel umgeben, die Option **WITHOUT_ARRAY_WRAPPER** an. Verwenden Sie diese Option, um ein einzelnes JSON-Objekt als Ausgabe zu generieren. Wenn Sie diese Option nicht angeben, wird die JSON-Ausgabe in eckige Klammern eingeschlossen. Weitere Informationen finden Sie unter [Remove Square Brackets from JSON Output with the WITHOUT_ARRAY_WRAPPER Option &#40;SQL Server&#41; (Entfernen von rechteckigen Klammern von JSON-Ausgabe mit der Option WITHOUT_ARRAY_WRAPPER (SQL Server))](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md). 
   
## <a name="output-of-the-for-json-clause"></a>Ausgabe der FOR JSON-Klausel  
 Die Ausgabe der **FOR JSON** -Klausel besitzt die folgenden Eigenschaften.  
  
1.  Das Resultset enthält eine einzelne Spalte. Ein kleines Resultset kann eine einzelne Zeile enthalten. Ein großes Resultset enthält mehrere Zeilen.  
  
     ![Beispiel für JSON-Ausgabe](../../relational-databases/json/media/forjson-example2.png "Example of FOR JSON output")  
  
2.  Die Ergebnisse werden als Array von JSON-Objekten formatiert.  
  
    -   Die Anzahl der Elemente im Array entspricht der Anzahl der Zeilen in den Ergebnissen.  
  
    -   Jede Zeile im Resultset wird zu einem separaten JSON-Objekt im Array.  
  
    -   Jede Spalte im Resultset wird zu einer Eigenschaft des JSON-Objekts.  
  
3.  Sowohl die Namen der Spalten als auch deren Werte werden entsprechend der JSON-Syntax geschützt. Weitere Informationen finden Sie unter [How FOR JSON escapes special characters and control characters &#40;SQL Server&#41; (So maskiert FOR JSON Sonderzeichen und Steuerzeichen (SQL Server))](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md).
  
 Hier ist ein Beispiel, das die Formatierung der JSON-Ausgabe veranschaulicht.  
  
 **Abfrageergebnisse**  
  
|||||  
|-|-|-|-|  
|**A**|**B**|**C**|**D**|  
|10|11|12|X|  
|20|21|22|J|  
|30|31|32|Z|  
  
 **JSON-Ausgabe**  
  
```json  
[{
    "A": 10,
    "B": 11,
    "C": 12,
    "D": "X"
}, {
    "A": 20,
    "B": 21,
    "C": 22,
    "D": "Y"
}, {
    "A": 30,
    "B": 31,
    "C": 32,
    "D": "Z"
}] 
```  
 Weitere Informationen darüber, was Sie in der Ausgabe der **FOR JSON**-Klausel sehen, finden Sie in den folgenden Themen.  
-   [How FOR JSON converts SQL Server data types to JSON data types &#40;SQL Server&#41; (So konvertiert FOR JSON SQL Server-Datentypen in JSON-Datentypen (SQL Server))](../../relational-databases/json/how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server.md)  
Die **FOR JSON** -Klausel verwendet die in diesem Thema beschriebenen Regeln, um SQL-Datentypen in JSON-Typen in der JSON-Ausgabe zu konvertieren.  

-   [How FOR JSON escapes special characters and control characters &#40;SQL Server&#41; (So maskiert FOR JSON Sonderzeichen und Steuerzeichen (SQL Server))](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)  
 Die **FOR JSON** -Klausel maskiert Sonderzeichen und stellt die Steuerzeichen in der JSON-Ausgabe dar, wie in diesem Thema beschrieben.  

## <a name="learn-more-about-for-json-and-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über FOR JSON und integrierte JSON-Unterstützung in SQL Server  
 [Blogeinträge von Jovan Popovic, Program Manager bei Microsoft](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## <a name="see-also"></a>Siehe auch  
 [FOR-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [Use FOR JSON output in SQL Server and in client apps &#40;SQL Server&#41; (Verwenden der FOR JSON-Ausgabe in SQL Server und Client-Apps (SQL Server))](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  

