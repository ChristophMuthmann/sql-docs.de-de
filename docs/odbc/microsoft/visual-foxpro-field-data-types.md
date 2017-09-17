---
title: Visual FoxPro-Felddatentypen | Microsoft Docs
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
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c1ae849d91962cb7d11ca8bac755665217fe1a2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro-Felddatentypen
Die folgende Tabelle enthält die Werte für die *FieldType* -Argument in ALTER TABLE und CREATE TABLE und gibt an, ob *nFieldWidth* und *nPrecision* Argumente sind Erforderlich.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|Zeichenfeld der Breite*n*|  
|D|-|-|Datum|  
|V|N|d|Gleitkommawert numerisches Feld der Breite * n * mit *d* Dezimalstellen an.|  
|G|-|-|Allgemein|  
|I|-|-|Integer|  
|L|-|-|Logische Operatoren|  
|M|-|-|Memo|  
|N|N|d|Numerisches Feld der Breite * n * mit *d* Dezimalstellen an.|  
|T|-|-|DateTime|  
|J|-|-|Währung|
