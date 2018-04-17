---
title: Visual FoxPro-Felddatentypen | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ccb1adbe822aeb29bd34749333d59b6b67f6f5fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro-Felddatentypen
Die folgende Tabelle enthält die Werte für die *FieldType* -Argument in ALTER TABLE und CREATE TABLE und gibt an, ob *nFieldWidth* und *nPrecision* Argumente sind Erforderlich.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|Zeichenfeld der Breite *n*|  
|D|-|-|Datum|  
|V|N|d|Gleitkommawert numerisches Feld der Breite *n* mit *d* Dezimalstellen an.|  
|G|-|-|Allgemein|  
|I|-|-|Integer|  
|L|-|-|Logische Operatoren|  
|M|-|-|Memo|  
|N|N|d|Numerisches Feld der Breite *n* mit *d* Dezimalstellen an.|  
|T|-|-|datetime|  
|J|-|-|Währung|
