---
title: Zum Abrufen der Werte in Deskriptorfelder | Microsoft Docs
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f86dd2e2cb625da359c677fedd297b510fee8593
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Die Werte in Deskriptorfeldern abrufen
Eine Anwendung kann Aufrufen **SQLGetDescField** zum Abrufen eines einzelnen Felds aus einem anwendungsparameterdeskriptor-Datensatz. **SQLGetDescField** erhält die Anwendungszugriff auf alle deskriptorfelder, die in ODBC definiert, oder auf Felder treiberdefinierten ebenfalls.  
  
 **SQLGetDescRec** aufgerufen werden, um die Einstellungen des mehrere deskriptorfelder, die den Datentyp auswirken und Speicherung von Spalten- oder Parameternamen Daten abzurufen.
