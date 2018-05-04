---
title: dBASE-Indizes | Microsoft Docs
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
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe8787e299d57fcac9d437be6d71023268e6c7d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dbase-indexes"></a>dBASE-Indizes
Der ODBC-Treiber dBASE öffnet automatisch und dBASE IV-Indexdateien aktualisiert. Verwenden Sie die **Indizes auswählen** Dialogfeld angezeigt, über die ODBC-Datenquellen-Administrator, dBASE-Dateien dBASE III NDX-Dateien zugeordnet werden soll.  
  
 Die folgenden Einschränkungen gelten für die Erstellung von dBASE Indizes:  
  
-   Alle Spaltennamen müssen gültig sein.  
  
-   Alle Spalten müssen in derselben aufsteigenden oder absteigenden Reihenfolge aufweisen.  
  
-   Die Länge der jede Spalte muss weniger als 100 Byte sein.  
  
-   Wenn mehr als eine Spalte vorhanden ist, muss alle Spalten in den Spalten, und die Summe der Spaltengrößen muss weniger als 100 Byte sein.  
  
-   Memo-Felder können nicht indiziert werden.  
  
-   Ein Index muss nicht angegeben werden, für den aktuellen Satz von Feldern (d. h. doppelten Indizes sind nicht zulässig).  
  
-   Der Indexname muss die Namenskonvention für dBASE Index übereinstimmen. dBASE III erfordert, dass jeder Index in einer separaten Datei, jeder mit der Erweiterung NDX. In dBASE IV werden Indizes als Tagnamen erstellt, die in einer einzigen MDX-Datei gespeichert werden. Die MDX-Datei hat den gleichen Basisnamen wie die Datenbankdatei (z. B. die Emp.mdx die Indexdatei für die Datenbank Emp.dbf ist).  
  
-   dBASE definiert einen eindeutigen Index als, in denen nur ein Datensatz aus einem Satz mit zwei identische Schlüsselwerte, die dem Index hinzugefügt wird.
