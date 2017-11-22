---
title: Visual FoxPro-Felddatentypen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b4dbb88985b114e0e2f89c4a3f57d8dae4c9210
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro-Felddatentypen
Die folgende Tabelle enthält die Werte für die *FieldType* -Argument in ALTER TABLE und CREATE TABLE und gibt an, ob *nFieldWidth* und *nPrecision* Argumente sind Erforderlich.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|Zeichenfeld der Breite*n*|  
|D|-|-|Datum|  
|V|N|d|Gleitkommawert numerisches Feld der Breite  *n*  mit *d* Dezimalstellen an.|  
|G|-|-|Allgemein|  
|I|-|-|Integer|  
|L|-|-|Logische Operatoren|  
|M|-|-|Memo|  
|N|N|d|Numerisches Feld der Breite  *n*  mit *d* Dezimalstellen an.|  
|T|-|-|DateTime|  
|J|-|-|Währung|
