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
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- general error checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0c9a3425-0a7c-48de-9ff6-73601c26283e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6373b688a73c6de5d5612c978495509ee2dde5c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="general-error-checks"></a>Überprüfungen auf allgemeine Fehler
Der Treiber-Manager überprüft ein allgemeinen Fehler. Wird immer SQL_ERROR zurückgegeben, wenn den folgenden Fehler gefunden wird: die Funktion, die vom Treiber unterstützt werden muss.
