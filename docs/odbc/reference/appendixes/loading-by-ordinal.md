---
title: Laden nach Ordnungszahl | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d23eccad532e57b754e1305e1381613938cd6168
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="loading-by-ordinal"></a>Laden nach Ordnungszahl
In ODBC 2. *x*, laden nach Ordnungszahl konnte zur Verbesserung der Leistung des Verbindungsprozesses ausgeführt werden. Eine ODBC-2. *x* Treiber exportiert eine dummy-Funktion mit der Ordnungszahl 199; Wenn der Treiber-Manager erkannt wird, löst es die Adressen der ODBC-Funktionen, über die Ordnungszahl, nicht anhand des Namens. Diese Funktionalität ist weiterhin für ODBC 2. unterstützt. *x* Treiber für ODBC 3. nicht unterstützt wird, aber*.x* Treiber.
