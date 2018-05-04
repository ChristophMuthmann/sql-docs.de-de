---
title: Anzahl der Datensätze | Microsoft Docs
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
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4ab002f144070c94a659f0b1d67d09de9ceed50
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="record-count"></a>Anzahl der Datensätze
Das Headerfeld SQL_DESC_COUNT einen Deskriptor ist der einsbasierte Index des höchsten nummerierten Datensatzes, der Daten enthält. Dieses Feld ist nicht die Anzahl aller Spalten oder Parameter, die gebunden sind. Wenn ein Deskriptor, der belegt wurde, ist der Anfangswert von SQL_DESC_COUNT 0.  
  
 Der Treiber nimmt eine beliebige Aktion zum Zuordnen und verwalten den Speicher, der zum Speichern von Deskriptorinformationen dafür erforderlich. Die Anwendung weder nicht explizit angeben der Größe ein Deskriptor noch neue Datensätze reservieren. Wenn die Anwendung Informationen für den anwendungsparameterdeskriptor-Datensatz bereitstellt, deren Anzahl größer als der Wert des SQL_DESC_COUNT ist, wird der Treiber automatisch SQL_DESC_COUNT erhöht. Wenn die Anwendung die höchste Nummer Deskriptordatensatz hebt die Bindung, verringert der Treiber automatisch SQL_DESC_COUNT, um die Anzahl von den höchsten verbleibenden gebundenen Datensatz enthalten.
