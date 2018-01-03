---
title: Sortieren Sie die Eigenschaft | Microsoft Docs
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
apitype: COM
f1_keywords:
- Recordset15::get_Sort
- Recordset15::put_Sort
- Recordset15::PutSort
- Recordset15::GetSort
- Recordset15::Sort
helpviewer_keywords:
- DESC [ADO]
- ASC [ADO]
- Sort property [ADO]
ms.assetid: 3683ffa0-6f93-4906-9533-ef6942f24f39
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e668f5d2644ece0fa9210bdb492fd37ca8089a8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sort-property"></a>Sort-Eigenschaft
Gibt einen oder mehrere Feldnamen, auf denen die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) sortiert ist, und gibt an, ob jedes Feld in aufsteigender oder absteigender Reihenfolge sortiert wird.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Zeichenfolge** Wert an das Feld den Namen der **Recordset** für die Sortierung. Jeder Name wird durch ein Komma getrennt und ist durch ein Leerzeichen und das Schlüsselwort optional gefolgt **ASC**, die das Feld in aufsteigender Reihenfolge sortiert oder **"DESC"**, die das Feld in absteigender Reihenfolge sortiert. In der Standardeinstellung Wenn kein Schlüsselwort angegeben ist, wird das Feld in aufsteigender Reihenfolge sortiert.  
  
## <a name="remarks"></a>Hinweise  
 Diese Eigenschaft ist erforderlich, die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft festgelegt werden, um **AdUseClient**. Ein temporärer Index wird für jedes Feld im angegebenen erstellt die **sortieren** Eigenschaft, wenn ein Index nicht bereits vorhanden ist.  
  
 Der Sortiervorgang ist effizient, da Daten nicht physisch neu angeordnet, sondern einfach in der Reihenfolge, die vom Index angegebenen zugegriffen wird.  
  
 Bei den Wert des der **sortieren** Eigenschaft ist etwas anderes als eine leere Zeichenfolge, die **sortieren** Eigenschaftenreihenfolge hat Vorrang vor der Reihenfolge im ein **ORDER BY** Klausel enthalten in der SQL-Anweisung, die zum Öffnen der **Recordset**.  
  
 Die **Recordset** muss nicht geöffnet werden, bevor der Zugriff auf die **sortieren** Eigenschafts-kann festgelegt werden, zu einem beliebigen Zeitpunkt nach der **Recordset** Objekt instanziiert wird.  
  
 Festlegen der **sortieren** Eigenschaft auf eine leere Zeichenfolge wird die Zeilen in der ursprünglichen Reihenfolge zurückgesetzt und temporäre Indizes zu löschen. Vorhandene Indizes werden nicht gelöscht werden.  
  
 Nehmen Sie an einer **Recordset** enthält drei Felder mit dem Namen *FirstName*, *MiddleInitial*, und *LastName*. Legen Sie die **sortieren** -Eigenschaft die Zeichenfolge "`lastName DESC, firstName ASC`", die Reihenfolge der **Recordset** nach dem Nachnamen in absteigender Reihenfolge aus, und klicken Sie dann nach Vornamen in aufsteigender Reihenfolge. Der Wert von MiddleInitial wird ignoriert.  
  
 Kein Feld kann den Namen "ASC" oder "DESC", da diese Namen in mit den Schlüsselwörtern Konflikt **ASC** und **"DESC"**. Sie können einen Alias für ein Feld mit einem in Konflikt stehende Namen erstellen, mit der **AS** Schlüsselwort in der Abfrage, die zurückgibt der **Recordset**.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Sortieren-Eigenschaft (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Sort-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimieren Sie die Eigenschaft dynamisch (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn-Eigenschaft (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection-Eigenschaft (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
