---
title: Verwenden der Option BINARY BASE64 | Microsoft-Dokumentation
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
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a0cfc14849df2f82429b00e8d912ceba6c74200e
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="use-the-binary-base64-option"></a>Verwenden der Option BINARY BASE64
  Wenn die Option BINARY BASE64 in der Abfrage angegeben ist, werden die Binärdaten im Base64-codierten Format zurückgegeben. Der AUTO-Modus unterstützt die URL-Codierung von Binärdaten standardmäßig (sofern die Option BINARY BASE64 nicht angegeben wurde). Das heißt, anstelle von Binärdaten wird ein Verweis (eine relative URL auf das virtuelle Stammverzeichnis der Datenbank, in der die Abfrage ausgeführt wird) zurückgegeben. Dieser Verweis kann für den Zugriff auf die Binärdaten in nachfolgenden Vorgängen verwendet werden. Die Abfrage muss ausreichend Informationen, wie etwa Primärschlüsselspalten, bereitstellen, damit Teile des Images später im XML-Dokument identifiziert werden können.  
  
 Wenn beim Angeben einer Abfrage ein Alias für die Binärspalte der Sicht verwendet wird, wird der Alias in der URL-Codierung der Binärdaten zurückgegeben. In nachfolgenden Vorgängen ist der Alias bedeutungslos, und die URL-Codierung kann nicht zum Abrufen des Images verwendet werden. Sie sollten somit keine Aliasse bei der Abfrage einer Sicht mithilfe des FOR XML AUTO-Modus verwenden.  
  
 In einer SELECT-Abfrage werden beispielsweise Spalten durch Konvertieren in ein BLOB (Binary Large Object) insofern zu einer temporären Entität, als sie den zugehörigen Tabellen- und Spaltennamen verlieren. Abfragen im AUTO-Modus geben daher einen Fehler aus, da der Wert nicht in der XML-Hierarchie eingeordnet werden kann. Beispiel:  
  
```  
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)  
INSERT INTO MyTable VALUES (1, 0x7);  
```  
  
 Diese Abfrage führt wegen der Konvertierung in BLOB (Binary Large Object) zu einem Fehler:  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO;  
```  
  
 Die Lösung besteht im Hinzufügen der Option BINARY BASE64 zur FOR XML-Klausel. Ohne die Konvertierung liefert die Abfrage die erwarteten Ergebnisse:  
  
```  
SELECT Col1,  
CAST(Col2 as image) as Col2  
FROM MyTable  
FOR XML AUTO, BINARY BASE64;  
```  
  
 Dies ist das Ergebnis:  
  
```  
<MyTable Col1="1" Col2="Bw==" />  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des AUTO-Modus mit FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
