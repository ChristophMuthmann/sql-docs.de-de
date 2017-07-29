---
title: "Lösen häufiger Probleme mit JSON in SQL Server | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, FAQ
ms.assetid: feae120b-55cc-4601-a811-278ef1c551f9
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 94435e9fb466887a00c8d22076f229481a83f280
ms.contentlocale: de-de
ms.lasthandoff: 06/23/2017

---
# <a name="solve-common-issues-with-json-in-sql-server"></a>Lösen häufiger Probleme mit JSON in SQL Server
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 Hier finden Sie Antworten auf einige häufig gestellte Fragen zu der integrierten JSON-Unterstützung in SQL Server.  
 
## <a name="for-json-and-json-output"></a>FOR JSON- und JSON-Ausgabe

### <a name="for-json-path-or-for-json-auto"></a>FOR JSON PATH oder FOR JSON AUTO?  
 **Frage:** Ich möchte eine JSON-Textergebnis aus einer einfachen SQL-Abfrage für eine einzelne Tabelle zu erstellen. FOR JSON PATH und FOR JSON AUTO erzeugen dieselbe Ausgabe. Welche dieser beiden Optionen sollte ich verwenden?  
  
 **Antwort:** Verwenden Sie FOR JSON PATH. Obwohl es kein Unterschied in der JSON-Ausgabe besteht, gilt die AUTO-Modus zusätzliche Logik, die überprüft, ob Spalten geschachtelt werden sollen. Betrachten Sie PATH als Standardoption.  

### <a name="create-a-nested-json-structure"></a>Erstellen einer geschachtelten JSON-Struktur  
 **Frage:** Ich möchte mit mehreren Arrays auf der gleichen Ebene komplexe JSON-Objekte erstellen. FOR JSON PATH kann geschachtelter Objekte mithilfe von Pfaden erstellen.FOR JSON AUTO erstellt eine zusätzliche Schachtelungsebene für jede Tabelle. Weder eine dieser beiden Optionen kann ich die Ausgabe zu generieren, ich möchte. Wie kann ich ein benutzerdefiniertes JSON-Format erstellen, das die vorhandenen Optionen nicht direkt unterstützen?  
  
 **Antwort:** Sie können eine beliebige Datenstruktur erstellen, indem Sie FOR JSON-Abfragen als Spaltenausdrücke, die JSON-Text zurückgeben hinzufügen. Sie können JSON auch manuell erstellen, mithilfe der JSON_QUERY-Funktion. Die im folgende Beispiel veranschaulicht diese Techniken.  
  
```sql  
SELECT col1, col2, col3,  
     (SELECT col11, col12, col13 FROM t11 WHERE t11.FK = t1.PK FOR JSON PATH) as t11,  
     (SELECT col21, col22, col23 FROM t21 WHERE t21.FK = t1.PK FOR JSON PATH) as t21,  
     (SELECT col31, col32, col33 FROM t31 WHERE t31.FK = t1.PK FOR JSON PATH) as t31,  
     JSON_QUERY('{"'+col4'":"'+col5+'"}' as t41  
FROM t1  
FOR JSON PATH  
```  
  
Jedes Ergebnis einer FOR JSON-Abfrage oder die Funktion JSON_QUERY in den Spaltenausdrücken wird als separates geschachteltes JSON-Unterobjekt formatiert und im Hauptergebnis aufgenommen.  

### <a name="prevent-double-escaped-json-in-for-json-output"></a>Verhindern von doppelt geschütztem JSON in der FOR JSON-Ausgabe  
 **Frage:** Ich habe einen JSON-Text, der in einer Tabellenspalte gespeichert ist. Ich möchte ihn in der Ausgabe von FOR JSON einschließen. Aber FOR JSON schützt alle Zeichen in JSON, damit ich eine JSON-Zeichenfolge anstelle eines geschachtelten-Objekts, erhalte, wie im folgenden Beispiel gezeigt.  
  
```sql  
SELECT 'Text' AS myText, '{"day":23}' AS myJson  
FOR JSON PATH  
```  
  
 Diese Abfrage generiert die folgende Ausgabe:  
  
```json  
[{"myText":"Text", "myJson":"{\"day\":23}"}]  
```  
  
 Wie kann ich verhindern, dass dieses Verhalten auftritt? Ich möchte, dass `{"day":23}` als JSON-Objekt und nicht als geschützter Text zurückgegeben wird.  
  
 **Antwort:** Ein JSON-Objekt, das in einer Textspalte oder als Literal gespeichert wird, wird wie jeder beliebige Text behandelt. Es besitzt, also in doppelte Anführungszeichen eingeschlossen und mit einem Escapezeichen versehen. Wenn ein ungeschütztes JSON-Objekt zurückgegeben werden soll, übergeben Sie die JSON-Spalte als Argument an die Funktion JSON_QUERY, wie im folgenden Beispiel gezeigt.  
  
