---
title: Unterstützte Datentypen | Microsoft Docs
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
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b11c3df36ba36153f71721d9a10dee702ef745d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="supported-data-types"></a>Unterstützte Datentypen
Die Datentypen, die vom DBMS unterstützt variieren erheblich. Eine Anwendung kann bestimmen, die Namen und die Eigenschaften der unterstützten Datentypen durch Aufrufen von **SQLGetTypeInfo**. Aufgrund der großen Unterschiede in Datentypnamen muss die Anwendung den Datentypnamen zurückgegebenes verwenden **SQLGetTypeInfo** in **CREATE TABLE** Anweisungen. Weitere Informationen finden Sie unter [Datentypen in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
