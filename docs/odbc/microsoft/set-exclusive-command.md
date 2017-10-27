---
title: EXKLUSIVE SET-Befehls | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 830cec1dbb87ae2bc4336d28d6112fd76b4db0ed
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="set-exclusive-command"></a>EXKLUSIVE SET-Befehl
Gibt an, ob die Tabellendateien für die exklusive oder gemeinsame Verwendung in einem Netzwerk geöffnet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argumente  
 ON  
 Grenzwerte für die Barrierefreiheit einer Tabelle in einem Netzwerk an den Benutzer, der er geöffnet geöffnet. Die Tabelle kann nicht an andere Benutzer im Netzwerk zugegriffen werden. SET exklusive ON verhindert, dass alle anderen Benutzer schreibgeschützten Zugriff verfügen.  
  
 OFF  
 (Standard für den Treiber, die Standardwerte für Visual FoxPro sind ON oder OFF die globalen Daten für eine Sitzung private Daten.) Kann eine Tabelle in einem Netzwerk freigegeben werden, und von jedem Benutzer im Netzwerk geändert geöffnet.  
  
## <a name="remarks"></a>Hinweise  
 Ändern der Einstellung der exklusive festlegen, nicht den Status des zuvor geöffneten Tabellen ändern. Wenn eine Tabelle, mit der EXKLUSIVEN festgelegt auf ON festgelegt geöffnet wird und exklusive festgelegt ist auf OFF später geändert, behält die Tabelle die exklusive Verwendung Status.  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-Visual FoxPro einrichten (Dialogfeld)](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)

