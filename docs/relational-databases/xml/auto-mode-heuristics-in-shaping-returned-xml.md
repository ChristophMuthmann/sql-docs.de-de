---
title: "AUTO-Modus-Heuristik beim Ermitteln der Form des zurückgegebenen XML-Codes | Microsoft-Dokumentation"
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
- AUTO FOR XML mode, heuristics in shaping returned XML
ms.assetid: 6c5cb6c1-2921-4ba1-8100-0bf8074f9103
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d5c3ff12e84d7f858db6458aa6d43609ab68182f
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="auto-mode-heuristics-in-shaping-returned-xml"></a>AUTO-Modus-Heuristik beim Ermitteln der Form des zurückgegebenen XML-Codes
  Der AUTO-Modus ermittelt die Form des zurückgegebenen XML-Codes auf der Grundlage der Abfrage. Um zu ermitteln, wie die Elemente geschachtelt werden sollen, vergleicht die AUTO-Modus-Heuristik die Spaltenwerte in benachbarten Zeilen. Dabei werden Spalten aller Datentypen, mit Ausnahme von **ntext**, **text**, **image**und **xml**miteinander verglichen. Spalten des Datentyps **(n)varchar(max)** und **varbinary(max)** werden verglichen.  
  
 Das folgende Beispiel veranschaulicht die Heuristik des AUTO-Modus beim Ermitteln der Form des resultierenden XML-Codes:  
  
```  
SELECT T1.Id, T2.Id, T1.Name  
FROM   T1, T2  
WHERE ...  
FOR XML AUTO  
ORDER BY T1.Id  
```  
  
 Um zu ermitteln, wo ein neues <`T1`>-Element beginnt, werden alle Spaltenwerte von Tabelle T1 (außer **ntext**, **text**, **image** und **xml**) verglichen, wenn der Schlüssel für die Tabelle T1 nicht angegeben wurde. Nehmen wir als Nächstes an, dass die **Name**-Spalte den Typ **nvarchar(40)** aufweist und dass die SELECT-Anweisung das folgende Rowset zurückgibt:  
  
```  
T1.Id  T1.Name  T2.Id  
-----------------------  
1       Andrew    2  
1       Andrew    3  
1       Nancy     4  
```  
  
 Die Heuristik des AUTO-Modus vergleicht alle Werte aus Tabelle T1, die Id- und die Name-Spalten. Da die ersten zwei Zeilen über die gleichen Werte für die Spalten „Id“ und „Name“ verfügen, wird ein \<T1>-Element, das über zwei untergeordnete \<T2>-Elemente verfügt, im Ergebnis hinzugefügt.  
  
 Der folgende XML-Code wird zurückgegeben:  
  
```  
<T1 Id="1" Name="Andrew">  
    <T2 Id="2" />  
    <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
      <T2 Id="4" />  
</T>  
```  
  
 Nehmen wir jetzt an, dass die Name-Spalte den **text** -Datentyp aufweist. Die Heuristik des AUTO-Modus führt keinen Vergleich der Werte für diesen Datentyp durch. Stattdessen wird angenommen, dass sich die Werte voneinander unterscheiden. Dadurch wird der folgende XML-Code generiert:  
  
```  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="2" />  
</T1>  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
  <T2 Id="4" />  
</T1>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des AUTO-Modus mit FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
