---
title: Append-Methode (ADO) | Microsoft Docs
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
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9a192286d39660580968305d16cb159480b6a09a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-ado"></a>Append-Methode (ADO)
Fügt ein Objekt für eine Sammlung an. Wenn die Auflistung [Felder](../../../ado/reference/ado-api/fields-collection-ado.md), ein neues [Feld](../../../ado/reference/ado-api/field-object.md) Objekt kann erstellt werden, bevor sie auf die Auflistung angefügt wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>Parameter  
 *collection*  
 Ein Auflistungsobjekt.  
  
 *fields*  
 Ein **Felder** Auflistung.  
  
 *Objekt*  
 Ein Object-Variablen, die das-Objekt anzufügenden darstellt.  
  
 *Name*  
 Ein **Zeichenfolge** -Wert, der den Namen der neuen enthält **Feld** -Objekt, und muss nicht der gleiche Namen wie jede andere Objekt in *Felder*.  
  
 *Typ*  
 Ein [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) Wert, dessen Standardwert **AdEmpty**, die den Datentyp des neuen Felds angibt. Die folgenden Datentypen werden nicht unterstützt, die für ADO und sollte nicht werden verwendet, wenn anfügen neuer Felder zu einer [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **AdIDispatch**, **AdIUnknown**, **AdVariant**.  
  
 *DefinedSize*  
 Optional. Ein **lange** Wert, der die definierte Größe in Zeichen oder Bytes, der das neue Feld darstellt. Der Standardwert für diesen Parameter abgeleitet *Typ*. Felder, denen ein *DefinedSize* größer als 255 Bytes als Spalten mit variabler Länge behandelt werden. Die Standardeinstellung für *DefinedSize* ist nicht angegeben.  
  
 *Attrib*  
 Optional. Ein [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md) Wert, dessen Standardwert **AdFldDefault**, die Attribute für das neue Feld angibt. Wenn dieser Wert nicht angegeben ist, enthält das Feld Attribute abgeleitet *Typ*.  
  
 *FieldValue*  
 Optional. Ein **Variant** , das der Wert für das neue Feld darstellt. Wenn nicht angegeben, wird das Feld einen null-Wert angefügt.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="parameters-collection"></a>Parameters-Auflistung  
 Müssen Sie festlegen der [Typ](../../../ado/reference/ado-api/type-property-ado.md) Eigenschaft eine [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekt vor dem Anfügen, damit die [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung. Wenn Sie einen Datentyp mit variabler Länge auswählen, müssen Sie auch Festlegen der [Größe](../../../ado/reference/ado-api/size-property-ado-parameter.md) Eigenschaft auf einen Wert größer als 0 (null).  
  
 Minimiert die Aufrufe an den Anbieter, und daher verbessert die Leistung bei der Verwendung von gespeicherten Prozeduren oder parametrisierte Abfragen, Parameter zu beschreiben. Allerdings müssen Sie wissen, die Eigenschaften der Parameter der gespeicherten Prozedur zugeordnet oder einer parametrisierten Abfrage, die Sie aufrufen möchten.  
  
 Verwenden Sie die [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) Methode zum Erstellen der **Parameter** Objekte mit dem entsprechenden eigenschafteneinstellungen und Verwenden der **Anfügen** Methode hinzugefügt der [ Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung. Dadurch können Sie die festzulegen und Parameterwerte zurückzugeben, ohne den Anbieter für die Parameterinformationen aufrufen. Wenn Sie an einen Anbieter, der keine Parameterinformationen bereitstellt schreiben, müssen Sie diese Methode verwenden, um manuell Auffüllen der **Parameter** Auflistung, um den Parameter verwenden.  
  
## <a name="fields-collection"></a>Fields-Auflistung  
 Die *FieldValue* Parameter ist nur gültig, beim Hinzufügen einer **Feld** -Objekt an eine [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) -Objekts können nicht für eine **Recordset** Objekt. Mit einem **Datensatz** -Objekt, Sie fügen Felder und Werte bereitstellen, zur gleichen Zeit. Mit einer **Recordset** Objekt ist, müssen Sie die Felder, die beim Erstellen der **Recordset** ist geschlossen, und öffnen Sie dann die **Recordset** und den Feldern Werte zugewiesen.  
  
> [!NOTE]
>  Für neue **Feld** Objekte, die angefügt wurden die **Felder** Auflistung von einer **Datensatz** -Objekt, das [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft muss festgelegt werden vor allen anderen **Feld** Eigenschaften können angegeben werden. Zunächst, einen bestimmten Wert für die **Wert** Eigenschaft zugewiesen und [Update](../../../ado/reference/ado-api/update-method.md) auf die **Felder** Auflistung aufgerufen. Klicken Sie dann, um andere Eigenschaften wie z. B. [Typ](../../../ado/reference/ado-api/type-property-ado.md) oder [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) zugegriffen werden kann. **Feld** Objekte der folgenden Datentypen (**DataTypeEnum**) kann nicht angefügt werden, um die **Felder** Auflistung und führt dazu, dass einen Fehler auftreten: **AdArray**, **AdChapter**, **AdEmpty**, **AdPropVariant**, und **AdUserDefined**. Darüber hinaus werden die folgenden Datentypen von ADO nicht unterstützt: **AdIDispatch**, **AdIUnknown**, und **AdIVariant**. Für diese Typen beim Anfügen fehlerfrei ausgeführt wird, sondern Verwendung kann zu unvorhersehbaren Ergebnissen einschließlich Speicherverluste erzeugen.  
  
## <a name="recordset"></a>Recordset  
 Wenn Sie nicht Festlegen der [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft vor dem Aufruf der **Anfügen** -Methode, **CursorLocation** festgelegt, um **AdUseClient** () eine [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) Wert) automatisch, wenn die [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) -Objekts aufgerufen wird.  
  
 Wird ein Laufzeitfehler auftreten, wenn der **Anfügen** Methode wird aufgerufen, auf der **Felder** Auflistung eines geöffneten **Recordset**, oder auf eine **Recordset** in dem die [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) Eigenschaft festgelegt wurde. Sie können nur Felder mit Anfügen einer **Recordset** , die nicht geöffnet ist und noch nicht mit einer Datenquelle verbunden. Dies ist normalerweise der Fall bei einer **Recordset** Objekt wird erstellt, mit der [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) Methode oder einer Objektvariablen zugewiesen.  
  
## <a name="record"></a>Aufzeichnung (Record)  
 Ein Laufzeitfehler nicht durchgeführt, falls die **Anfügen** Methode wird aufgerufen, auf die **Felder** Auflistung eines geöffneten **Datensatz**. Wird das neue Feld hinzugefügt werden die **Felder** Auflistung von der **Datensatz** Objekt. Wenn die **Datensatz** abgeleitet wurde eine **Recordset**, das neue Feld wird nicht angezeigt, der **Felder** Auflistung von der **Recordset** Objekt.  
  
 Ein nicht vorhandenes Feld erstellt und angefügt werden kann, die **Felder** Auflistung von Field-Objekt einen Wert zuweisen, als ob sie bereits in der Auflistung vorhanden waren. Die Zuweisung wird ausgelöst, die automatische Erstellung von und Anhängen von der **Feld** -Objekt, und klicken Sie dann die Zuweisung abgeschlossen werden.  
  
 Nach dem Anhängen ein **Feld** auf die **Felder** Auflistung von eine **Datensatz** -Objekt, rufen Sie die **Update** Methode der **Felder**  -Auflistung, um die Änderung zu speichern.  
  
## <a name="applies-to"></a>Gilt für  
  
- [Fields-Collection (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Parameters-Collection (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Anfügen und CreateParameter-Methoden (Beispiel) (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Anfügen und CreateParameter-Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter-Methode (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete-Methode (ADO Fields-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete-Methode (ADO-Parameters-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete-Methode (ADO-Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update-Methode](../../../ado/reference/ado-api/update-method.md)
