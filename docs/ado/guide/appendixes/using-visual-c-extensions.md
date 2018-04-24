---
title: Verwenden von Visual C++-Erweiterungen | Microsoft Docs
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
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 80dd87f6946abc4cc37af7d75de6d36a8bb9980e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="visual-c-extensions"></a>Visual C++-Erweiterungen
## <a name="the-iadorecordbinding-interface"></a>Die IADORecordBinding-Schnittstelle
 Die Microsoft Visual C++-Erweiterungen für ADO zuordnen oder Bindung Felder einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt C/C++-Variablen. Wenn die Grenze der aktuellen Zeile **Recordset** ändert, die gebundenen Felder in der **Recordset** in die C/C++-Variablen kopiert werden. Bei Bedarf ist die kopierten Daten in den deklarierten Datentyp der C/C++-Variablen konvertiert.

 Die **BindToRecordset** Methode der **IADORecordBinding** Schnittstelle bindet Felder C/C++-Variablen. Die **AddNew** Methode fügt eine neue Zeile mit dem Grenzwert **Recordset**. Die **Update** Methode füllt die Felder in neue Zeilen von der **Recordset**, oder Felder in vorhandenen Zeilen mit dem Wert der C/C++-Variablen aktualisiert.

 Die **IADORecordBinding** Schnittstelle wird implementiert, indem Sie die **Recordset** Objekt. Sie die Implementierung nicht selbst code.

