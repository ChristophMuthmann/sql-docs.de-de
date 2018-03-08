---
title: "Transaktionsunterstützung in DBMS | Microsoft Docs"
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
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b20cef18c97b0195bb42b687394bf3756a5f225
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="transaction-support-in-dbmss"></a>Transaktionsunterstützung in Datenbank-Managementsysteme
Einige Datenbanken, insbesondere Desktopdatenbanken wie z. B. Paradox, dBASE und Btrieve, unterstützen keine Transaktionen. Selbst zwischen Datenbanken, die Transaktionen unterstützen, gibt es Variante in welche Arten von SQL-Anweisungen in einer Transaktion werden können. Weitere Informationen finden Sie unter der Option SQL_TXN_CAPABLE in der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung.
