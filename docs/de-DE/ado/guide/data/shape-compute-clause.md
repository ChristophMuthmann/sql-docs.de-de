---
title: Form von COMPUTE-Klausel | Microsoft Docs
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
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f819175724a2b1de803dce5ef5c4a14e4d3c1665
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="shape-compute-clause"></a>Shape-COMPUTE-Klausel
Eine Form "COMPUTE-Klausel generiert ein übergeordnetes Element **Recordset**, einen Verweis auf das untergeordnete Element, dessen Spalten bestehen aus **Recordset**; Dies ist optional Spalten, deren Inhalt neue, Kapitel oder berechnete Spalten werden, oder die Ergebnis der Ausführung von Aggregatfunktionen auf dem untergeordneten Element **Recordset** oder eine zuvor geformten **Recordset**; und alle Spalten aus den untergeordneten **Recordset** abgelesen Das optionale BY-Klausel.  
  
## <a name="syntax"></a>Syntax  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Description  
 Die Teile dieser Klausel sind wie folgt aus:  
  
 *child-command*  
 Besteht aus einer der folgenden:  
  
-   Einen Abfragebefehl in geschweiften Klammern ("{}"), die ein untergeordnetes Element zurückgibt **Recordset** Objekt. Der Befehl wird an den zugrunde liegenden Datenanbieter ausgegeben, und die Syntax ist abhängig von den Anforderungen von diesem Anbieter. Dies ist der SQL-Sprache in der Regel wird, obwohl ADO keine bestimmte Abfragesprache erforderlich ist.  
  
-   Der Name eines vorhandenen geformten **Recordset**.  
  
-   Eine andere Form-Befehl.  
  
-   Das TABLE-Schlüsselwort, gefolgt vom Namen einer Tabelle in der Datenanbieter.  
  
 *child-alias*  
 Ein Alias, der zum Verweisen auf die **Recordset** zurückgegebenes der *untergeordnete-Befehl.* Die *untergeordnete-Alias* ist in der Liste der Spalten in der COMPUTE-Klausel erforderlich und definiert die Beziehung zwischen übergeordneten und untergeordneten **Recordset** Objekte.  
  
 *appended-column-list*  
 Eine Liste, in der jedes Element eine Spalte im generierten übergeordneten Element definiert. Jedes Element enthält eine Kapitelspalte, eine neue Spalte, einer berechneten Spalte oder einen Wert, der eine Aggregatfunktion für das untergeordnete Element entstandene **Recordset**.  
  
 *grp-field-list*  
 Eine Liste der Spalten in den übergeordneten und untergeordneten **Recordset** Objekten, das angibt, wie die Zeilen im untergeordneten gruppiert werden sollen.  
  
 Für jede Spalte in der *Gruppe-Feld-List* ist es eine entsprechende Spalte in den untergeordneten und übergeordneten **Recordset** Objekte. Für jede Zeile in der übergeordneten Tabelle **Recordset**, die *Gruppe Feldliste* Spalten eindeutige Werte und das untergeordnete Element aufweisen **Recordset** verwiesen wird, von der übergeordneten Zeile besteht ausschließlich aus untergeordneten Zeilen, deren *Gruppe Feldliste* Spalten haben die gleichen Werte wie die übergeordnete Zeile.  
  
 Wenn die BY-Klausel enthalten ist, ist das untergeordnete Element **Recordset**der Zeilen basierend auf den Spalten in der COMPUTE-Klausel gruppiert. Das übergeordnete Element **Recordset** enthält eine Zeile für jede Gruppe von Zeilen in der untergeordneten **Recordset**.  
  
 Wenn die BY-Klausel weggelassen wird, das gesamte untergeordnete **Recordset** so behandelt, als eine einzelne Gruppe und das übergeordnete Element **Recordset** genau eine Zeile enthält. Diese Zeile verweist auf das gesamte untergeordnete **Recordset**. Das Weglassen der BY-Klausel können Sie zum Berechnen von Aggregaten "Gesamtsumme" über das gesamte untergeordnete **Recordset**.  
  
 Beispiel:  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 Unabhängig von der Art der übergeordneten **Recordset** formatiert ist (mithilfe von COMPUTE oder mithilfe von APPEND), enthält es eine Kapitelspalte, die verwendet wird, besteht die Beziehung zu einer untergeordneten **Recordset**. Wenn Sie möchten, das übergeordnete Element **Recordset** Spalten, die Aggregate (SUM, MIN, MAX, usw.) enthalten möglicherweise auch über die untergeordneten Zeilen enthalten. Das übergeordnete Element und dem untergeordneten **Recordset** kann Spalten enthalten, die einen Ausdruck in der Zeile enthalten die **Recordset**sowie Spalten, die neu und anfangs leer.  
  
