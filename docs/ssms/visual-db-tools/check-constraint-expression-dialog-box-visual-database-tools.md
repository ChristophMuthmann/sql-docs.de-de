---
title: "CHECK-Einschränkungsausdruck (Dialogfeld) (Visual Database Tools) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.checkconstraintexpression
ms.assetid: beb6ce43-3913-4d66-8826-8e885335b790
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2d768a6db424008daaffdcb5b14491adfa48962f
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="check-constraint-expression-dialog-box-visual-database-tools"></a>CHECK-Einschränkungsausdruck (Dialogfeld) (Visual Database Tools)
Wenn Sie eine CHECK-Einschränkung einer Tabelle oder Spalte anfügen, müssen Sie einen SQL-Ausdruck einschließen. Geben Sie den CHECK-Einschränkungsausdruck in das zur Verfügung gestellte Feld ein.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
expression  
Geben Sie den Ausdruck ein.  
  
Sie können einen einfachen Einschränkungsausdruck erstellen, um Daten auf eine einfache Bedingung zu prüfen. Sie können aber auch einen komplexen Ausdruck mithilfe boolescher Operatoren erstellen, um Daten auf mehrere Bedingungen zu prüfen. Angenommen, die authors-Tabelle enthält eine zip-Spalte, in die nur Zeichenfolgen aus 5 Ziffern eingegeben werden sollen. Der folgende Einschränkungsausdruck stellt sicher, dass nur fünfstellige Zahlen zulässig sind:  
  
```  
zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
```  
  
Angenommen, die Tabelle sales enthält die Spalte qty, für die ein Wert größer als 0 erforderlich ist. Die folgende Einschränkung stellt sicher, dass nur positive Werte zulässig sind:  
  
```  
qty > 0  
```  
  
Ein weiteres Beispiel: Die orders-Tabelle schränkt die Art der Kreditkarten ein, die für Kreditkartenaufträge akzeptiert werden. Die folgende Einschränkung stellt sicher, dass nur Visa-, MasterCard- oder American Express-Kreditkarten akzeptiert werden, wenn als Zahlungsmittel für den Auftrag eine Kreditkarte verwendet wird.  
  
```  
NOT (payment_method = 'credit card') OR  
   (card_type IN ('VISA', 'MASTERCARD', 'AMERICAN EXPRESS'))  
```  
  
## <a name="to-define-a-constraint-expression"></a>So definieren Sie einen Einschränkungsausdruck  
Geben Sie auf der Registerkarte Einschränkungen überprüfen der Eigenschaftenseiten einen Ausdruck in das Feld Einschränkungsausdruck ein. Verwenden Sie dabei die folgende Syntax:  
  
<pre>{constant | column_name | function | (subquery)}  
[{operator | AND | OR | NOT}  
{constant | column_name | function | (subquery)}...]</pre>  
  
Die SQL-Syntax besteht aus folgenden Parametern:  
  
|Parameter|Description|  
|-------------|---------------|  
|Konstante|Ein Literalwert, wie numerische Daten oder Zeichendaten. Zeichendaten müssen in einfache Anführungszeichen (') eingeschlossen werden.|  
|column_name|Gibt eine Spalte an.|  
|Funktion|Eine integrierte Funktion.|  
|Operator|Arithmetischer oder bitweiser Operator bzw. ein Vergleichs- oder Zeichenfolgenoperator.|  
|AND|Wird in booleschen Ausdrücken verwendet, um zwei Ausdrücke miteinander zu verbinden. Wenn beide Ausdrücke True sind, werden Ergebnisse zurückgegeben.<br /><br />Wenn in einer Anweisung sowohl AND als auch OR verwendet werden, wird AND zuerst verarbeitet. Sie können die Reihenfolge der Ausführung ändern, indem Sie Klammern verwenden.|  
|OR|Wird in booleschen Ausdrücken verwendet, um zwei oder mehr Bedingungen miteinander zu verbinden. Wenn eine der beiden Bedingungen True ist, werden Ergebnisse zurückgegeben.<br /><br />Wenn in einer Anweisung sowohl AND als auch OR verwendet werden, wird zuerst AND und dann OR ausgewertet. Sie können die Reihenfolge der Ausführung ändern, indem Sie Klammern verwenden.|  
|NICHT|Negiert jeden booleschen Ausdruck (auch Schlüsselwörter wie LIKE, NULL, BETWEEN, IN und EXISTS).<br /><br />Wenn mehrere logische Operatoren in einer Anweisung verwendet werden, wird NOT zuerst verarbeitet. Sie können die Reihenfolge der Ausführung ändern, indem Sie Klammern verwenden.|  
  
## <a name="see-also"></a>Siehe auch  
[UNIQUE- und CHECK-Einschränkungen](http://msdn.microsoft.com/en-us/637098af-2567-48f8-90f4-b41df059833e)  
[Erstellen von Unique-Einschränkungen](http://msdn.microsoft.com/en-us/a86f9d6f-f242-43be-b65d-b3435b71b62a)  
  

