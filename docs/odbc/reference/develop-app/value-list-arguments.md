---
title: Auflisten von Argumenten Wert | Microsoft Docs
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
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a8386d5ffbb4d492bc8489272596fb9f6d58d245
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="value-list-arguments"></a>Auflisten von Argumenten Wert
Eine Liste Wertargument besteht aus einer Liste mit durch Trennzeichen getrennten Werten, die für den Abgleich verwendet werden. Argument für nur einen einzigen Wert-Liste vorhanden ist, in der ODBC-Katalogfunktionen: die *TableType* Argument in **SQLTables**. Festlegen von *TableType* auf einen null-Zeiger ist identisch, als wäre er auf SQL_ALL_TABLE_TYPES, festgelegt ist, der alle verfügbaren Elemente der Werteliste aufgeführt. Dieses Argument ist das SQL_ATTR_METADATA_ID-Anweisungsattribut nicht betroffen. Weitere Informationen finden Sie unter der [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) funktionsbeschreibung.
