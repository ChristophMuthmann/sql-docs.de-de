---
title: Keysetgesteuerte Cursor | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7cbd7ca159b09ee1482139ef76bfff48115a62bd
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="keyset-driven-cursors"></a>Keysetgesteuerte Cursor
Ein keysetgesteuerter Cursor liegt zwischen statischen und einen dynamischen Cursor in seiner Fähigkeit, Änderungen zu erkennen. Wie ein statischer Cursor kann es nicht immer zum Ändern der Mitgliedschaft und Reihenfolge des Resultsets erkennen. Z. B. einen dynamischen Cursor erkennt er Änderungen auf die Werte der Zeilen im Resultset (unterliegen die Isolationsstufe der Transaktion, wie durch das Verbindungsattribut SQL_ATTR_TXN_ISOLATION festgelegt).  
  
 Wenn ein keysetgesteuerter Cursor geöffnet wird, werden die Schlüssel für das gesamte Resultset gespeichert; Dies behebt die offensichtlichen Mitgliedschaft und Reihenfolge des Resultsets. Wenn der Cursor über das Resultset einen Bildlauf durchführt, verwendet Sie Schlüssel in dieser *Keyset* zum Abrufen der aktuellen Datenwerte für jede Zeile. Nehmen wir beispielsweise an ein keysetgesteuerter Cursor abruft, eine Zeile und einer anderen Anwendung wird diese Zeile aktualisiert. Wenn der Cursor die Zeile refetches, sind die Werte, die er angezeigt wird neue, da sie die Zeile mit dem Schlüssel erneut abgerufen. Aus diesem Grund erkennen die keysetgesteuerte Cursor immer von sich selbst und anderen Benutzern vorgenommene Änderungen.  
  
 Wenn der Cursor versucht, eine Zeile abzurufen, die gelöscht wurde, wird diese Zeile als "Loch" im Resultset angezeigt: der Schlüssel für die Zeile im Keyset vorhanden ist, aber die Zeile im Resultset nicht mehr vorhanden ist. Wenn die Schlüsselwerte in einer Zeile aktualisiert werden, die Zeile gilt gelöscht, und klicken Sie dann eingefügt werden, damit dieser Zeilen auch als Lücken im Resultset angezeigt. Während ein keysetgesteuerten Cursors immer von anderen Benutzern gelöschte Zeilen erkennen kann, können sie optional entfernen, auf die Schlüssel für Zeilen löscht selbst über das Keyset. Keysetgesteuerte Cursor, die hierfür nicht ihre eigenen Löschvorgänge erkannt werden. Gibt an, ob ein bestimmter keysetgesteuerte Cursor einen eigenen Löschvorgänge erkennt, wird durch die SQL_STATIC_SENSITIVITY-Option in gemeldet **SQLGetInfo**.  
  
 Zeilen, die von anderen Benutzern eingefügt sind nie auf einen keysetgesteuerten Cursor sichtbar, da kein Schlüssel für diese Zeilen im Keyset befinden. Ein keysetgesteuerter Cursor kann jedoch optional hinzufügen, die Schlüssel für Zeilen fügt sich selbst auf das Keyset. Keysetgesteuerte Cursor, die hierfür können ihre eigenen einfügungen ermittelt werden. Gibt an, ob ein bestimmter keysetgesteuerte Cursor einen eigenen Einfügevorgänge erkennt, wird durch die SQL_STATIC_SENSITIVITY-Option in gemeldet **SQLGetInfo**.  
  
 Die zeilenstatusarray SQL_ATTR_ROW_STATUS_PTR-Anweisungsattribut gemäß kann SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO oder SQL_ROW_ERROR für jede Zeile enthalten. Es gibt SQL_ROW_UPDATED, SQL_ROW_DELETED oder SQL_ROW_ADDED für Zeilen, die als aktualisierte, erkannt wird, gelöscht oder eingefügt.  
  
 Keysetgesteuerte Cursor werden häufig implementiert, durch das Erstellen einer temporären Tabelle, die die Schlüssel für jede Zeile im Resultset enthält. Da sich der Cursor auch bestimmen muss, ob Zeilen aktualisiert wurden, enthält diese Tabelle häufig auch eine Spalte mit zeilenversionsverwaltungs-Informationen.  
  
 Um über die ursprünglichen Resultset zu blättern, öffnet der keysetgesteuerte Cursor einen statischen Cursor über die temporäre Tabelle. Zum Abrufen einer Zeile im ursprünglichen Resultset des Cursors ruft zunächst den entsprechenden Schlüssel aus der temporären Tabelle und ruft dann die aktuellen Werte für die Zeile ab. Blockcursor verwendet werden, muss der Cursor mehrere Schlüssel und Zeilen abgerufen werden.

