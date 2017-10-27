---
title: Generieren mit dem Ergebnis und Ergebnis frei Anweisungen | Microsoft Docs
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
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a99ea01cbd5a00ea4aa12e4b1461ca7f1ce9afa5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="result-generating-and-result-free-statements"></a>Generieren mit dem Ergebnis und Ergebnis frei-Anweisungen
SQL-Anweisungen können lose in den folgenden fünf Kategorien unterteilt werden:  
  
-   **Erstellen einer Gruppe von Anweisungen führen** Hierbei handelt es sich um SQL-Anweisungen, die ein Resultset generieren. Z. B. eine **wählen** Anweisung.  
  
-   **Row Count Generieren von Anweisungen** Hierbei handelt es sich um SQL-Anweisungen, die Anzahl der betroffenen Zeilen zu generieren. Angenommen, ein **UPDATE** oder **löschen** Anweisung.  
  
-   **Anweisungen von Data Definition Language (DDL)** Hierbei handelt es sich um SQL-Anweisungen, die die Struktur der Datenbank zu ändern. Beispielsweise **CREATE TABLE** oder **DROP INDEX**.  
  
-   **Ändern von Kontext Anweisungen** Hierbei handelt es sich um SQL-Anweisungen, die den Kontext einer Datenbank zu ändern. Z. B. die **verwenden** und **festgelegt** Anweisungen in SQL Server.  
  
-   **Administrative Anweisungen** diese SQL-Anweisungen zu Verwaltungszwecken in einer Datenbank verwendet werden. Beispielsweise **GRANT** und **widerrufen**.  
  
 SQL-Anweisungen in den ersten beiden Kategorien werden zusammenfassend als bezeichnet *Ergebnis Generieren von Anweisungen*. SQL-Anweisungen in den letzten drei Kategorien werden zusammenfassend als bezeichnet *Anweisungen Ergebnis freier*. ODBC definiert die Semantik der Batches, die nur aus dem Ergebnis generieren Anweisungen enthalten. Diese Semantik stark variieren und sind daher Daten datenquellenspezifischen. Beispielsweise unterstützt der SQL Server-Treiber ein Objekt löschen und verweisen auf oder das gleiche Objekt im selben Batch neu zu erstellen. Daher der Begriff *Batch* wie dies bei bezieht sich dieses Handbuch nur auf Batches Ergebnis Generieren von Anweisungen.

