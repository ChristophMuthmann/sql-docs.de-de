---
title: MSSQLSERVER_102 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 8be7bf223e9c7aa323919488e5a70b7331493209
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver102"></a>MSSQLSERVER_102
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
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
  
