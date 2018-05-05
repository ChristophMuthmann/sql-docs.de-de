---
title: CREATE Indexanweisung | Microsoft Docs
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
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 86d4cf1bb047cd475b86b9a58c37f3268c07c91d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-index-statement"></a>CREATE Indexanweisung
Die Syntax der CREATE INDEX-Anweisung lautet:  
  
 Erstellen [UNIQUE] INDEX *Indexname* ON *Tabellenname* (*Spaltenbezeichner* [ASC] [DESC] [, *Spaltenbezeichner* [ASC][DESC]...]) MIT \< *Liste der Index-Optionen*>  
  
 auf dem \< *Index Optionsliste*> kann sein: primäre &#124; NULL nicht zulassen &#124; ignorieren NULL  
  
 Der Microsoft Access-Treiber verwendet die NULL nicht zulassen und ignorieren NULL-Index-Optionen. Die dBASE und Paradox-Treiber akzeptiert die Syntax, aber ignorieren Sie das Vorhandensein der beiden Optionen.  
  
 Wenn der Paradox-Treiber verwendet wird, erstellt die CREATE INDEX-Anweisung Paradox Schlüsseldateien primäre und sekundäre Dateien.  
  
 Diese Anweisung wird von Microsoft Excel- oder Textdateien-Treibern nicht unterstützt.
