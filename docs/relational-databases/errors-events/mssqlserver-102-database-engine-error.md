---
title: MSSQLSERVER_102 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3864da9f40dab1b0f796bf88e255c963b48a5539
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver102"></a>MSSQLSERVER_102
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|102|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|P_SYNTAXERR2|  
|Meldungstext|Falsche Syntax in der Nähe von '%.*ls'.|  
  
## <a name="explanation"></a>Erklärung  
Gibt einen Syntaxfehler an. Weitere Informationen sind nicht verfügbar, da der Fehler verhindert, dass das [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Anweisung verarbeitet.  
  
Eine mögliche Ursache ist, dass versucht wurde, mit der veralteten RC4- oder RC4_128-Verschlüsselung einen symmetrischen Schlüssel zu erstellen und der Kompatibilitätsmodus nicht auf 90 oder 100 festgelegt war.  
  
## <a name="user-action"></a>Benutzeraktion  
Suchen Sie in der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung nach Syntaxfehlern.  
  
Wenn Sie mit RC4 oder RC4_128 einen symmetrischen Schlüssel erstellen, wählen Sie eine neuere Verschlüsselung aus, z. B. einen der AES-Algorithmen. (Empfohlen.) Wenn RC4 erforderlich ist, verwenden Sie die Anweisung ALTER DATABASE SET COMPATIBILITY_LEVEL, um den Kompatibilitätsgrad der Datenbank auf 90 oder 100 festzulegen. (Nicht empfohlen.)  
  
