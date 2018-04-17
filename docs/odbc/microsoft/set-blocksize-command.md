---
title: SET BLOCKSIZE-Befehl | Microsoft Docs
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
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee5b55501d055d3bea09903a5486e88de3cdc993
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE-Befehl
Gibt an, wie der Speicherplatz für die Speicherung von Memo-Felder verwendet wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argumente  
 *Anzahl_byte*  
 Gibt die Blockgröße, die in der Speicherplatz für Memofelder verwendet wird. Wenn *Anzahl_byte* gleich 0 ist, Speicherplatz einzelbytes (Blöcke von 1 Byte) verwendet wird. Wenn *Anzahl_byte* ist eine ganze Zahl zwischen 1 und 32, Speicherplatz wird in Blöcke zugeordnet *Anzahl_byte* Bytes multipliziert mit 512. Wenn *Anzahl_byte* ist größer als 32, Speicherplatz wird verwendet, in Blöcken von *Anzahl_byte* Bytes. Wenn Sie einen Block Größenwert größer als 32 angeben, können Sie erhebliche sehr viel Speicherplatz sparen.  
  
## <a name="remarks"></a>Hinweise  
 Der Standardwert für BLOCKSIZE festgelegt ist 64. Um die Blockgröße auf einen anderen Wert zurückgesetzt, nachdem die Datei erstellt wurde, legen Sie es auf einen neuen Wert aus, und klicken Sie dann verwenden Sie kopieren, um eine neue Tabelle zu erstellen. Die neue Tabelle besitzt die angegebene Blockgröße.
