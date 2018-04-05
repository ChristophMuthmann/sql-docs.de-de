---
title: Zum Abrufen der Werte in Deskriptorfelder | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 37efd70ccd8fa0ad5c6d4bb573eb1c158a3ec35b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Die Werte in Deskriptorfeldern abrufen
Eine Anwendung kann Aufrufen **SQLGetDescField** zum Abrufen eines einzelnen Felds aus einem anwendungsparameterdeskriptor-Datensatz. **SQLGetDescField** erhält die Anwendungszugriff auf alle deskriptorfelder, die in ODBC definiert, oder auf Felder treiberdefinierten ebenfalls.  
  
 **SQLGetDescRec** aufgerufen werden, um die Einstellungen des mehrere deskriptorfelder, die den Datentyp auswirken und Speicherung von Spalten- oder Parameternamen Daten abzurufen.
