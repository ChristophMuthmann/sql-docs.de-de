---
title: Intervall Literal Syntax | Microsoft Docs
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
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f0d7155a5ba476906bc1d8453b7732d8d5b45c1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="interval-literal-syntax"></a>Intervall Literal-Syntax
Die folgende Syntax wird für die Intervall-Literale in ODBC verwendet.  
  
 *Intervall-Literals:: = Intervall* [+*&#124;*-] *Intervall Intervall-zeichenfolgenqualifizierer*  
  
 *Intervall Zeichenfolge* :: = *Angebot* { *Jahr-Monat-Literal* &#124; *Tag Zeitliteral* } *Angebot*  
  
 *Jahr-Monat-Literal* :: = *Jahre Wert* &#124; [*Jahre Wert* -] *Wert für die Monate*  
  
 *Tag-Uhrzeit-Literal* :: = *Tag Zeitintervall* &#124; *Zeitintervall*  
  
 *Tag Zeitintervall* :: = *Wert Tage* [*Stundenwert* [:*Minutenwert*[:*Wert für die Sekunden*]]]  
  
 *Zeitintervall* :: = *Stundenwert* [:*Minutenwert* [:*Wert für die Sekunden* ]]  
  
 &#124;*Minutenwert* [:*Wert für die Sekunden* ]  
  
 &#124;*Wert für die Sekunden*  
  
 *Jahre Wert* :: = *Datetime-Wert*  
  
 *Wert für die Monate* :: = *Datetime-Wert*  
  
 *Wert für die Tage* :: = *Datetime-Wert*  
  
 *Wert für die Stunden* :: = *Datetime-Wert*  
  
 *Wert Minuten* :: = *Datetime-Wert*  
  
 *Wert für die Sekunden* :: = *Sekunden Ganzzahlwert* [. [ *Sekundenbruchteils*]]  
  
 *Sekunden Ganzzahlwert* :: = *unsigned Integer*  
  
 *Sekundenbruchteils* :: = *unsigned Integer*  
  
 *DateTime-Wert* :: = *unsigned Integer*  
  
 *Intervall-Qualifizierer* :: = *Start-Feld* TO *End-Feld* &#124; *Single-Datetime-Feld*  
  
 *Start-Feld* :: = *nicht-Sekunde-Datetime-Feld* [(*Intervall führende Feld Genauigkeit* )]  
  
 *End-Feld* :: = *nicht-Sekunde-Datetime-Feld* &#124; zweite [(*Intervall--Sekunden-Genauigkeit von Bruchteilen*)]  
  
 *Single-Datetime-Feld* :: = *nicht-Sekunde-Datetime-Feld* [(*Intervall führende Feld Genauigkeit*)] &#124; zweite [(*Intervall führende Feld Genauigkeit*  [, (*Intervall--Sekunden-Genauigkeit von Bruchteilen*)]  
  
 *DateTime-Feld* :: = *nicht-Sekunde-Datetime-Feld* &#124; zweite  
  
 *nicht-Sekunde-Datetime-Feld* :: = Jahr &#124; Monat &#124; Tag &#124; Stunde &#124; MINUTE  
  
 *Intervall--Sekunden-Genauigkeit von Bruchteilen* :: = *unsigned Integer*  
  
 *Intervall führende Feld Genauigkeit* :: = *unsigned Integer*  
  
 *Angebot* :: = "  
  
 *unsigned Integer* :: = *Ziffer...*
