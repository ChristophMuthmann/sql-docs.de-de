---
title: CREATE Indexanweisung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ca556e41216bd2f9418c2ed31369347b51efd4a9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="create-index-statement"></a>CREATE Indexanweisung
Die Syntax der CREATE INDEX-Anweisung lautet:  
  
 Erstellen [UNIQUE] INDEX *Indexname* ON *Tabellenname* (*Spaltenbezeichner* [ASC] [DESC] [, *Spaltenbezeichner* [ASC][DESC]...]) MIT \< *Liste der Index-Optionen*>  
  
 auf dem \< *Index Optionsliste*> sind möglich: primären Dateigruppe &#124; Nicht zulassen Sie, NULL &#124; IGNORIEREN VON NULL  
  
 Der Microsoft Access-Treiber verwendet die NULL nicht zulassen und ignorieren NULL-Index-Optionen. Die dBASE und Paradox-Treiber akzeptiert die Syntax, aber ignorieren Sie das Vorhandensein der beiden Optionen.  
  
 Wenn der Paradox-Treiber verwendet wird, erstellt die CREATE INDEX-Anweisung Paradox Schlüsseldateien primäre und sekundäre Dateien.  
  
 Diese Anweisung wird von Microsoft Excel- oder Textdateien-Treibern nicht unterstützt.
