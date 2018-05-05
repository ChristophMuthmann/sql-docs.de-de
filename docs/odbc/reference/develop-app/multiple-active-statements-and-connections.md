---
title: Mehrere aktive Anweisungen und Verbindungen | Microsoft Docs
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
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b548b6d1b1aa7e7b260abcc9f507e2dbd566e7c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="multiple-active-statements-and-connections"></a>Mehrere aktive Anweisungen und Verbindungen
Einige Treiber und DBMS begrenzen die Anzahl der Anweisungen und Verbindungen, die gleichzeitig aktiv sein können. Diese Werte können so klein wie eine sein. Weitere Informationen finden Sie unter der SQL_MAX_CONCURRENT_ACTIVITIES und SQL_MAX_DRIVER_CONNECTIONS Optionen in der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung, und [Anweisung verarbeitet](../../../odbc/reference/develop-app/statement-handles.md) und [ Verbindungshandles](../../../odbc/reference/develop-app/connection-handles.md).
