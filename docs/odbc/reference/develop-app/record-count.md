---
title: Anzahl der Datensätze | Microsoft Docs
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
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af24e83bc4f09f086ab1606dbb6d4dccbd9444e6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="record-count"></a>Anzahl der Datensätze
Das Headerfeld SQL_DESC_COUNT einen Deskriptor ist der einsbasierte Index des höchsten nummerierten Datensatzes, der Daten enthält. Dieses Feld ist nicht die Anzahl aller Spalten oder Parameter, die gebunden sind. Wenn ein Deskriptor, der belegt wurde, ist der Anfangswert von SQL_DESC_COUNT 0.  
  
 Der Treiber nimmt eine beliebige Aktion zum Zuordnen und verwalten den Speicher, der zum Speichern von Deskriptorinformationen dafür erforderlich. Die Anwendung weder nicht explizit angeben der Größe ein Deskriptor noch neue Datensätze reservieren. Wenn die Anwendung Informationen für den anwendungsparameterdeskriptor-Datensatz bereitstellt, deren Anzahl größer als der Wert des SQL_DESC_COUNT ist, wird der Treiber automatisch SQL_DESC_COUNT erhöht. Wenn die Anwendung die höchste Nummer Deskriptordatensatz hebt die Bindung, verringert der Treiber automatisch SQL_DESC_COUNT, um die Anzahl von den höchsten verbleibenden gebundenen Datensatz enthalten.
