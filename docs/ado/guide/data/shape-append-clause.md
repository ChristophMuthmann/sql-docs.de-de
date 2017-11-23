---
title: APPEND-Klausel Form | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ab01c719611309117308c818930b1553741495e6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="shape-append-clause"></a>Form "APPEND-Klausel
Die Form Befehl APPEND-Klausel fügt eine Spalte oder Spalten zu einer **Recordset**. Diese Spalten sind in vielen Fällen Kapitelspalten, die auf ein untergeordnetes Element verweisen **Recordset**.  
  
## <a name="syntax"></a>Syntax  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Description  
 Die Teile dieser Klausel sind wie folgt aus:  
  
 *Parent-Befehl*  
 0 (null) oder eines der folgenden (-Eigenschaftenmethode der *übergeordneten Befehl* vollständig):  
  
-   Ein Anbieterbefehl in geschweifte Klammern ("") eingeschlossen, zurückgibt eine **Recordset** Objekt. Der Befehl wird an den zugrunde liegenden Datenanbieter ausgegeben, und die Syntax ist abhängig von den Anforderungen von diesem Anbieter. Dies ist der SQL-Sprache in der Regel wird, obwohl ADO keine bestimmte Abfragesprache erforderlich ist.  
  
-   Eine andere Form-Befehl, die in Klammern eingebettet sind.  
  
-   Das TABLE-Schlüsselwort, gefolgt vom Namen einer Tabelle in der Datenanbieter.  
  
 *übergeordneten alias*  
 Ein optionaler Alias, der auf das übergeordnete Element verweist **Recordset**.  
  
 *Spaltenliste*  
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
 *untergeordnete recordset*  
 -   Ein Anbieterbefehl in geschweifte Klammern ("") eingeschlossen, zurückgibt eine **Recordset** Objekt. Der Befehl wird an den zugrunde liegenden Datenanbieter ausgegeben, und die Syntax ist abhängig von den Anforderungen von diesem Anbieter. Dies ist der SQL-Sprache in der Regel wird, obwohl ADO keine bestimmte Abfragesprache erforderlich ist.  
  
-   Eine andere Form-Befehl, die in Klammern eingebettet sind.  
  
-   Der Name eines vorhandenen geformten **Recordset**.  
  
-   Das TABLE-Schlüsselwort, gefolgt vom Namen einer Tabelle in der Datenanbieter.  
  
 *untergeordnete-alias*  
 Ein Alias, der auf das untergeordnete Element verweist **Recordset**.  
  
 *Übergeordnete Spalten*  
 Eine Spalte in der **Recordset** zurückgegebenes der *übergeordneten-Befehl.*  
  
 *Untergeordnete Spalten*  
 Eine Spalte in der **Recordset** zurückgegebenes der *untergeordnete Befehl*.  
  
 *Param-Anzahl*  
 Finden Sie unter [von parametrisierten Befehlen](../../../ado/guide/data/operation-of-parameterized-commands.md).  
  
 *Kapitel-alias*  
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
