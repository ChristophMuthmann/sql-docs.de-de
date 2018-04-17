---
title: NICHT in CREATE TABLE-Anweisungen NULL | Microsoft Docs
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
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85f2b85208daef4645e519a743274ed6d8effab5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="not-null-in-create-table-statements"></a>NOT NULL in CREATE TABLE-Anweisungen
Einige Datenbanken und insbesondere Desktopdatenbanken unterstützen nicht die **NOT NULL** spalteneinschränkung in **CREATE TABLE** Anweisungen. Weitere Informationen finden Sie unter der Option SQL_NON_NULLABLE_COLUMNS in der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung.
