---
title: Auflisten von Argumenten Wert | Microsoft Docs
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
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47ef5564ae56f04877aa33b4ffb0f1644aa4d605
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="value-list-arguments"></a>Auflisten von Argumenten Wert
Eine Liste Wertargument besteht aus einer Liste mit durch Trennzeichen getrennten Werten, die für den Abgleich verwendet werden. Argument für nur einen einzigen Wert-Liste vorhanden ist, in der ODBC-Katalogfunktionen: die *TableType* Argument in **SQLTables**. Festlegen von *TableType* auf einen null-Zeiger ist identisch, als wäre er auf SQL_ALL_TABLE_TYPES, festgelegt ist, der alle verfügbaren Elemente der Werteliste aufgeführt. Dieses Argument ist das SQL_ATTR_METADATA_ID-Anweisungsattribut nicht betroffen. Weitere Informationen finden Sie unter der [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) funktionsbeschreibung.
