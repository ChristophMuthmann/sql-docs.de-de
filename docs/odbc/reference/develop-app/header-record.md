---
title: Headerdatensatz | Microsoft Docs
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
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea43540c17449f4163f1f51450674774a6d220e1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="header-record"></a>Headerdatensatz
Die Felder im Headerdatensatz enthalten allgemeine Informationen über die Ausführung einer Funktion, einschließlich Rückgabecode, Zeilenanzahl, Anzahl der Statusdatensätze und Typ der ausgeführten Anweisung. Der Headerdatensatz wird immer erstellt, es sei denn, die Funktion gibt SQL_INVALID_HANDLE zurück. Eine vollständige Liste der Felder im Headerdatensatz, finden Sie unter der [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) funktionsbeschreibung.
