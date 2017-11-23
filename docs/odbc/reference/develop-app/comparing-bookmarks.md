---
title: Vergleichen von Lesezeichen | Microsoft Docs
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
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3d26095cf879859e6ea74784fcf87694ba5eb5d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="comparing-bookmarks"></a>Vergleichen von Lesezeichen
Da Lesezeichen Byte vergleichbar sind, können sie auf Gleichheit oder Ungleichheit verglichen werden. Zu diesem Zweck wird eine Anwendung jedes Lesezeichen behandelt, als ein Array von Bytes und vergleicht zwei Lesezeichen Byte für Byte. Da Lesezeichen garantiert nur innerhalb eines Resultsets unterscheiden, ist es nicht sinnvoll, Lesezeichen zu vergleichen, die aus verschiedenen Resultsets abgerufen wurden.
