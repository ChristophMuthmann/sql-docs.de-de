---
title: Daten abschneiden Erkennung mit ExtendedAnsiSQL aktiviert | Microsoft Docs
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
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2704dac2cd6b3a64becf5592d082a0635243153c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Daten abschneiden Erkennung mit ExtendedAnsiSQL aktiviert
Wenn das Flag ExtendedAnsiSQL eingeschaltet ist und die Anwendung Daten in einer char- oder binary-Spalte eingefügt wird. und Daten abgeschnitten, wird das Abschneiden erkannt werden. Wenn das Flag ExtendedAnsiSQL deaktiviert ist, werden die Daten ohne Warnung abgeschnitten, wie dies in früheren Versionen der ODBC-Treiber für die Desktop-Datenbank war.
