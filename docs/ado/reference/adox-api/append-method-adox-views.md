---
title: Append-Methode (ADOX Views) | Microsoft Docs
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
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 040e7d79a2c2fc30cc4782cf47f4b7d25733f692
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="append-method-adox-views"></a>Append-Methode (ADOX Ansichten)
Erstellt ein neues [Ansicht](../../../ado/reference/adox-api/view-object-adox.md) -Objekt und fügt es an die [Ansichten](../../../ado/reference/adox-api/views-collection-adox.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parameter  
 *Name*  
 Ein **Zeichenfolge** Wert, der den Namen des zu erstellenden Sicht angibt.  
  
 *Befehl*  
 Ein ADO [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt, das den zu erstellenden Sicht darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Erstellt eine neue Ansicht in der Datenquelle mit dem Namen und Attribute in der **Befehl** Objekt.  
  
 Wenn der Befehlstext, den angibt, der Benutzer eine Sicht, sondern eine Prozedur darstellt, ist das Verhalten vom Anbieter abhängig. **Append** schlägt fehl, wenn der Anbieter keine persistenten Befehle unterstützt.  
  
> [!NOTE]
>  Bei Verwendung des OLE DB-Anbieters für Microsoft Jet, der **Ansichten** Auflistung **Anfügen** Methode ermöglicht Ihnen die Angabe einer **Prozedur** anstelle eines **anzeigen**  in der *Befehl* Parameter. Die **Prozedur** wird an die Datenquelle hinzugefügt werden und werden hinzugefügt, um die **Ansichten** Auflistung. Nach der **Append**, wenn die **Prozeduren** und **Ansichten** Sammlungen werden aktualisiert, die **Prozedur** werden nicht mehr in der **Ansichten** Auflistung und erscheint der **Prozeduren** Auflistung.  
  
## <a name="applies-to"></a>Gilt für  
 [Views-Auflistung (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Ansichten Append-Methode (Beispiel) (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append-Methode (ADOX-Spalten)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append-Methode (ADOX-Gruppen)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append-Methode (ADOX Indizes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append-Methode (ADOX-Schlüssel)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append-Methode (ADOX Prozeduren)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append-Methode (ADOX-Tabellen)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append-Methode (ADOX-Benutzer)](../../../ado/reference/adox-api/append-method-adox-users.md)
