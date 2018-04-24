---
title: Append-Methode (ADOX-Benutzer) | Microsoft Docs
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
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 267dbd8bc1eb05a1d0f56c9078c5f5518d1e38d7
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="append-method-adox-users"></a>Append-Methode (ADOX-Benutzer)
Fügt ein neues [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) -Objekt an die [Benutzer](../../../ado/reference/adox-api/users-collection-adox.md) Auflistung.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parameter  
 *Benutzer*  
 Ein **Variant** -Wert enthält das **Benutzer** anzufügende Objekt oder den Namen des Benutzers, der erstellt oder ergänzt.  
  
 *Kennwort*  
 Optional. Ein **Zeichenfolge** Wert, der das Kennwort für den Benutzer enthält. Die *Kennwort* Parameter den angegebenen Wert entspricht der [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) Methode eine **Benutzer** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Die **Benutzer** Auflistung von einem [Katalog](../../../ado/reference/adox-api/catalog-object-adox.md) Benutzer alle des Katalogs darstellt. Die **Benutzer** Auflistung für einen [Gruppe](../../../ado/reference/adox-api/group-object-adox.md) stellt nur die Benutzer, die eine Mitgliedschaft in der bestimmten Gruppe haben.  
  
 Es wird eine Fehlermeldung angezeigt, wenn der Anbieter beim Erstellen von Benutzern nicht unterstützt.  
  
> [!NOTE]
>  Vor dem Anfügen einer **Benutzer** -Objekt an die **Benutzer** Auflistung von eine **Gruppe** -Objekt, eine **Benutzer** Objekt mit dem gleichen [Name ](../../../ado/reference/adox-api/name-property-adox.md) wie die Vorlage zum anzufügenden im bereits vorhanden sind, muss die **Benutzer** Auflistung von der **Katalog**.  
  
## <a name="applies-to"></a>Gilt für  
 [Users-Auflistung (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Gruppen und Benutzer für anfügen, ChangePassword-Methoden (Beispiel) (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append-Methode (ADOX-Spalten)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append-Methode (ADOX-Gruppen)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append-Methode (ADOX Indizes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append-Methode (ADOX-Schlüssel)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append-Methode (ADOX Prozeduren)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append-Methode (ADOX-Tabellen)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append-Methode (ADOX-Ansichten)](../../../ado/reference/adox-api/append-method-adox-views.md)
