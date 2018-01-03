---
title: Property-Objekt (ADO) | Microsoft Docs
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
f1_keywords: Property
helpviewer_keywords: Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c43ea682cb6ca8e0dc7767cd0372fa258cea27db
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="property-object-ado"></a>Property-Objekt (ADO)
Stellt ein dynamisches Merkmal eines ADO-Objekts, das vom Anbieter definiert ist.  
  
## <a name="remarks"></a>Hinweise  
 ADO-Objekte sind zwei Eigenschaften: integrierte und dynamische.  
  
 Vordefinierte Eigenschaften sind diese Eigenschaften in ADO implementiert und sofort zur Verfügung, um eine neue Objekt mithilfe der `MyObject.Property` Syntax. Sie erscheinen nicht als **Eigenschaft** Objekte in einem Objekt [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) -Auflistung, damit auch deren Werte zu ändern, können Sie ihre Eigenschaften nicht ändern.  
  
 Dynamische Eigenschaften werden von der zugrunde liegende Datenanbieter definiert und werden in der **Eigenschaften** Auflistung für den entsprechenden ADO-Objekt. Beispielsweise kann eine Eigenschaft, die spezifisch für den Datenanbieter anzugeben, ob ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt unterstützt, Transaktionen oder aktualisieren. Diese zusätzlichen Eigenschaften hostnamensadresse **Eigenschaft** Objekte in diesem **Recordset** des Objekts **Eigenschaften** Auflistung. Dynamische Eigenschaften verwiesen werden können, nur über die Auflistung mit den `MyObject.Properties(0)` oder `MyObject.Properties("Name")` Syntax.  
  
 Beide Arten der Eigenschaft kann nicht gelöscht werden.  
  
 Eine dynamische **Eigenschaft** -Objekt hat vier integrierte Eigenschaften selbst:  
  
-   Die [Namen](../../../ado/reference/ado-api/name-property-ado.md) Eigenschaft ist eine Zeichenfolge, die die Eigenschaft identifiziert.  
  
-   Die [Typ](../../../ado/reference/ado-api/type-property-ado.md) Eigenschaft ist eine ganze Zahl, die den Datentyp der Eigenschaft angibt.  
  
-   Die [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft ist eine Variante, die die Einstellung der Eigenschaft enthält. **Wert** ist die Standardeigenschaft für ein **Eigenschaft** Objekt.  
  
-   Die [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) Eigenschaft ist ein long-Wert, der die Eigenschaften, die spezifisch für den Datenanbieter angibt.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Eigenschaft-Objekteigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
