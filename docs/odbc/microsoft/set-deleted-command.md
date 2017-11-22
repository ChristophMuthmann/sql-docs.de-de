---
title: "Gelöschte Befehle | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 34bcce12665dd3e0bcaa49e4c6e1ff93a807f514
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
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
 [DELETE (SQL-Befehl)](../../odbc/microsoft/delete-sql-command.md)
