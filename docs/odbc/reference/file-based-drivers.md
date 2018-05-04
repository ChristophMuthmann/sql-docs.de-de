---
title: Dateibasierten Treibern | Microsoft Docs
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
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c827972d0d4478431f085a6aa4d69f70f020be89
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="file-based-drivers"></a>Dateibasierten Treibern
Dateibasierten Treibern werden mit Datenquellen wie z. B. dBASE verwendet, die keine eigenständige Datenbank-Engine für den Treiber bieten verwenden. Diese Treiber Zugriff auf die physischen Daten direkt und müssen eine Datenbank-Engine, SQL-Anweisungen verarbeiten implementieren. Als eine standardmäßige Vorgehensweise implementieren die Datenbankmodule in einem dateibasierten Treibern die Teilmenge von ODBC-SQL, die durch die minimale SQL Konformitätsgrad definiert; eine Liste der SQL-Anweisungen in diesem Konformitätsgrad, finden Sie unter [Anhang C: SQL-Grammatik](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Bei Vergleichen von Datei und DBMS-basierten Treibern sind dateibasierten Treibern schwieriger zu schreiben, die aufgrund der datenbankmodulkomponente konfigurieren, da keine Figuren Netzwerk stehen weniger kompliziert und weniger leistungsfähiges Schreibberechtigung wenige Personen die Zeit für die Datenbank schreiben die Module ist so leistungsfähig wie die von Datenbank-Unternehmen.  
  
 Die folgende Abbildung zeigt zwei verschiedene Konfigurationen von dateibasierten Treibern, ein, in dem die Daten lokal befinden, und der andere in der er sich befindet, auf einem Netzwerkserver für die Datei.  
  
 ![Zwei Konfigurationen der Datei&#45;basierten Treiber](../../odbc/reference/media/pr06.gif "pr06")
