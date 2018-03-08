---
title: Filter-Eigenschaft | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Filter
helpviewer_keywords:
- Filter property
ms.assetid: 80263a7a-5d21-45d1-84fc-34b7a9be4c22
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e0a74efdc9eeef18eac76e582355653d6677139
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="filter-property"></a>Filter-Eigenschaft
Gibt einen Filter für Daten in einem [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Variant** -Wert, der einen der folgenden enthalten kann:  
  
-   **Zeichenfolge der Suchkriterien** ??? eine Zeichenfolge, die eine oder mehrere einzelne Klauseln, die mit dieser verkettet bestehend aus **AND** oder **OR** Operatoren.  
  
-   **Array von Lesezeichen** ??? ein Array von eindeutigen Lesezeichen Werten, die den Datensätzen in der **Recordset** Objekt.  
  
-   Ein [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) Wert.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **Filter** Eigenschaft, um selektiv herauszufiltern Datensätze in einem **Recordset** Objekt. Die gefilterten **Recordset** verwandelt sich der aktuelle Cursor. Andere Eigenschaften, die Werte zurückgeben, basierend auf dem aktuellen **Cursor** betroffen sind, z. B. [AbsolutePosition-Eigenschaft (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage-Eigenschaft (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md), [ RecordCount-Eigenschaft (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md), und ["PageCount"-Eigenschaft (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md). Dies ist, da das Festlegen der **Filter** Eigenschaft auf einen bestimmten Wert wird den aktuellen Datensatz verschoben, auf den ersten Eintrag, der den neuen Wert entspricht.  
  
 Die Zeichenfolge der Suchkriterien besteht aus Klauseln in der Form *FieldName Operatorwert* (z. B. `"LastName = 'Smith'"`). Sie können zusammengesetzte Klauseln erstellen, indem Sie einzelne Klauseln mit verketten **AND** (z. B. `"LastName = 'Smith' AND FirstName = 'John'"`) oder **OR** (z. B. `"LastName = 'Smith' OR LastName = 'Jones'"`). Verwenden Sie die folgenden Richtlinien für Kriterienzeichenfolgen an:  
  
-   *Feldname* muss ein gültigen Feldnamen aus der **Recordset**. Wenn das Feldname Leerzeichen enthält, müssen Sie den Namen in eckige Klammern einschließen.  
  
-   Operator muss eine der folgenden sein: \<, >, \<=, > =, <>, =, oder **wie**.  
  
-   Ist gleich dem Wert, mit denen Sie die Feldwerte vergleichen (z. B. 'Smith' #8/24/&#95;, 12.345 oder 50,00 $). Verwenden Sie einfache Anführungszeichen mit Zeichenfolgen und Nummernzeichen (#) mit Datumsangaben aus. Für Zahlen können Sie das Dezimaltrennzeichen, Dollarzeichen sowie die wissenschaftliche Schreibweise. Wenn Operator **wie**, Wert kann Platzhalter verwenden. Nur das Sternchen (*) und Prozentzeichen (%)-Platzhalter sind zulässig, und sie müssen das letzte Zeichen in der Zeichenfolge sein. Wert darf nicht null sein.  
  
> [!NOTE]
>  Um einfache Anführungszeichen (') in den Filterwert einzuschließen, verwenden Sie zwei einfache Anführungszeichen zur Darstellung. Beispielsweise um lautet filtern, die Zeichenfolge der Suchkriterien muss "col1 =" O "Malley'". Um einfache Anführungszeichen am Anfang und Ende der Filterwert einzuschließen, schließen Sie die Zeichenfolge mit dem Nummernzeichen (#). Angenommen, um auf "1" zu filtern, die Zeichenfolge der Suchkriterien muss "col1 = #"1"#".  
  
-   Es gibt keine Rangfolge zwischen und und oder. Klauseln können in Klammern gruppiert werden. Allerdings kann nicht durch ein OR verknüpften Klauseln group und treten Sie der Gruppe mit einer anderen Klausel mit einer AND, wie folgt:`(LastName = 'Smith' OR LastName = 'Jones') AND FirstName = 'John'`  
  
-   Stattdessen erstellen Sie auf diesen Filter als`(LastName = 'Smith' AND FirstName = 'John') OR (LastName = 'Jones' AND FirstName = 'John')`  
  
-   In einer **wie** -Klausel, können Sie einen Platzhalter am Anfang und Ende des Musters (z. B. LastName Like ' * Mit\*"), oder nur am Ende des Musters (z. B. LastName Like ' Smit\*").  
  
 Die Filter-Konstanten erleichtern das zum Auflösen einzelner Datensatz Konflikte während der Batch-Aktualisierungsmodus können Sie anzeigen, z. B. nur die Datensätze, die während des letzten betroffen [UpdateBatch-Methode](../../../ado/reference/ado-api/updatebatch-method.md) -Methodenaufruf.  
  
 Festlegen der Filter-Eigenschaft selbst möglicherweise ein Fehler aufgrund eines Konflikts mit dem zugrunde liegenden Daten (z. B. wurde ein Datensatz bereits von einem anderen Benutzer gelöscht wurde). In diesem Fall gibt der Anbieter Warnungen an, die die [Fehler Auflistung (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung jedoch nicht Halt programmausführung. Ein Laufzeitfehler tritt nur dann, wenn auf den angeforderten Datensätzen Konflikte bestehen. Verwenden der [Status-Eigenschaft (ADO-Recordset)](../../../ado/reference/ado-api/status-property-ado-recordset.md) Eigenschaft, um Datensätze mit Konflikten zu suchen.  
  
 Festlegen der **Filter** Eigenschaft, um eine leere Zeichenfolge ("") hat dieselbe Wirkung wie das Verwenden von der **AdFilterNone** konstant.  
  
 Wenn die **Filter** Eigenschaft festgelegt ist, verschiebt die Position des aktuellen Datensatzes auf den ersten Eintrag in der gefilterten Teilmenge der Datensätze in der **Recordset**. Auf ähnliche Weise, wenn die **Filter** Eigenschaft deaktiviert ist, verschiebt die Position des aktuellen Datensatzes auf den ersten Eintrag in der **Recordset**.  
  
 Wenn eine **Recordset** auf ein Feld des einige variant-Typ (z. B. Sql_variant) ein Fehler Basis gefiltert (DISP_E_TYPEMISMATCH oder 80020005) führt die Untertypen von in die Zeichenfolge der Suchkriterien verwendeten Werte für Felder und Filter stimmen nicht überein. Z. B. wenn ein **Recordset** Objekt (Rs) enthält eine Spalte (C) mit den Sql_variant-Typ und ein Feld für diese Spalte den Wert 1 festlegen die Zeichenfolge der Suchkriterien von Rs I4 Typs zugewiesen wurde. Filter = "C = 'A'" auf das Feld, der zur Laufzeit löst den Fehler. Allerdings Rs. Filter = "C = 2" angewendet werden, auf dem gleichen Feld erstellt keine Fehler, obwohl das Feld aus der aktuellen Ressourceneintragssatz gefiltert werden.  
  
 Finden Sie unter der [Lesezeichen-Eigenschaft (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md) -Eigenschaft für eine Erläuterung der Lesezeichenwerte, die aus dem Sie ein Array zur Verwendung mit der Filter-Eigenschaft erstellen können.  
  
 Nur in Form von Zeichenfolgen Kriterien gefiltert (z. B. OrderDate > ' 12/31/1999 ') wirken sich auf den Inhalt einer permanenten **Recordset**. Filter mit einem Array von Lesezeichen erstellt oder mithilfe eines Wertes aus FilterGroupEnum wirkt sich nicht auf den Inhalt des beibehaltenen **Recordset**. Diese Regeln gelten für Recordsets mit Client- oder serverseitige Cursor erstellt wurde.  
  
> [!NOTE]
>  Wenn Sie das Flag AdFilterPendingRecords anwenden, um einen gefilterten und geändert **Recordset** im Batchmodus Update ausgeführt, die resultierenden **Recordset** ist leer, wenn die Filterung auf das Schlüsselfeld der basierendes ein Tabelle und die Änderung wurde versucht, auf den Werten Schlüsselfeld. Die resultierenden **Recordset** werden nicht leer, wenn eine der folgenden Aussagen zutrifft:  
  
-   Die Filterung wurde auf nichtschlüsselfelder in einer Tabelle basieren.  
  
-   Die Filterung wurde auf alle Felder in einer Tabelle mit mehreren Schlüsseln basieren.  
  
-   Änderungen, die auf nichtschlüsselfelder in einer Tabelle vorgenommen wurden.  
  
-   Änderungen, die auf alle Felder in einer Tabelle mit mehreren Schlüsseln vorgenommen wurden.  
  
 Die folgende Tabelle enthält die Auswirkungen der **AdFilterPendingRecords** in verschiedenen Kombinationen von Filterung und Änderungen. Die linke Spalte zeigt die möglichen Änderungen; Änderungen können auf die nicht als Schlüssel Felder, auf das Schlüsselfeld in einer Tabelle oder eines der wichtigsten Felder in einer Tabelle mit mehreren Schlüsseln vorgenommen werden. Die oberste Zeile wird das Filterkriterium gezeigt: Filterung kann auf eines der Felder nicht sortiert das Schlüsselfeld in einer Tabelle oder eines der wichtigsten Felder in einer Tabelle mit mehreren Schlüsseln basieren. Die sich überschneidenden Zellen enthalten die Ergebnisse: + bedeutet angewendet **AdFilterPendingRecords** führt zu einer nicht leeren **Recordset**; - bedeutet, dass eine leere **Recordset**.  
  
||Nicht-Schlüssel|Einzelner Schlüssel|Mehrere Schlüssel|  
|-|--------------|----------------|-------------------|  
|**Nicht-Schlüssel**|+|+|+|  
|**Einzelner Schlüssel**|+|-|–|  
|**Mehrere Schlüssel**|+|–|+|  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Filter- und RecordCount Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
 [Filter- und RecordCount Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
 [Clear-Methode (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Dynamische Eigenschaft Optimize (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)