## <a name="binding-entries"></a>Binden von Einträgen
 Die Visual C++-Erweiterungen für ADO Zuordnen von Feldern von einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt C/C++-Variablen. Die Definition einer Zuordnung zwischen einem Feld und eine Variable wird aufgerufen, eine *binden Eintrag*. Makros bieten Bindungseinträge für numerische fester Länge und variabler Länge, die Daten an. Die Bindungseinträge und die C/C++-Variablen in von der Visual C++-Erweiterungen-Klasse abgeleitete Klasse deklariert **CADORecordBinding**. Die **CADORecordBinding** Klasse wird intern durch die Bindung Eintrag Makros definiert.

 ADO ordnet die Parameter in dieser Makros intern einen OLE DB- **DBBINDING** strukturieren und erstellt einen OLE DB- **Accessor** Objekt, um die Bewegung und die Konvertierung von Daten zwischen Felder und Variablen verwalten. OLE DB definiert Daten als besteht aus drei Teilen: ein *Puffer* , wo die Daten gespeichert werden; eine *Status* , der angibt, ob ein Feld erfolgreich im Puffer gespeichert wurde oder wie die Variable wiederhergestellt werden soll das Feld sein. und die *Länge* der Daten. (Siehe [abrufen und Einrichten von Daten (OLE DB)](http://msdn.microsoft.com/en-us/4369708b-c9fb-4d48-a321-bf949b41a369)in der OLE DB Programmer's Reference, Weitere Informationen.)

## <a name="header-file"></a>Header-Datei
 Schließen Sie die folgende Datei, in der Anwendung, um die Visual C++-Erweiterungen für ADO verwenden:

```
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>Binden von Recordset-Feldern

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>So binden Sie Recordset-Feldern an C/C++-Variablen

1.  Erstellen eine abgeleitete Klasse die **CADORecordBinding** Klasse.

2.  Geben Sie die Bindungseinträge für die und entsprechende C/C++-Variablen in der abgeleiteten Klasse. Die Bindungseinträge zwischen Klammer **BEGIN_ADO_BINDING** und **END_ADO_BINDING** Makros. Beenden Sie die Makros mit Kommas oder Semikolons nicht. Entsprechende Trennzeichen werden automatisch durch die einzelnen Makros angegeben.

     Geben Sie ein Bindungseintrag für jedes Feld eine C/C++-Variable zugeordnet werden. Verwenden Sie ein geeignetes Mitglied aus der **ADO_FIXED_LENGTH_ENTRY**, **ADO_NUMERIC_ENTRY**, oder **ADO_VARIABLE_LENGTH_ENTRY** Makros-Betriebssystemfamilie.

3.  In der Anwendung und erstellen Sie eine Instanz der abgeleiteten Klasse von **CADORecordBinding**. Abrufen der **IADORecordBinding** -Schnittstelle aus dem **Recordset**. Rufen Sie anschließend die **BindToRecordset** Methode zum Binden der **Recordset** Felder, die die C/C++-Variablen.

 Weitere Informationen finden Sie unter der [Visual C++-Erweiterungen-Beispiel](../../../ado/guide/appendixes/visual-c-extensions-example.md).

## <a name="interface-methods"></a>Schnittstellenmethoden
 Die **IADORecordBinding** Schnittstelle verfügt über drei Methoden: **BindToRecordset**, **AddNew**, und **Update**. Das einzige Argument für jede Methode ist ein Zeiger auf eine Instanz der abgeleiteten Klasse von **CADORecordBinding**. Aus diesem Grund die **AddNew** und **Update** Methoden können keine Parameter von der gleichen Namens ihre ADO-Methode angeben.

## <a name="syntax"></a>Syntax
 Die **BindToRecordset** Methode ordnet die **Recordset** Felder mit C/C++-Variablen.

```
BindToRecordset(CADORecordBinding *binding)
```

 Die **AddNew** Methode ruft die gleichnamige ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) Methode, um eine neue Zeile hinzufügen der **Recordset**.

```
AddNew(CADORecordBinding *binding)
```

 Die **aktualisieren** Methode ruft die gleichnamige ADO [aktualisieren](../../../ado/reference/ado-api/update-method.md) -Methode zum Aktualisieren der **Recordset**.

```
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>Binden von Eintrag-Makros
 Bindung Eintrag Makros definieren die Zuordnung von einem **Recordset** Feld und eine Variable. Ein Makro Anfangs- und Enddatumsangaben begrenzt die Reihe von bindungseinschränkungen Einträge.

 Familien des Makros werden für Daten mit fester Länge bereitgestellt, z. B. **AdDate** oder **AdBoolean**; numerischen Daten, z. B. **AdTinyInt**, **AdInteger**, oder **AdDouble**; und Daten mit variabler Länge, z. B. **AdChar**, **AdVarChar** oder **AdVarBinary**. Alle numerischen Typen, mit Ausnahme von **AdVarNumeric**, sind auch Typen mit fester Länge. Jede Familie hat unterschiedliche Sätze von Parametern, sodass Sie Bindungsinformationen ausschließen können, die nicht von Interesse ist.

 Weitere Informationen finden Sie unter [Anhang A: Datentypen](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6), von der OLE DB Programmer's Reference.

### <a name="begin-binding-entries"></a>Binden von Einträgen zu beginnen
 **BEGIN_ADO_BINDING**(*Klasse*)

### <a name="fixed-length-data"></a>Daten fester Länge
 **ADO_FIXED_LENGTH_ENTRY**(*Ordnungszahl, Datentyp, Puffer, den Status ändern*)

 **ADO_FIXED_LENGTH_ENTRY2**(*Ordnungszahl, Datentyp, Puffer ändern*)

### <a name="numeric-data"></a>Numerische Daten
 **ADO_NUMERIC_ENTRY**(*Ordnungszahl, Datentyp, Puffer, Genauigkeit, Dezimalstellen, Status ändern*)

 **ADO_NUMERIC_ENTRY2**(*Ändern der Ordnungszahl "," DataType "," Puffer "," Precision, Scale,*)

### <a name="variable-length-data"></a>Daten variabler Länge
 **ADO_VARIABLE_LENGTH_ENTRY**(*Ordnungszahl, Datentyp, Puffer, Größe, Status, Länge ändern*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*Ordnungszahl, Datentyp, Puffer, Größe, den Status ändern*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*ändern Ordnungszahl, Datentyp, Puffer, Größe, Länge,*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*Ordnungszahl, Datentyp, Puffer, Größe, ändern*)

### <a name="end-binding-entries"></a>Binden Einträge Ende
 **END_ADO_BINDING**()

|Parameter|Description|
|---------------|-----------------|
|*Class*|Klasse, die in dem die Bindungseinträge und die C/C++-Variablen definiert werden.|
|*Ordinal*|Ordnungszahl, beginnend mit 1, der die **Recordset** Feld, das die C/C++-Variable entspricht.|
|*DataType*|Entsprechende ADO-Datentyp, der die C/C++-Variable (finden Sie unter [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) eine Liste gültiger Datentypen). Der Wert, der die **Recordset** Feld wird in diesen Datentyp konvertiert werden, bei Bedarf.|
|*Buffer*|Name der C/C++-Variablen, in denen die **Recordset** Feld gespeichert werden.|
|*Größe*|Maximale Größe in Byte der *Puffer*. Wenn *Puffer* enthält eine Zeichenfolge variabler Länge Platz für ein abschließendes NULL zulassen.|
|*Status*|Name einer Variablen, die angibt, ob der Inhalt des *Puffer* gültig sind, und gibt an, ob die Konvertierung des Felds, das *DataType* war erfolgreich.<br /><br /> Die beiden wichtigsten Werte für diese Variable sind **AdFldOK**, was bedeutet, dass die Konvertierung war erfolgreich, und **AdFldNull**, was bedeutet, dass den Wert des Felds wäre eine Variante des Typs VT_NULL und nicht nur leer.<br /><br /> Mögliche Werte für *Status* sind aufgeführt, in der nächsten Tabelle, "Statuswerte".|
|*Ändern*|Boolesches Flag; Wenn TRUE, gibt ADO ist zulässig, zum Aktualisieren der entsprechenden **Recordset** Feld mit dem Wert in *Puffer*.<br /><br /> Die mit einem booleschen Wert *ändern* Parameter auf "true", Aktivieren von ADO, um dem gebundenen Feld zu aktualisieren, und "false", wenn Sie den überprüfen, jedoch nicht ändern möchten.|
|*Genauigkeit*|Anzahl der Ziffern, die in einer numerischen Variablen dargestellt werden können.|
|*Dezimalstellen*|Die Anzahl der Dezimalstellen in einer numerischen Variablen.|
|*Länge*|Name einer 4-Byte-Variablen, die die tatsächliche Länge der Daten in enthält *Puffer*.|

## <a name="status-values"></a>Statuswerte
 Der Wert, der die *Status* Variable gibt an, ob ein Feld in einer Variablen erfolgreich kopiert wurde.

 Beim Festlegen der Daten, *Status* kann festgelegt werden, um **AdFldNull** an, dass die **Recordset** Feld sollte festgelegt werden auf Null.

|Konstante|Wert|Description|
|--------------|-----------|-----------------|
|**adFldOK**|0|Ein Wert ungleich Null-Felds wurde zurückgegeben.|
|**adFldBadAccessor**|1|Bindung war ungültig.|
|**adFldCantConvertValue**|2|Wert konnte nicht für Datenüberlaufs Konflikt oder Daten konvertiert werden.|
|**adFldNull**|3|Gibt an, dass ein null-Wert zurückgegeben wurde, beim Abrufen eines Felds.<br /><br /> Wenn Sie ein Feld festlegen, gibt an, das Feld sollte festgelegt werden, um **NULL** Wenn das Feld kann nicht codiert **NULL** selbst (z. B. ein Array von Zeichen oder eine ganze Zahl).|
|**adFldTruncated**|4|Daten variabler Länge oder numerische Zeichen abgeschnitten wurden.|
|**adFldSignMismatch**|5|Wert ist signiert und Datentyp der Variablen ohne Vorzeichen.|
|**adFldDataOverFlow**|6|Wert ist größer als die in den Datentyp der Variablen gespeichert werden können.|
|**adFldCantCreate**|7|Unbekannter Spaltentyp und Feld bereits geöffnet.|
|**adFldUnavailable**|8|Feldwert konnte nicht bestimmt werden – z. B. auf ein neues, nicht zugewiesene Feld verfügt über keinen Standardwert.|
|**adFldPermissionDenied**|9|Bei der Aktualisierung nicht berechtigt, Daten zu schreiben.|
|**adFldIntegrityViolation**|10|Bei der Aktualisierung würde Feldwert Spaltenintegrität verletzen.|
|**adFldSchemaViolation**|11|Bei der Aktualisierung würde Spaltenschemas Feldwert verletzt werden.|
|**adFldBadStatus**|12|Beim Aktualisieren von ungültigen Status-Parameter.|
|**adFldDefault**|13|Bei der Aktualisierung wurde ein Standardwert verwendet.|

## <a name="see-also"></a>Siehe auch
 [Visual C++-Erweiterungen-Beispiel](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual C++-Erweiterungen-Header](../../../ado/guide/appendixes/visual-c-extensions-header.md)
