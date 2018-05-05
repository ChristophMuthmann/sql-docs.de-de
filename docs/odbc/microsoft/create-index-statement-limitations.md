---
title: Erstellen des INDEX-Anweisung Einschränkungen | Microsoft Docs
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
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9501e07fcdb70984153a718eed22be4d5448ec9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-index-statement-limitations"></a>Erstellen von Einschränkungen für INDEX-Anweisung
CREATE INDEX-Anweisung wird für die Microsoft Excel- oder Textdateien-Treiber nicht unterstützt.  
  
 Ein Index kann auf maximal 10 Spalten definiert werden. Wenn mehr als 10 Spalten in einer CREATE INDEX-Anweisung enthalten sind, der Index wird nicht erkannt werden, und die Tabelle behandelt werden, als wären, wenn kein Index erstellt wurden.  
  
 DBASE-Treiber kann nicht für eine logische Spalte einen Index erstellen.  
  
 Wenn dBASE-Treiber verwendet wird, kann die Antwortzeit große Dateien verbessert werden, durch Erstellen eines Indexes MDX-(oder NDX) für die Spalte (Feld) in der WHERE-Klausel einer SELECT-Anweisung angegeben. Vorhandene MDX-Indizes automatisch ausgeglichen werden für =, >, \<, > =, = <, Operatoren, die in einer WHERE-Klausel und LIKE-Prädikaten sowie in Join-Prädikaten und BETWEEN.  
  
 Wenn der Treiber dBASE verwendet wird, der Index erstellt, indem eine CREATE UNIQUE INDEX-Anweisung ist eigentlich nicht eindeutig und doppelte Werte in der indizierten Spalte eingefügt werden können. Der Index kann nur ein Datensatz aus einem Satz mit zwei identische Schlüsselwerte hinzugefügt werden.  
  
 Wenn der Paradox-Treiber verwendet wird, muss ein eindeutiger Index nach einem zusammenhängenden Teilmenge der Spalten in einer Tabelle, einschließlich der ersten Spalte definiert werden. Eine Tabelle kann nicht vom Treiber Paradox aktualisiert werden, wenn ein eindeutiger Index für die Tabelle oder der Paradox-Treiber verwendet wird, ohne die Implementierung von Borland Database Engine nicht definiert ist.
