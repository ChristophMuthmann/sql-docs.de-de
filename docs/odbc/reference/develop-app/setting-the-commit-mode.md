---
title: Durch Festlegen des Commitmodus | Microsoft Docs
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
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6d56a85716d88658c6e365484136460f7cce04b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setting-the-commit-mode"></a>Durch Festlegen des Commitmodus
Anwendungen Geben Sie den Transaktionsmodus mit das SQL_ATTR_AUTOCOMMIT-Verbindungsattribut. ODBC-Transaktionen werden standardmäßig im Autocommit Modus (es sei denn, **SQLSetConnectAttr** und **SQLSetConnectOption** werden nicht unterstützt, ist es unwahrscheinlich, dass). Der Wechsel von Manualcommit-Modus in den Autocommit-Modus automatisch führt einen Commit alle offenen Transaktionen für die Verbindung aus.
