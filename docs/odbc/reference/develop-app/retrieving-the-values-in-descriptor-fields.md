---
title: Zum Abrufen der Werte in Deskriptorfelder | Microsoft Docs
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8284167a27439c65256ee4559210843ec7dcffe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Die Werte in Deskriptorfeldern abrufen
Eine Anwendung kann Aufrufen **SQLGetDescField** zum Abrufen eines einzelnen Felds aus einem anwendungsparameterdeskriptor-Datensatz. **SQLGetDescField** erhält die Anwendungszugriff auf alle deskriptorfelder, die in ODBC definiert, oder auf Felder treiberdefinierten ebenfalls.  
  
 **SQLGetDescRec** aufgerufen werden, um die Einstellungen des mehrere deskriptorfelder, die den Datentyp auswirken und Speicherung von Spalten- oder Parameternamen Daten abzurufen.
