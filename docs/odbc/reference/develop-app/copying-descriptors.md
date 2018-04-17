---
title: Kopieren die Deskriptoren | Microsoft Docs
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
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e135544e7cc54027c3f7b0e50ecd32cb4b0991a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="copying-descriptors"></a>Kopieren die Deskriptoren
Die **SQLCopyDesc** Funktion wird aufgerufen, um die Felder der einen Deskriptor mit einem anderen zu kopieren. Felder können nur für einen Deskriptor für die Anwendung oder einem IPD, jedoch nicht zu einer IRD kopiert werden. Felder können aus jeder Art von Deskriptor kopiert werden. Nur die Felder, die für die Quell- und Zielserver Deskriptoren definiert sind, werden kopiert. **SQLCopyDesc** Feld SQL_DESC_ALLOC_TYPE wird nicht kopiert werden, weil ein Deskriptor publicip-Zuweisungstyp geändert werden kann. Kopierte Felder überschreiben vorhandene Felder.  
  
 Ein ARD auf einem Anweisungshandle kann als APD auf ein anderes Anweisungshandle dienen. Dabei kann es sich um eine Anwendung so kopieren Sie die Zeilen zwischen Tabellen ohne Daten auf Anwendungsebene zu kopieren. Zu diesem Zweck wird eine Zeilendeskriptor, die eine abgerufene Zeile einer Tabelle wird beschrieben, die als eine Parameterdeskriptor für einen Parameter in einer INSERT-Anweisung wiederverwendet. Der Typ der SQL_MAX_CONCURRENT_ACTIVITIES Informationen muss größer als 1 ist für diesen Vorgang erfolgreich ausgeführt werden kann.
