---
title: Durch Festlegen des Commitmodus | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45e975f0cb9ccc78a7cadd4f1a71b046528a9c10
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="setting-the-commit-mode"></a>Durch Festlegen des Commitmodus
Anwendungen Geben Sie den Transaktionsmodus mit das SQL_ATTR_AUTOCOMMIT-Verbindungsattribut. ODBC-Transaktionen werden standardmäßig im Autocommit Modus (es sei denn, **SQLSetConnectAttr** und **SQLSetConnectOption** werden nicht unterstützt, ist es unwahrscheinlich, dass). Der Wechsel von Manualcommit-Modus in den Autocommit-Modus automatisch führt einen Commit alle offenen Transaktionen für die Verbindung aus.
