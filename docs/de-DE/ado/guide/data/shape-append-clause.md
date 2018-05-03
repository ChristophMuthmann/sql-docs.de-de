---
title: APPEND-Klausel Form | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 377419c89d8a21910aa6ef1e925af4006115b147
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="shape-append-clause"></a>Form "APPEND-Klausel
Die Form Befehl APPEND-Klausel fügt eine Spalte oder Spalten zu einer **Recordset**. Diese Spalten sind in vielen Fällen Kapitelspalten, die auf ein untergeordnetes Element verweisen **Recordset**.  
  
## <a name="syntax"></a>Syntax  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Description  
 Die Teile dieser Klausel sind wie folgt aus:  
  
 *parent-command*  
 0 (null) oder eines der folgenden (-Eigenschaftenmethode der *übergeordneten Befehl* vollständig):  
  
-   Ein Anbieterbefehl wird in geschweiften Klammern ("{}") zurückgibt, die eine **Recordset** Objekt. Der Befehl wird an den zugrunde liegenden Datenanbieter ausgegeben, und die Syntax ist abhängig von den Anforderungen von diesem Anbieter. Dies ist der SQL-Sprache in der Regel wird, obwohl ADO keine bestimmte Abfragesprache erforderlich ist.  
  
-   Eine andere Form-Befehl, die in Klammern eingebettet sind.  
  
-   Das TABLE-Schlüsselwort, gefolgt vom Namen einer Tabelle in der Datenanbieter.  
  
 *parent-alias*  
 Ein optionaler Alias, der auf das übergeordnete Element verweist **Recordset**.  
  
 *column-list*  
 Eine oder mehrere der folgenden:  
  
-   Fügt die aggregierte Spalte.  
  
-   Eine berechnete Spalte.  
  
-   Eine neue Spalte, die mithilfe der neuen-Klausel erstellt wird.  
  
-   Eine Kapitelspalte. Die Definition einer Kapitel-Spalte wird in Klammern ("()") eingeschlossen. Siehe die folgende Syntax.  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>Hinweise  
 *child-recordset*  
 -   Ein Anbieterbefehl wird in geschweiften Klammern ("{}") zurückgibt, die eine **Recordset** Objekt. Der Befehl wird an den zugrunde liegenden Datenanbieter ausgegeben, und die Syntax ist abhängig von den Anforderungen von diesem Anbieter. Dies ist der SQL-Sprache in der Regel wird, obwohl ADO keine bestimmte Abfragesprache erforderlich ist.  
  
-   Eine andere Form-Befehl, die in Klammern eingebettet sind.  
  
-   Der Name eines vorhandenen geformten **Recordset**.  
  
-   Das TABLE-Schlüsselwort, gefolgt vom Namen einer Tabelle in der Datenanbieter.  
  
 *child-alias*  
 Ein Alias, der auf das untergeordnete Element verweist **Recordset**.  
  
 *parent-column*  
 Eine Spalte in der **Recordset** zurückgegebenes der *übergeordneten-Befehl.*  
  
 *child-column*  
 Eine Spalte in der **Recordset** zurückgegebenes der *untergeordnete Befehl*.  
  
 *param-number*  
 Finden Sie unter [von parametrisierten Befehlen](../../../ado/guide/data/operation-of-parameterized-commands.md).  
  
 *chapter-alias*  
 Ein Alias, der auf die Kapitelspalte, angefügt an das übergeordnete Element verweist.  
  
> [!NOTE]
>  Die *"Parent-Spalte* TO *untergeordnete-Spalte"* -Klausel ist tatsächlich eine Liste, jede Beziehung definiert ist, in dem durch ein Komma getrennt.  
  
> [!NOTE]
>  Die Klausel nach dem ANFÜGEN-Schlüsselwort ist tatsächlich eine Liste, in dem jede Klausel, die durch ein Komma getrennt ist, und definiert eine andere Spalte an das übergeordnete Element angefügt wird.  
  
## <a name="remarks"></a>Hinweise  
 Beim Erstellen von Anbieterbefehlen aus Benutzereingaben als Teil eines Befehls Form Form ein Befehls als nicht transparente Zeichenfolge behandelt den vom Benutzer bereitgestellten und nutzungsvereinbarungen an dem Anbieter zu übergeben. Beispielsweise ist in den folgenden Befehl für die Form "  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 Form "werden zwei Befehle ausgeführt: `select * from t1` und (`select * from t2 RELATE k1 TO k2)`. Wenn der Benutzer einen zusammengesetzten Befehl bereitstellt, der mehrere durch Semikolons getrennte Anbieterbefehlen besteht, kann Form nicht um den Unterschied zu unterscheiden. Klicken Sie hierzu in der folgenden Form-Befehl  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 Form führt `select * from t1; drop table t1` und (`select * from t2 RELATE k1 TO k2),` bemerken, die nicht `drop table t1` ist eine Separate und in diese Anbieterbefehl wird Groß-/Kleinschreibung, gefährlich. Anwendungen müssen immer der Benutzereingabe um solche potenziellen Hackerangriffe verhindern überprüfen.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Operation of Non-Parameterized Commands (Verarbeitung nicht-parametrisierter Befehle)](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [Operation of Parameterized Commands (Verarbeitung parametrisierter Befehle)](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [Hybridbefehle](../../../ado/guide/data/hybrid-commands.md)  
  
-   [Intervening Shape COMPUTE Clauses (Zwischenschalten von SHAPE COMPUTE-Klauseln)](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Daten strukturiert werden, Beispiel](../../../ado/guide/data/data-shaping-example.md)   
 [Formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)