## <a name="operation"></a>Vorgang  
 Die *untergeordneten Produktionsabfragen* ausgegeben wird, an den Anbieter, die ein untergeordnetes Element zurückgibt **Recordset**.  
  
 Die COMPUTE-Klausel gibt die Spalten des übergeordneten Elements **Recordset**, was u. u. einen Verweis auf das untergeordnete Element nicht **Recordset**, eine oder mehrere Aggregate, einem berechneten Ausdruck oder neue Spalten. Ist eine BY-Klausel, die Spalten, die es definiert auch an der übergeordneten Tabelle angefügt **Recordset**. Die BY-Klausel gibt an, wie die Zeilen der untergeordneten **Recordset** gruppiert sind.  
  
 Nehmen wir beispielsweise an, dass Sie eine Tabelle namens Demographics verfügen Felder Zustand, Ort und Auffüllung besteht. (Die Auffüllung Zahlen in der Tabelle dienen lediglich als Beispiel).  
  
|Status|Ort|Auffüllung|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|OR|Medford|200,000|  
|OR|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|SAN Diego|600,000|  
|WA|Tacoma|500,000|  
|OR|Corvallis|300,000|  
  
 Geben Sie nun diese Shape-Befehl ein:  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 Dieser Befehl öffnet ein geformten **Recordset** mit zwei Ebenen. Die übergeordnete Ebene wird eine generierte **Recordset** mit eine Aggregatsspalte (`SUM(rs.population)`), eine Spalte verweisen auf das untergeordnete Element **Recordset** (`rs`), und eine Spalte zum Gruppieren des untergeordneten **Recordset** (`state`). Die untergeordnete Ebene ist die **Recordset** durch den Abfragebefehl zurückgegeben (`select * from demographics`).  
  
 Das untergeordnete Element **Recordset** Detailzeilen werden nach Zustand gruppiert, aber ansonsten keine bestimmte Reihenfolge. Die Gruppen werden also nicht in alphabetischer bzw. numerischer Reihenfolge. Wenn Sie möchten, dass das übergeordnete Element **Recordset** um sortiert zu werden, können Sie die **Recordset sortieren** Methode, um das übergeordnete Element zu sortieren **Recordset**.  
  
 Sie können jetzt im geöffneten übergeordneten navigieren **Recordset** und Zugriff auf die untergeordneten Detail **Recordset** Objekte. Weitere Informationen finden Sie unter [zugreifen auf Zeilen in einem hierarchischen Recordset](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>Übergeordnete und untergeordnete Detail-Recordsets  
  
### <a name="parent"></a>Parent  
  
|SUM (Rs. Auffüllung)|rs|Status|  
|---------------------------|--------|-----------|  
|1,300,000|Verweis auf child1|CA|  
|1,200,000|Verweis auf child2|WA|  
|1,100,000|Verweis auf child3|OR|  
  
## <a name="child1"></a>Child1  
  
|Status|Ort|Auffüllung|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|SAN Diego|600,000|  
  
## <a name="child2"></a>Child2  
  
|Status|Ort|Auffüllung|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|Status|Ort|Auffüllung|  
|-----------|----------|----------------|  
|OR|Medford|200,000|  
|OR|Portland|400,000|  
|OR|Corvallis|300,000|  
  
## <a name="see-also"></a>Siehe auch  
 [Zugreifen auf Zeilen in einem hierarchischen Recordset](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Daten strukturieren (Übersicht)](../../../ado/guide/data/data-shaping-overview.md)   
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)   
 [Formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Erforderlichen Anbieter Daten können strukturiert werden.](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Form "APPEND-Klausel](../../../ado/guide/data/shape-append-clause.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value-Eigenschaft (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications-Funktionen](../../../ado/guide/data/visual-basic-for-applications-functions.md)
