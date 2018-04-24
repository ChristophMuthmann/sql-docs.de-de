---
title: AddNew-Methode (ADO) | Microsoft Docs
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
apitype: COM
f1_keywords:
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords:
- AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cee18a3fe0997243308dbb3bf71620ba5920adb6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="addnew-method-ado"></a>AddNew-Methode (ADO)
Erstellt einen neuen Datensatz für ein aktualisierbares [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>Parameter  
 *recordset*  
 Ein **Recordset** Objekt.  
  
 *FieldList*  
 Optional. Ein einzelner Name oder ein Array von Namen oder die Ordnungsposition der Felder im neuen Datensatz.  
  
 *Werte*  
 Optional. Ein einzelner Wert oder ein Array von Werten für die Felder im neuen Datensatz. Wenn *Fieldlist* ist ein Array *Werte* muss auch ein Array mit derselben Anzahl von Elementen ist andernfalls, ein Fehler auftritt. Die Reihenfolge von Feldnamen muss die Reihenfolge der Feldwerte in jedem Array entsprechen.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **AddNew** Methode zum Erstellen und initialisieren einen neuen Datensatz. Verwenden der [unterstützt](../../../ado/reference/ado-api/supports-method.md) Methode mit **AdAddNew** (eine [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) Wert) zu überprüfen, ob Sie Datensätze, mit dem aktuellen hinzufügen können **Recordset**Objekt.  
  
 Nach dem Aufruf der **AddNew** -Methode, der neue Datensatz wird zum aktuellen Datensatz und bleibt nach dem Aufruf von aktuellen der [Update](../../../ado/reference/ado-api/update-method.md) Methode. Da an der neue Datensatz angefügt wird die **Recordset**, einen Aufruf von **MoveNext** befolgen das Update wird das Ende verschoben der **Recordset**dadurch **EOF**  "True". Wenn die **Recordset** Objekt unterstützt keine Lesezeichen sind Sie möglicherweise nicht in der Lage, den neuen Datensatz zugreifen können, nachdem Sie zu einem anderen Datensatz wechseln. Abhängig vom Cursortyp, müssen Sie möglicherweise rufen die [Requery](../../../ado/reference/ado-api/requery-method.md) Methode zum Erstellen von neuen Datensatzes zugegriffen werden kann.  
  
 Beim Aufrufen **AddNew** beim Bearbeiten des aktuellen Datensatzes oder beim Hinzufügen eines neuen Datensatzes ADO Ruft die **Update** Methode zum Speichern ändert, und klicken Sie dann den neuen Eintrag erstellt.  
  
 Das Verhalten von der **AddNew** Methode hängt vom Aktualisierungsmodus von der **Recordset** -Objekt und gibt an, ob Sie übergeben die *Fieldlist* und *Werte*Argumente.  
  
 In *sofortupdatemodus* (in dem der Anbieter schreibt Änderungen in der zugrunde liegenden Datenquelle nach Aufrufen der **aktualisieren** Methode) wird beim Aufrufen der **AddNew** Methode ohne Argumente legt die [EditMode](../../../ado/reference/ado-api/editmode-property.md) Eigenschaft **AdEditAdd** (ein [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) Wert). Der Anbieter werden alle Feld Wert ändert sich lokal zwischengespeichert. Aufrufen der **Update** Methode wird der neue Datensatz in der Datenbank und setzt die **EditMode** Eigenschaft **AdEditNone** (ein **EditModeEnum**Wert). Wenn Sie übergeben die *Fieldlist* und *Werte* Argumente, ADO sofort wird der neue Datensatz in der Datenbank (keine **Update** Aufruf ist erforderlich); das **EditMode**  Eigenschaftswert ändert sich nicht (**AdEditNone**).  
  
 In *Update Batchmodus* (in dem der Anbieter speichert mehrere Änderungen und schreibt Sie sie in der zugrunde liegenden Datenquelle aus, nur bei Aufruf der [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode) wird beim Aufrufen der **AddNew** -Methode ohne Argumente legt die **EditMode** Eigenschaft **AdEditAdd**. Der Anbieter werden alle Feld Wert ändert sich lokal zwischengespeichert. Aufrufen der **Update** Methode fügt den neuen Eintrag mit dem aktuellen **Recordset**, aber der Anbieter nicht die Änderungen an der zugrunde liegenden Datenbank post oder Zurücksetzen der **EditMode** um **AdEditNone**, bis Sie rufen die **UpdateBatch** Methode. Wenn Sie übergeben die *Fieldlist* und *Werte* Argumente, ADO sendet den neuen Eintrag an den Anbieter für die Speicherung in einem Cache und legt die **EditMode** auf **AdEditAdd** ; aufrufen, müssen Sie die **UpdateBatch** Methode, um den neuen Eintrag der zugrunde liegenden Datenbank bereitstellen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird die Verwendung der AddNew-Methode mit der Feldliste und die Werteliste enthalten, um festzustellen, wie Sie die Feldliste und die Werteliste als Arrays enthalten.  
  
```  
create table aa1 (intf int, charf char(10))  
insert into aa1 values (2, 'aa')  
  
Dim cn As New adodb.Connection  
Dim rs As New adodb.Recordset  
Dim cmd As New adodb.Command  
  
cn.ConnectionString = "Provider=SQLOLEDB;Data Source=alexverb2;uid=sa;pwd=foo$bar00;"  
  
cn.Open  
rs.Open "select * from xxx..aa1", cn, adOpenKeyset, adLockOptimistic  
  
Dim fieldsArray(1) As Variant  
fieldsArray(0) = "intf"  
fieldsArray(1) = "charf"  
Dim values(1) As Variant  
values(0) = 4  
values(1) = "as"  
rs.AddNew fieldsArray, values  
rs.Update  
```  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [AddNew-Methode (Beispiel) (VB)](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [AddNew-Methode (Beispiel (VBScript)](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [AddNew-Methode (VC++-Beispiel)](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [CancelUpdate-Methode (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode-Eigenschaft](../../../ado/reference/ado-api/editmode-property.md)   
 [Requery-Methode](../../../ado/reference/ado-api/requery-method.md)   
 [Unterstützt-Methode](../../../ado/reference/ado-api/supports-method.md)   
 [Update-Methode](../../../ado/reference/ado-api/update-method.md)   
 [UpdateBatch-Methode](../../../ado/reference/ado-api/updatebatch-method.md)