```sql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 JSON_QUERY ohne den optionalen zweiten Parameter gibt nur das erste Argument als Ergebnis zurück. Da JSON_QUERY immer gültige JSON zurückgibt, weiß FOR JSON, dass dieses Ergebnis nicht mit Escapezeichen versehen werden.

### <a name="json-generated-with-the-withoutarraywrapper-clause-is-escaped-in-for-json-output"></a>Ein mit der WITHOUT_ARRAY_WRAPPER-Klausel generiertes JSON wird in der FOR JSON-Ausgabe geschützt  
 **Frage:** Ich versuche, einen Spaltenausdruck mit FOR JSON und der Option WITHOUT_ARRAY_WRAPPER zu formatieren.  
  
```sql  
SELECT 'Text' as myText,  
   (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 Es scheint, dass der von der FOR JSON-Abfrage zurückgegebene Text als Klartext geschützt wird. Dies geschieht nur, wenn WITHOUT_ARRAY_WRAPPER angegeben wird. Warum wird es nicht als ein JSON-Objekt behandelt und im Ergebnis ungeschützt eingefügt?  
  
 **Antwort:** Bei Angabe der `WITHOUT_ARRAY_WRAPPER` -Option in der inneren `FOR JSON`, die resultierenden JSON-Text ist nicht notwendigerweise gültiges JSON-Format. Aus diesem Grund die äußere `FOR JSON` wird davon ausgegangen, dass dies um Klartext handelt und die Zeichenfolge schützt. Wenn Sie sicher sind, dass die JSON output gültig ist, binden Sie diese mit der `JSON_QUERY` Funktion, um ihn ordnungsgemäß höher stufen JSON formatiert, wie im folgenden Beispiel gezeigt.  
  
```sql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## <a name="openjson-and-json-input"></a>OPENJSON und JSON-Eingabe

### <a name="return-a-nested-json-sub-object-from-json-text-with-openjson"></a>Zurückgeben eines geschachtelten untergeordneten JSON-Objekts aus dem JSON-Text mit OPENJSON  
 **Frage:** Das sowohl skalare Werte als auch Objekte und arrays enthält, verwenden OPENJSON mit einem expliziten Schema ein Array komplexer JSON-Objekte kann nicht geöffnet werden. Wenn ich auf einen Schlüssel in der WITH-Klausel verweise, werden nur skalare Werte zurückgegeben. Objekte und Arrays werden als NULL-Werte zurückgegeben. Wie kann ich Objekte oder Arrays als JSON-Objekten extrahieren?  
  
 **Antwort:** Wenn Sie ein Objekt oder ein Array als eine Spalte zurückgeben möchten, verwenden Sie die Option AS JSON in der Spaltendefinition, wie im folgenden Beispiel gezeigt.  
  
```sql  
SELECT scalar1, scalar2, obj1, obj2, arr1  
FROM OPENJSON(@json)  
    WITH ( scalar1 int,  
        scalar2 datetime2,  
        obj1 NVARCHAR(MAX) AS JSON,  
        obj2 NVARCHAR(MAX) AS JSON,  
        arr1 NVARCHAR(MAX) AS JSON)  
```  

### <a name="return-long-text-value-with-openjson-instead-of-jsonvalue"></a>Rückgabewert langer Text mit OPENJSON anstelle von JSON_VALUE
 **Frage:** Ich habe einen Beschreibungsschlüssel im JSON-Text, der langen Text enthält. `JSON_VALUE(@json, '$.description')` gibt NULL zurück, statt eines Werts.  
  
 **Antwort:** JSON_VALUE ist dafür konzipiert, kleine skalare Werte zurückzugeben. Im Allgemeinen gibt die Funktion NULL zurück, statt eines Überlauffehlers. Wenn längere Werte zurückgegeben werden sollen, verwenden Sie OPENJSON, das NVARCHAR(MAX)-Werte unterstützt, wie im folgenden Beispiel gezeigt.  
  
```sql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### <a name="handle-duplicate-keys-with-openjson-instead-of-jsonvalue"></a>Mit OPENJSON anstelle von JSON_VALUE mit doppelten Schlüsseln umgehen
 **Frage:** Ich habe doppelte Schlüssel im JSON-Text. JSON_VALUE gibt nur den ersten Schlüssel zurück, der im Pfad gefunden wird. Wie kann ich alle Schlüssel zurückgeben, die den gleichen Namen haben?  
  
 **Antwort:** Die integrierten Skalarfunktionen von JSON zurückgeben, nur das erste Vorkommen des Objekts, auf die verwiesen wird. Wenn Sie mehr als einen Schlüssel benötigen, verwenden Sie die OPENJSON-Tabellenwertfunktion, wie im folgenden Beispiel gezeigt.  
  
```sql  
SELECT value FROM OPENJSON(@json, '$.info.settings')  
WHERE [key] = 'color'  
```  

### <a name="openjson-requires-compatibility-level-130"></a>OPENJSON erfordert Kompatibilitätsgrad 130  
 **Frage:** Ich versuche, OPENJSON in SQL Server 2016 auszuführen, und erhalte die folgende Fehlermeldung.  
  
 `Msg 208, Level 16, State 1 ‘Invalid object name OPENJSON’`  
  
 **Antwort:** Die OPENJSON-Funktion steht nur für Kompatibilitätsgrad 130 zur Verfügung. Wenn der Kompatibilitätsgrad Ihrer DB kleiner als 130 ist, wird OPENJSON ausgeblendet. Andere JSON-Funktionen sind für alle Kompatibilitätsgrade verfügbar.  
 
## <a name="other-questions"></a>Andere Fragen

### <a name="reference-keys-that-contain-non-alphanumeric-characters-in-json-text"></a>Referenzschlüssel, die nicht-alphanumerische Zeichen in JSON-Text enthalten  
 **Frage:** Schlüssel in meinem JSON-Text enthalten nicht-alphanumerische Zeichen. Wie kann ich diese Eigenschaften verweisen?  
  
 **Antwort:** In JSON-Pfaden müssen Sie diese in Anführungszeichen einschließen. Beispiel: `JSON_VALUE(@json, '$."$info"."First Name".value')`.
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Erfahren Sie mehr über die integrierte JSON-Unterstützung in SQL Server  
Für viele spezifische Lösungen Fälle und Empfehlungen zu verwenden, finden Sie unter der [Blogeinträge von jovan zur integrierten JSON-Unterstützung](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) in SQL Server und Azure SQL-Datenbank von Microsoft Program Manager Jovan Popovic.

