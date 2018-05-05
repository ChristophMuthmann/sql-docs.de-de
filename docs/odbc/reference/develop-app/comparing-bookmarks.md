---
title: Vergleichen von Lesezeichen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cb844592d47e46a38f431f0127845583b82498a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="comparing-bookmarks"></a>Vergleichen von Lesezeichen
Da Lesezeichen Byte vergleichbar sind, können sie auf Gleichheit oder Ungleichheit verglichen werden. Zu diesem Zweck wird eine Anwendung jedes Lesezeichen behandelt, als ein Array von Bytes und vergleicht zwei Lesezeichen Byte für Byte. Da Lesezeichen garantiert nur innerhalb eines Resultsets unterscheiden, ist es nicht sinnvoll, Lesezeichen zu vergleichen, die aus verschiedenen Resultsets abgerufen wurden.
