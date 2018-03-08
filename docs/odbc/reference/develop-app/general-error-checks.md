---
title: "Allgemeine Fehlerprüfung | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- general error checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0c9a3425-0a7c-48de-9ff6-73601c26283e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b224d4df223d189e2532a7ed195ba6bfa9822b4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="general-error-checks"></a>Überprüfungen auf allgemeine Fehler
Der Treiber-Manager überprüft ein allgemeinen Fehler. Wird immer SQL_ERROR zurückgegeben, wenn den folgenden Fehler gefunden wird: die Funktion, die vom Treiber unterstützt werden muss.
