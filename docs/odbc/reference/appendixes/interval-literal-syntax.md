---
title: Intervall Literal Syntax | Microsoft Docs
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
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 472a8a68032c1d5b119bbf1d366b353927eca0dd
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="interval-literal-syntax"></a>Intervall Literal-Syntax
Die folgende Syntax wird für die Intervall-Literale in ODBC verwendet.  
  
 *Intervall-Literals:: = Intervall* [+*&#124;* -] *Intervall Intervall-zeichenfolgenqualifizierer*  
  
 *Intervall Zeichenfolge* :: = *Angebot* { *Jahr-Monat-Literal* &#124; *Tag Zeitliteral* } *Angebot*  
  
 *Jahr-Monat-Literal* :: = *Jahre Wert* &#124; [*Jahre Wert* -] *Wert für die Monate*  
  
 *Tag-Uhrzeit-Literal* :: = *Tag Zeitintervall* &#124; *Zeitintervall*  
  
 *Tag Zeitintervall* :: = *Wert Tage* [*Stundenwert* [:*Minutenwert*[:*Wert für die Sekunden*]]]  
  
 *Zeitintervall* :: = *Stundenwert* [:*Minutenwert* [:*Wert für die Sekunden* ]]  
  
 &#124; *Minutenwert* [:*Wert für die Sekunden* ]  
  
 &#124; *Wert für die Sekunden*  
  
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
  
 *End-Feld* :: = *nicht-Sekunde-Datetime-Feld* &#124; ZWEITE [(*Intervall--Sekunden-Genauigkeit von Bruchteilen*)]  
  
 *Single-Datetime-Feld* :: = *nicht-Sekunde-Datetime-Feld* [(*Intervall führende Feld Genauigkeit*)] &#124; ZWEITE [(*Intervall führende Feld Genauigkeit* [, (*Intervall--Sekunden-Genauigkeit von Bruchteilen*)]  
  
 *DateTime-Feld* :: = *nicht-Sekunde-Datetime-Feld* &#124; SEKUNDE  
  
 *nicht-Sekunde-Datetime-Feld* :: = Jahr &#124; Monat &#124; Tag &#124; Stunde &#124; MINUTE  
  
 *Intervall--Sekunden-Genauigkeit von Bruchteilen* :: = *unsigned Integer*  
  
 *Intervall führende Feld Genauigkeit* :: = *unsigned Integer*  
  
 *Angebot* :: = "  
  
 *unsigned Integer* :: = *Ziffer...*

