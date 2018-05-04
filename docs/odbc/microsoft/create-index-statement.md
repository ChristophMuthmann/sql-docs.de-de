---
title: CREATE Indexanweisung | Microsoft Docs
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
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afe47371db4ef8aee2e225cc9b11523c507c129f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
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
