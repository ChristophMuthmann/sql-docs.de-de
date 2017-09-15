---
title: Laden nach Ordnungszahl | Microsoft Docs
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
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ef22486a7cbd9932c90069f461b83358c2db8fd4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="loading-by-ordinal"></a>Laden nach Ordnungszahl
In ODBC 2. *x*, laden nach Ordnungszahl konnte zur Verbesserung der Leistung des Verbindungsprozesses ausgeführt werden. Eine ODBC-2. *x* Treiber exportiert eine dummy-Funktion mit der Ordnungszahl 199; Wenn der Treiber-Manager erkannt wird, löst es die Adressen der ODBC-Funktionen, über die Ordnungszahl, nicht anhand des Namens. Diese Funktionalität ist weiterhin für ODBC 2. unterstützt. *x* Treiber für ODBC 3. nicht unterstützt wird, aber*.x* Treiber.
