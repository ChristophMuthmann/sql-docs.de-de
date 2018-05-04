---
title: Typen von Sperren | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AdLockBatchOptimistic [ADO]
- AdLockReadOnly [ADO]
- AdLockUnspecified [ADO]
- locks [ADO], types
- AdLockOptimistic [ADO]
- AdLockPessimistic [ADO]
ms.assetid: 12a978c0-b8a0-4ef0-87f0-a43c13659272
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f20cb8bb9344b107a32f29aa2a9a9f83206ccaf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="types-of-locks"></a>Typen von Sperren
## <a name="adlockbatchoptimistic"></a>adLockBatchOptimistic  
 Gibt die vollständige BatchUpdates an. Für Batchmodus-Update erforderlich.  
  
 Viele Anwendungen eine Anzahl von Zeilen auf einmal abrufen und koordinierte Aktualisierungen vornehmen, die den gesamten Satz von Zeilen, die eingefügt, aktualisiert oder gelöscht werden, enthalten müssen. Mit Batchcursorn, nur ein Roundtrip zum Server erforderlich ist, damit die Update-Leistung verbessern und den Netzwerkverkehr zu verringern. Eine Batch-Cursorbibliothek können Sie einen statischen Cursor erstellen und trennt dann die Datenquelle. An diesem Punkt können nehmen Sie Änderungen an den Zeilen und nachfolgend erneut eine Verbindung herstellen und die Änderungen an die Datenquelle in einem Batch bereitstellen.  
  
## <a name="adlockoptimistic"></a>adLockOptimistic  
 Gibt an, dass der Anbieter optimistischen Sperre verwendet – Sperren von Datensätzen nur bei Aufruf der **Update** Methode. Dies bedeutet, dass es besteht die Möglichkeit, dass ein anderer Benutzer die Daten zwischen der Zeit ändern können Sie den Datensatz und beim Aufruf bearbeiten **Update**, wodurch Konflikte erstellt. Verwenden Sie diesen Sperre in Situationen, in denen die Wahrscheinlichkeit zu einem Konflikt mit niedriger sind, oder, in denen Konflikte leicht aufgelöst werden können.  
  
## <a name="adlockpessimistic"></a>adLockPessimistic  
 Gibt das pessimistische Sperren, Datensatz nach dem anderen an. Der Anbieter unterstützt, was erforderlich ist, um sicherzustellen, dass erfolgreiche Bearbeitung der Datensätze in der Regel durch Sperren von Datensätzen in der Datenquelle unmittelbar vor der Bearbeitung ist. Natürlich, dies bedeutet, dass die Datensätze nicht für andere Benutzer verfügbar, sind Nachdem Sie beginnen, bis die Sperre durch den Aufruf zu bearbeiten, **Update.** Verwenden Sie diesen Typ der Sperre in einem System, auf dem nicht Sie leisten gleichzeitige Änderungen an Daten, z. B. einer Reservierung des Systems haben.  
  
## <a name="adlockreadonly"></a>adLockReadOnly  
 Gibt an, nur-Lese Datensätze. Sie können die Daten nicht ändern. Eine nur-Lese Sperre ist der "schnellste" Typ der Sperre, da es nicht, dass der Server erfordert, um eine Sperre für die Datensätze zu verwalten.  
  
## <a name="adlockunspecified"></a>adLockUnspecified  
 Gibt einen Typ von Sperre keine.
