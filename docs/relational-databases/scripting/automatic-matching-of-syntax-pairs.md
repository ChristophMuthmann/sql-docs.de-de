---
title: Automatischer Vergleich von Syntaxpaaren | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IntelliSense [SQL Server], delimiter highlighting
- IntelliSense [SQL Server], syntax pair matching
ms.assetid: bfc54cda-bfd6-4545-a5b9-f9db2ae13769
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a86f4ede8645a7346234ab1bbfd3a45e3d01393a
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="automatic-matching-of-syntax-pairs"></a>Automatischer Vergleich von Syntaxpaaren
  Durch den automatischen Vergleich von Syntaxpaaren erhalten Sie unmittelbar Aufschluss darüber, ob Syntaxelemente, die paarweise codiert werden müssen, ordnungsgemäß miteinander kombiniert sind. Im Abfrage-Editor von [!INCLUDE[ssDE](../../includes/ssde-md.md)] wird dieser Vorgang als Trennzeichenvergleich, im XMLA-Abfrage-Editor von Analysis Services als Klammernvergleich und im MDX- sowie im DMX-Editor als Klammernvergleich bezeichnet.  
  
## <a name="database-engine-query-editor-delimiter-matching"></a>Trennzeichenvergleich im Datenbankmodul-Abfrage-Editor  
 Der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor vergleicht die Trennzeichen, die die Begrenzungen von Codeblöcken angeben. Der Vergleich erfolgt auf zwei verschiedene Weisen:  
  
-   Der Editor hebt beide Trennzeichen in einem Paar hervor, sobald Sie das zweite Trennzeichen des Paars eingegeben haben.  
  
-   Immer, wenn sich der Cursor auf einem der Trennzeichen eines Paars befindet, können Sie mithilfe der Tastenkombination STRG+] zum entsprechenden Trennzeichen springen.  
  
### <a name="delimiter-pairs"></a>Trennzeichenpaare  
 Beim automatischen Trennzeichenvergleich werden die folgenden Trennzeichen erkannt:  
  
|Vorangestelltes Trennzeichen|Schließendes Trennzeichen|  
|--------------------|-----------------------|  
|**(**|**)**|  
|**BEGIN**|**END**|  
|**BEGIN TRY**|**END TRY**|  
|**BEGIN CATCH**|**END CATCH**|  
  
 Beim automatischen Trennzeichenvergleich werden die Trennzeichen für Bezeichner in Klammern ([ObjectName]) oder Bezeichner in Anführungszeichen ("ObjectName") nicht erkannt. Beim Paarvergleich werden die einzelnen Anführungszeichen als Trennzeichen für Zeichenfolgenliterale ('string') nicht verglichen, weil die Farbcodierung bereits erkennen lässt, ob die Zeichenfolge ein Trennzeichen aufweist.  
  
### <a name="delimiter-highlighting"></a>Hervorhebung von Trennzeichen  
 Beim Vergleich werden sowohl das vorangestellte als auch das schließende Element eines Paars von Trennzeichen hervorgehoben. Auf diese Weise können Sie Codeblöcke visuell identifizieren und überprüfen, ob nicht übereinstimmende Paare von Trennzeichen vorhanden sind.  
  
 Trennzeichen werden hervorgehoben, wenn Sie den letzten Buchstaben des Paars eingeben. Wenn Sie z. B. bei einem BEGIN…END-Paar zuerst BEGIN und dann END eingeben, wird die Hervorhebung aktiviert, sobald Sie den letzten Buchstaben von END eingeben. Es ist nicht erforderlich, zuerst das vorangestellte und dann das schließende Trennzeichen einzugeben, um die Hervorhebung zu aktivieren. Wenn Sie zuerst END eingeben und dann im Skript einen Bildlauf nach oben ausführen und BEGIN eingeben, wird die Hervorhebung aktiviert, sobald Sie den letzten Buchstaben von BEGIN eingeben. Der letzte eingegebene Buchstabe muss nicht der Buchstabe sein, mit dem das Trennzeichen endet. Wenn Sie z. B. BEGIN zuerst falsch schreiben und BEIN eingeben, wird das BEGIN…END-Paar hervorgehoben, sobald Sie das fehlende G eingeben.  
  
 Das Trennzeichenpaar bleibt so lange hervorgehoben, bis Sie den Cursor verschieben. Die Hervorhebung wird auch dann beim Verschieben des Cursors deaktiviert, wenn der Cursor an eine Position im gleichen Trennzeichen verschoben wird. Sie können die Hervorhebung wieder aktivieren, indem Sie einen beliebigen Buchstaben in einem Element des Paars löschen und erneut eingeben.  
  
## <a name="analysis-services-xmla-query-editor-brace-matching"></a>Klammernvergleich im XMLA-Abfrage-Editor von Analysis Services  
 Beim Klammernvergleich im XMLA-Abfrage-Editor können Sie erkennen, ob Sie die Elemente geschlossen haben, da öffnende und schließende Klammern hervorgehoben werden. Sie können auch mithilfe der Tastenkombination STRG+] von einer Klammer zur jeweils entsprechenden Klammer springen.  
  
 Im XMLA-Abfrage-Editor wird der Klammernvergleich für die folgenden Ausdrücke ausgeführt:  
  
-   Übereinstimmende Start- und Endtags  
  
-   Ein beliebiges Paar von spitzen Klammern („\<“ und „>“).  
  
-   Beginn und Ende von Kommentaren  
  
-   Beginn und Ende von Verarbeitungsanweisungen  
  
-   Beginn und Ende von CDATA-Blöcken  
  
-   Beginn und Ende von DTD-Deklarationen  
  
-   Öffnende und schließende Anführungszeichen bei Attributen  
  
## <a name="mdx-and-dmx-editor-parenthesis-matching"></a>Klammernvergleich im MDX- und im DMX-Editor  
 Der MDX-Editor (Multidimensional Expressions) und der DMX-Editor (Data Mining Expressions) vergleichen automatisch Klammernpaare in Funktionen.  
  
  
