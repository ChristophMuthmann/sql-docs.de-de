---
title: Auflisten von Argumenten Wert | Microsoft Docs
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
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67d18da9372c9d82a3847caf7d404d2894189f8d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="value-list-arguments"></a>Auflisten von Argumenten Wert
Eine Liste Wertargument besteht aus einer Liste mit durch Trennzeichen getrennten Werten, die für den Abgleich verwendet werden. Argument für nur einen einzigen Wert-Liste vorhanden ist, in der ODBC-Katalogfunktionen: die *TableType* Argument in **SQLTables**. Festlegen von *TableType* auf einen null-Zeiger ist identisch, als wäre er auf SQL_ALL_TABLE_TYPES, festgelegt ist, der alle verfügbaren Elemente der Werteliste aufgeführt. Dieses Argument ist das SQL_ATTR_METADATA_ID-Anweisungsattribut nicht betroffen. Weitere Informationen finden Sie unter der [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) funktionsbeschreibung.
