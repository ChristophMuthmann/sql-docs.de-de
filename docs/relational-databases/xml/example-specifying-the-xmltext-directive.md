---
title: 'Beispiel: Angeben der XMLTEXT-Direktive | Microsoft-Dokumentation'
ms.custom: 
ms.date: 04/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XMLTEXT directive
ms.assetid: e78008ec-51e8-4fd1-b86f-1058a781de17
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 54ada9bad44e2cd8410fe3a70fd022769febc960
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="example-specifying-the-xmltext-directive"></a>Beispiel: Angeben der XMLTEXT-Direktive
  Dieses Beispiel veranschaulicht, wie Daten in der Überlaufspalte mithilfe der **XMLTEXT** -Direktive in einer `SELECT` -Anweisung im EXPLICIT-Modus verarbeitet werden.  
  
 Sie sehen hier die `Person` -Tabelle. In dieser Tabelle speichert die `Overflow` -Spalte den unverbrauchten Teil des XML-Dokuments.  
  
```  
USE tempdb;  
GO  
CREATE TABLE Person(PersonID varchar(5), PersonName varchar(20), Overflow nvarchar(200));  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
   ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P">content</SomeTag>');  
```  
  
 Diese Abfrage ruft Spalten aus der `Person` -Tabelle ab. `Overflow` AttributeName *ist für die* -Spalte nicht angegeben, *directive* ist jedoch auf den Wert `XMLTEXT` festgelegt, um einen Spaltennamen für die Universaltabelle bereitzustellen.  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- No AttributeName; XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 Im resultierenden XML-Dokument:  
  
-   Da für die `Overflow`-Spalte kein *AttributeName*, sondern die `xmltext`-Direktive angegeben ist, werden die Attribute des <`overflow`>-Elements der Attributliste des einschließenden <`Parent`>-Elements angehängt.  
  
-   Da das `PersonID`-Attribut des <`xmltext`>-Elements in Konflikt zu dem auf der gleichen Elementebene abgerufenen `PersonID`-Attribut steht, wird das Attribut des <`xmltext`>-Elements ignoriert, sogar wenn `PersonID` NULL ist. Im Allgemeinen überschreibt ein Attribut ein Attribut mit demselben Namen in der Überlaufspalte.  
  
 Dies ist das Ergebnis:  
  
 ```   
 <Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>  
 <Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>  
 <Parent PersonID="P3" PersonName="Joe" attr3="data">content</Parent>
 ```  
  
 Wird dieselbe Abfrage angegeben, und die Überlaufdaten besitzen Unterelemente, werden die Unterelemente in der `Overflow`-Spalte als Unterelemente des einschließenden <`Parent`>-Elements hinzugefügt.  
  
 So werden in diesem Beispiel die Daten in der `Person`-Tabelle so geändert, dass die `Overflow`-Spalte nun Unterelemente besitzt:  
  
```  
USE tempdb;  
GO  
TRUNCATE TABLE Person;  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
    ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P"><name>PersonName</name></SomeTag>');  
```  
  
 Beim Ausführen derselben Abfrage werden die Unterelemente des <`xmltext`>-Elements als Unterelemente des einschließenden <`Parent`>-Elements hinzugefügt:  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- no AttributeName, XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 Dies ist das Ergebnis:  
  
 ```   
 <Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>  
 <Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>  
 <Parent PersonID="P3" PersonName="Joe" attr3="data">  
 <name>PersonName</name>  
 </Parent>
 ```  
  
 Wird *AttributeName* mit der `xmltext`-Direktive angegeben, werden die Attribute des <`overflow`>-Elements als Attribute der Unterelemente des einschließenden <`Parent`>-Elements hinzugefügt. Der für *AttributeName* angegebene Name wird zum Namen des Unterelements.  
  
 In dieser Abfrage wird *AttributeName*, <`overflow`> zusammen mit der `xmltext`-Direktive angegeben*:*  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!overflow!XMLTEXT] -- Overflow is AttributeName  
                      -- XMLTEXT is a directive  
FROM Person  
FOR XML EXPLICIT  
```  
  
 Dies ist das Ergebnis:  
  
 ```   
 <Parent PersonID="P1" PersonName="Joe">  
 <overflow attr1="data">content</overflow>  
 </Parent>  
 <Parent PersonID="P2" PersonName="Joe">  
 <overflow attr2="data" />  
 </Parent>  
 <Parent PersonID="P3" PersonName="Joe">  
 <overflow attr3="data" PersonID="P">  
 <name>PersonName</name>  
 </overflow>  
 </Parent>
 ```  
  
 In diesem Abfrageelement wird *-Direktive angegeben* für das `PersonName` -Attribut angegeben. Dadurch wird `PersonName` als Unterelement des einschließenden <`Parent`>-Elements hinzugefügt. Die Attribute von <`xmltext`> werden weiterhin an das einschließende <`Parent`>-Element angefügt. Der Inhalt des <`overflow`>-Elements (Unterelemente usw.) wird den anderen Unterelementen der einschließenden <`Parent`>-Elemente vorangestellt.  
  
```  
SELECT 1      AS Tag, NULL as parent,  
       PersonID   AS [Parent!1!PersonID],  
       PersonName AS [Parent!1!PersonName!element], -- element directive  
       Overflow   AS [Parent!1!!XMLTEXT]  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 Dies ist das Ergebnis:  
  
 ```   
 <Parent PersonID="P1" attr1="data">content<PersonName>Joe</PersonName>  
 </Parent>  
 <Parent PersonID="P2" attr2="data">  
 <PersonName>Joe</PersonName>  
 </Parent>  
 <Parent PersonID="P3" attr3="data">  
 <name>PersonName</name>  
 <PersonName>Joe</PersonName>  
 </Parent>
 ```  
  
 Wenn die Daten der `XMLTEXT` -Spalte Attribute für das Stammelement enthalten, werden diese Attribute nicht im XML-Datenschema angezeigt, und der MSXML-Parser führt keine Überprüfung des resultierenden XML-Dokumentfragments aus. Beispiel:  
  
```  
SELECT 1 AS Tag,  
       0 ASParent,  
       N'<overflow a="1"/>' AS 'overflow!1!!xmltext'  
FOR XML EXPLICIT, xmldata;  
```  
  
 Dies ist das Ergebnis. Beachten Sie, dass das overflow-Attribut `a` im zurückgegebenen Schema fehlt:  
  
 ```   
 <Schema name="Schema2"  
 xmlns="urn:schemas-microsoft-com:xml-data"  
 xmlns:dt="urn:schemas-microsoft-com:datatypes">  
 <ElementType name="overflow" content="mixed" model="open">`  
 </ElementType>`  
 </Schema>`  
 <overflow xmlns="x-schema:#Schema2" a="1">  
 </overflow>
 ```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des EXPLICIT-Modus mit FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  

