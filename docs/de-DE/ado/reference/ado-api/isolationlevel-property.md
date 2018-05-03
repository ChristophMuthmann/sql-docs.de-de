---
title: IsolationLevel-Eigenschaft | Microsoft Docs
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
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 326f145da9c2e80b7f4765a0c4bae1a657f4ee25
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="isolationlevel-property"></a>IsolationLevel-Eigenschaft
Gibt die Ebene der Isolation für eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt eine [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) Wert. Die Standardeinstellung ist **AdXactReadCommitted**.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **IsolationLevel** die Isolation der festzulegenden Eigenschaft eine **Verbindung** Objekt. Die Einstellung wird wirksam, bis zum nächsten Aufruf der [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) Methode. Wenn die Ebene der Isolation, die Sie anfordern, nicht verfügbar ist, kann der Anbieter das größere Potenzial der Isolation zurückgegeben, ohne Aktualisierung der **IsolationLevel** Eigenschaft.  
  
 Die **IsolationLevel** Eigenschaft gilt Lese-/Schreibzugriff.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** bei Verwendung für eine clientseitige **Verbindung** -Objekt, das **IsolationLevel** Eigenschaft kann nur festgelegt werden **AdXactUnspecified**. Da Benutzer mit nicht verbundenen arbeiten **Recordset** Objekte für einen clientseitigen Cache können Sie mehrere Benutzer gezwungen sein. Für die Instanz, wenn zwei verschiedene Benutzer versuchen, denselben Datensatz zu aktualisieren, kann Remote Data Service einfach der Benutzer, die zuerst den Datensatz aktualisiert "win" an. Die zweite Anforderung des Benutzers Update schlägt mit einem Fehler fehl.  
  
## <a name="applies-to"></a>Gilt für  
 [Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [IsolationLevel und Eigenschaften-Beispiel für Modus (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel und Modus Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
