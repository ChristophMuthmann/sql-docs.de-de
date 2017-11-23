---
title: Cursor und die Sperre Merkmale | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84f06591c70a42701ca264c99af00e4f072aadd0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="cursor-and-lock-characteristics"></a>Cursor und Merkmale der Sperre
Während die Merkmale eines Cursors Funktionen des Anbieters abhängig, gelten sich die folgenden vor- und Nachteile im Allgemeinen für die verschiedenen Typen von Cursorn und sperren.  
  
|Cursor-oder Sperrtyp|Vorteile|Nachteile|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|– Ressourcenanforderungen niedrig|-Kann nicht rückwärts scrollen<br />– Keine Datenparallelität|  
|**adOpenStatic**|-Bildlauffähigen|– Keine Datenparallelität|  
|**adOpenKeyset**|-Für einige Datenparallelität<br />-Bildlauffähigen|-Höheren Ressourcenbedarf<br />-Nicht verfügbar in abgetrennten Szenario|  
|**adOpenDynamic**|-Hohe Datenparallelität<br />-Bildlauffähigen|-Die höchsten Anforderungen von Infrastrukturressourcen<br />-Nicht verfügbar in abgetrennten Szenario|  
|**adLockReadOnly**|– Ressourcenanforderungen niedrig<br />-Hochgradig skalierbarer|-Daten durch Cursor nicht aktualisiert.|  
|**adLockBatchOptimistic**|-Batch updates<br />– Ermöglicht es getrennten Szenarios<br />– Andere Benutzer auf Daten zugreifen.|-Daten können von mehreren Benutzern gleichzeitig geändert werden|  
|**adLockPessimistic**|-Daten können nicht von anderen Benutzern gesperrten geändert werden|-Verhindert, dass andere Benutzer den Zugriff auf Daten gesperrt ist|  
|**adLockOptimistic**|– Andere Benutzer auf Daten zugreifen.|-Daten können von mehreren Benutzern gleichzeitig geändert werden|
