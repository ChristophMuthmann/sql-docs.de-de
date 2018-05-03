---
title: ChangePassword-Methode (ADOX) | Microsoft Docs
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
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce933eb04cfa830696f69f13fdb36c6eacc83c55
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="changepassword-method-adox"></a>ChangePassword-Methode (ADOX)
Ändert das Kennwort für ein [Benutzer](../../../ado/reference/adox-api/user-object-adox.md) Konto.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parameter  
 *OldPassword*  
 Ein **Zeichenfolge** Wert, der das Kennwort des Benutzers vorhandenen angibt. Wenn der Benutzer aktuell nicht über ein Kennwort verfügt, verwenden Sie eine leere Zeichenfolge ("") für *OldPassword*.  
  
 *NewPassword*  
 Ein **Zeichenfolge** Wert, der das neue Kennwort angibt.  
  
## <a name="remarks"></a>Hinweise  
 Aus Sicherheitsgründen muss das alte Kennwort zusätzlich zu dem neuen Kennwort angegeben werden.  
  
 Es wird eine Fehlermeldung angezeigt, wenn der Anbieter die Verwaltung von Vertrauensnehmer Eigenschaften nicht unterstützt.  
  
## <a name="applies-to"></a>Gilt für  
 [User-Objekt (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Groups and Users Append, ChangePassword Methods Example (VB) (Gruppen und Benutzer – Append-, ChangePassword-Methode – Beispiele (VB))](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
