---
title: "Gelöschte Befehle | Microsoft Docs"
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
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f3bf1ec522bee6fda19349a71c894ebd98bd75b9
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="set-deleted-command"></a>SET DELETED-Befehl
Gibt an, ob zum Löschen markierte Einträge verarbeitet werden, und gibt an, ob sie für die Verwendung in anderen Befehlen verfügbar sind.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>Argumente  
 ON  
 (Standard für den Treiber; der Standardwert für Visual FoxPro ist OFF). Gibt an, die Befehle, die ausgeführt werden (einschließlich der Datensätze in verknüpften Tabellen) Datensätze ein Bereich zum Löschen markierte Einträge ignoriert.  
  
 OFF  
 Gibt an, dass Datensätze markiert, für die Löschung von Befehlen zugegriffen werden kann, die Vorgänge an (einschließlich der Datensätze in verknüpften Tabellen) Datensätze mit einem Bereich.  
  
## <a name="remarks"></a>Hinweise  
 Fragt ab, dass verwenden (gelöscht), zum Testen des Status von Datensätzen mit Visual FoxPro-Rushmore-Technologie, wenn die Tabelle indiziert ist, auf die gelöschte () optimiert werden kann.  
  
> [!IMPORTANT]  
>  Legen Sie gelöscht wird ignoriert, wenn der Standardbereich für den Befehl zum aktuellen Datensatz ist oder wenn Sie einen Bereich eines einzelnen Datensatzes einschließen. INDEX immer ignoriert wird, legen Sie gelöscht und alle Datensätze in der Tabelle indiziert.  
  
## <a name="see-also"></a>Siehe auch  
 [Löschen - SQL-Befehl](../../odbc/microsoft/delete-sql-command.md)

