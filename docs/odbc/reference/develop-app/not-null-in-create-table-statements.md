---
title: NICHT in CREATE TABLE-Anweisungen NULL | Microsoft Docs
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
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b1c2d2a96e12e09341d4bf34811bc7bcb6694e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="not-null-in-create-table-statements"></a>NOT NULL in CREATE TABLE-Anweisungen
Einige Datenbanken und insbesondere Desktopdatenbanken unterstützen nicht die **NOT NULL** spalteneinschränkung in **CREATE TABLE** Anweisungen. Weitere Informationen finden Sie unter der Option SQL_NON_NULLABLE_COLUMNS in der [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung.
