---
title: Append-Methode (ADOX Prozeduren) | Microsoft Docs
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
- Procedures::Append
- Procedures::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 38e3492c-c1e1-42e3-a71a-befdc90204db
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5a0974d3b6de9b1f8abfe61d9883aa60a4326c0a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="append-method-adox-procedures"></a>Append-Methode (ADOX Prozeduren)
Fügt ein neues [Prozedur](../../../ado/reference/adox-api/procedure-object-adox.md) -Objekt an die [Prozeduren](../../../ado/reference/adox-api/procedures-collection-adox.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Procedures.Append Name, Command  
```  
  
#### <a name="parameters"></a>Parameter  
 *Name*  
 Ein **Zeichenfolge** Wert, der den Namen der Prozedur, die erstellt oder ergänzt angibt.  
  
 *Befehl*  
 Ein ADO [Befehl](../../../ado/reference/ado-api/command-object-ado.md) -Objekt, das Verfahren zum Erstellen und Anfügen darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Erstellt eine neue Prozedur in der Datenquelle mit dem Namen und Attribute in der **Befehl** Objekt.  
  
 Wenn der Befehlstext, den der Benutzer gibt eine Ansicht anstatt in eine Prozedur darstellt, ist das Verhalten von den verwendeten Anbieter abhängig. **Append** schlägt fehl, wenn der Anbieter keine persistenten Befehle unterstützt.  
  
> [!NOTE]
>  Bei Verwendung des OLE DB-Anbieters für Microsoft Jet, der **Prozeduren** Auflistung **Anfügen** Methode ermöglicht Ihnen die Angabe einer **Ansicht** anstelle eines  **Prozedur** in der *Befehl* Parameter. Die **Ansicht** wird an die Datenquelle hinzugefügt werden und werden hinzugefügt, um die **Prozeduren** Auflistung. Nach der **Append**, wenn die **Prozeduren** und **Ansichten** Sammlungen werden aktualisiert, die **Ansicht** werden nicht mehr in der **Prozeduren** Auflistung und erscheint der **Ansichten** Auflistung.  
  
## <a name="applies-to"></a>Gilt für  
 [Procedures Collection (ADOX) (Procedures-Auflistung (ADOX))](../../../ado/reference/adox-api/procedures-collection-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Prozeduren Append-Methode (Beispiel) (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Append-Methode (ADOX-Spalten)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append-Methode (ADOX-Gruppen)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append-Methode (ADOX Indizes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append-Methode (ADOX-Schlüssel)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append-Methode (ADOX-Tabellen)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append-Methode (ADOX-Benutzer)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append-Methode (ADOX-Ansichten)](../../../ado/reference/adox-api/append-method-adox-views.md)
