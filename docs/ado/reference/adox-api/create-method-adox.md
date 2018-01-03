---
title: Create-Methode (ADOX) | Microsoft Docs
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
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords: Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cb1e3dfcf4152060c5828133444ec72ce0994249
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="create-method-adox"></a>Create-Methode (ADOX)
Wird einen neuen Katalog erstellt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>Parameter  
 *ConnectString*  
 Ein **Zeichenfolge** Wert für die Verbindung mit der Datenquelle verwendet.  
  
## <a name="remarks"></a>Hinweise  
 Die **erstellen** Methode erstellt und öffnet ein neues ADO- [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) mit der Datenquelle, die im angegebenen *ConnectString*. Bei erfolgreicher Ausführung der neuen **Verbindung** Objekt zugewiesen ist die [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) Eigenschaft.  
  
 Wenn der Anbieter das Erstellen neuer Kataloge nicht unterstützt wird, tritt ein Fehler auf.  
  
## <a name="applies-to"></a>Gilt für  
 [Katalogobjekt (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Create-Methode-Beispiel (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [ActiveConnection-Eigenschaft (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
