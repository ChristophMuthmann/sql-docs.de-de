---
title: Festlegen von Deskriptorfelder | Microsoft Docs
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
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5ea00d83f1f57498ee1094264c1895f50103526c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setting-descriptor-fields"></a>Deskriptorfelder festlegen
Eine Anwendung kann zum Ändern der Felder einen Deskriptor Aufrufen **SQLSetDescField**. Einige Felder sind schreibgeschützt und können nicht festgelegt werden. (Siehe die [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) funktionsbeschreibung.)  
  
 Deskriptorfelder Datensatz mit der Nummer eines Datensatzes festgelegt sind (*RecNumber*) 1 oder höher, While deskriptorheaderfelder diverse Datensatz 0 festgelegt. Die Nummer eines Datensatzes 0 wird auch verwendet, Lesezeichen Felder, gemäß der Konvention festlegen, dass Lesezeichen in Spalte 0 enthalten sind. Dadurch verbleibt möglicherweise den Eindruck, dass Lesezeichen Felder sind in der sicherheitsbeschreibungs-Header enthalten, aber dies nicht der Fall ist. Bookmark-Felder unterscheiden sich von Headerfelder.  
  
 Wenn Sie Felder einzeln festlegen, sollte die Anwendung die Sequenz, die in definierten folgen [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Einige Felder festlegen, führt der Treiber auf andere Felder festlegen. Dadurch wird sichergestellt, dass der Deskriptor wird immer verwendet wird, sobald die Anwendung einen-Datentyp angegeben wurde. Wenn die Anwendung das SQL_DESC_TYPE-Feld festlegt, überprüft der Treiber an, dass die anderen Felder, die den Typ angeben gültig und konsistent sind.  
  
 Wenn ein Funktionsaufruf, der einem Beschreibungsfeld festlegen würde ein Fehler auftritt, sind nach dem fehlerhaften Funktionsaufruf den Inhalt des Felds Deskriptor nicht definiert.
