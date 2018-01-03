---
title: Zugreifen auf Zeilen in einem hierarchischen Recordset | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a25fbf3437b05497093ec9a8b83c69342faba077
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>Zugreifen auf Zeilen in einem hierarchischen Recordset (Beispiel)
Das folgende Beispiel zeigt die Schritte in einer hierarchischen Zugriff Zeilen zum [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **Recordset** Objekte aus der **Autoren** und **Titleauthor** Tabellen beziehen sich vom Autor-ID an.

2.  Die äußere Schleife zeigt jeden Autor vor-und Nachname, Bundesland und Identifikation.

3.  Die angefügten **Recordset** für jede Zeile aus abgerufen wird die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung und zugewiesen *RstTitleAuthor*.

4.  Die innere Schleife zeigt vier Felder aus jeder Zeile in der angefügten **Recordset**.

 Die [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) -Eigenschaftensatz auf **"false"** zur Veranschaulichung, damit Sie sehen können, im Kapitel über das Ändern explizit in jeder Iteration der äußeren Schleife. Um das Codebeispiel effizienter zu gestalten, können Sie die Zuweisung in Schritt 3 vor der ersten Zeile in Schritt 2, verschieben, damit die Zuweisung wird nur einmal ausgeführt. Legen Sie dann die [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) Eigenschaft **"true"**, sodass *RstTitleAuthor* implizit und automatisch ändert sich im entsprechenden Kapitel immer *Rst* in eine neue Zeile bewegt.

## <a name="example"></a>Beispiel

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>Siehe auch
 [Übersicht über die Strukturierung Daten](../../../ado/guide/data/data-shaping-overview.md) [Field-Objekt](../../../ado/reference/ado-api/field-object.md) [Fields-Auflistung (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md) [formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md) [strukturiert werden, Dienst für Microsoft-Daten OLE DB (ADO-Dienstanbieter)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [Anbieter für die Strukturierung der Daten erforderlichen](../../../ado/guide/data/required-providers-for-data-shaping.md) [Form APPEND-Klausel](../../../ado/guide/data/shape-append-clause.md) [Form Befehle im allgemeinen](../../../ado/guide/data/shape-commands-in-general.md) [Shape-COMPUTE-Klausel](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic für Applikationen-Funktionen](../../../ado/guide/data/visual-basic-for-applications-functions.md)
