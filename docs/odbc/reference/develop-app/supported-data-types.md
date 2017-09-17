---
title: "Unterstützte Datentypen | Microsoft Docs"
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
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d76b98635cdc183f08f205374f8e7e0e66a4cb5f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="supported-data-types"></a>Unterstützte Datentypen
Die Datentypen, die vom DBMS unterstützt variieren erheblich. Eine Anwendung kann bestimmen, die Namen und die Eigenschaften der unterstützten Datentypen durch Aufrufen von **SQLGetTypeInfo**. Aufgrund der großen Unterschiede in Datentypnamen muss die Anwendung den Datentypnamen zurückgegebenes verwenden **SQLGetTypeInfo** in **CREATE TABLE** Anweisungen. Weitere Informationen finden Sie unter [Datentypen in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
