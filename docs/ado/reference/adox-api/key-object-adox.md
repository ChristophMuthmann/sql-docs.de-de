---
title: Key-Objekt (ADOX) | Microsoft Docs
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
f1_keywords: Key
helpviewer_keywords: Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea650d8389cee45e040db561948990ceb3701754
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="key-object-adox"></a>Schlüsselobjekt (ADOX)
Stellt eine primäre, Fremdschlüssel oder eindeutigen Schlüsselfeld aus einer Datenbanktabelle dar.  
  
## <a name="remarks"></a>Hinweise  
 Der folgende Code erstellt ein neues **Schlüssel**:  
  
```  
Dim obj As New Key  
```  
  
 Mit den Eigenschaften und Auflistungen von einer **Schlüssel** -Objekt können Sie:  
  
-   Identifizieren Sie den Schlüssel mit dem [Namen](../../../ado/reference/adox-api/name-property-adox.md) Eigenschaft.  
  
-   Bestimmen, ob die primäre, Fremdschlüssel oder eindeutig ist die [Typ](../../../ado/reference/adox-api/type-property-key-adox.md) Eigenschaft.  
  
-   Zugreifen auf die Datenbankspalten des Schlüssels mit der [Spalten](../../../ado/reference/adox-api/columns-collection-adox.md) Auflistung.  
  
-   Geben Sie den Namen der verknüpften Tabelle mit den [RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md) Eigenschaft.  
  
-   Bestimmen Sie die Aktion auf Löschen oder Aktualisieren eines primären Schlüssels mit dem [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) und [UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md) Eigenschaften.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Key-Objekt – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Append-Keys-Methode, Typ des Schlüssels, RelatedColumn, RelatedTable und UpdateRule Eigenschaften Beispiel (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Columns-Auflistung (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Keys Collection (ADOX) (Keys-Auflistung (ADOX))](../../../ado/reference/adox-api/keys-collection-adox.md)
