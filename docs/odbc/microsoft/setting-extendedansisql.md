---
title: Festlegen von ExtendedAnsiSQL | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d36c9462f2525930d8f3943461593bc3f51a95e1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setting-extendedansisql"></a>Festlegen von ExtendedAnsiSQL
Das Attribut kann in der Verbindungszeichenfolge durch Hinzufügen des Attributs ExtendedAnsiSQL gesteuert werden:  
  
|Wert|Description|  
|-----------|-----------------|  
|ExtendedAnsiSQL = 0 (Standard)|Diese Einstellung wird die neuen Funktionen nicht aktiviert.|  
|ExtendedAnsiSQL = 1|Diese Einstellung aktiviert die neuen Features.|  
  
 Das Attribut kann auch festgelegt werden, in einem DSN durch die **erweiterte Optionen** (Dialogfeld), wenn Sie einen DSN über die Systemsteuerung konfigurieren.  
  
 Dem Attribut festlegen auf 0 deaktiviert die neuen Funktionen; der Wert 1 aktiviert die neuen Features.  
  
 Das Attribut kann auch mit SQLSetConnectAttr() festgelegt werden. Der Attributwert ist 65501 und eine SQLINTEGER-Wert von 1 oder 0 (null) festgelegt ist, wie in der obigen Tabelle beschrieben. Es kann vor oder nach dem Herstellen einer Verbindung aufgerufen werden, aber es ist besser, rufen sie nach dem Herstellen einer Verbindung aufgrund der Reihenfolge, in der der Treiber Prozesse Verbindungsattribute und Verbindungszeichenfolgen zwischengespeichert.
