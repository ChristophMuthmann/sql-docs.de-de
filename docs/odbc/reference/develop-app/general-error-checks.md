---
title: Allgemeine Fehlerprüfung | Microsoft Docs
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
- diagnostic information [ODBC], driver manager error checking
- general error checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0c9a3425-0a7c-48de-9ff6-73601c26283e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3de7754a44034805c0b9f4c7784d6610eed5a1d6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="general-error-checks"></a>Überprüfungen auf allgemeine Fehler
Der Treiber-Manager überprüft ein allgemeinen Fehler. Wird immer SQL_ERROR zurückgegeben, wenn den folgenden Fehler gefunden wird: die Funktion, die vom Treiber unterstützt werden muss.
