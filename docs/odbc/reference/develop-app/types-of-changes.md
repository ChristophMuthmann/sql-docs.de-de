---
title: "Arten von Änderungen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7801d7bf8e7add5425ee6a8a97c4b1b17c556674
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="types-of-changes"></a>Arten von Änderungen
In ODBC 3. werden drei Arten von Änderungen vorgenommen. *x* (und alle ODBC-Version). Jede dieser wirkt sich unterschiedlich auf Abwärtskompatibilität und auf andere Weise behandelt wird. Diese Änderungen werden in der folgenden Tabelle beschrieben.  
  
|Art der Änderung|Description|  
|--------------------|-----------------|  
|Neue Funktionen|Hierbei handelt es sich um Funktionen, die ODBC 3. nicht vertraut sind. *x*, z. B. Out-of-Line-Bindung oder Deskriptoren. Diese werden nur, wenn die Anwendung und Treiber als auch der Treiber-Manager, Version 3 sind implementiert*.x*, sodass es nicht versucht wird, diese abwärts kompatibel zu machen.|  
|Doppelte Funktionen|Hierbei handelt es sich um Funktionen, die in ODBC 2.*.x* und ODBC 3.. *X* jedoch auf unterschiedliche Weise in den einzelnen implementiert werden. Die Funktionen **SQLAllocHandle** und **SQLAllocStmt:** sind ein Beispiel. Abwärtskompatibilität für diese Probleme und andere doppelten Funktionen größtenteils von Zuordnungen in der Treiber-Manager behandelt.|  
|Verhaltensänderungen|Hierbei handelt es sich um Funktionen, die in ODBC 2. unterschiedlich gehandhabt,*.x* und ODBC 3.. *X*. Eine "DateTime" **#define** ist ein Beispiel. Diese Funktionen werden durch die ODBC 3. verarbeitet. *x* Treiber basierend auf einem Attribut umgebungseinstellung. (Siehe [Verhaltensänderungen](../../../odbc/reference/develop-app/behavioral-changes.md) für Weitere Informationen.)|
