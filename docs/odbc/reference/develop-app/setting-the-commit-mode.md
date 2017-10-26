---
title: Durch Festlegen des Commitmodus | Microsoft Docs
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
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6d0c38d70b859b1fb986ebaa366a5396159a95da
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-commit-mode"></a>Durch Festlegen des Commitmodus
Anwendungen Geben Sie den Transaktionsmodus mit das SQL_ATTR_AUTOCOMMIT-Verbindungsattribut. ODBC-Transaktionen werden standardmäßig im Autocommit Modus (es sei denn, **SQLSetConnectAttr** und **SQLSetConnectOption** werden nicht unterstützt, ist es unwahrscheinlich, dass). Der Wechsel von Manualcommit-Modus in den Autocommit-Modus automatisch führt einen Commit alle offenen Transaktionen für die Verbindung aus.

