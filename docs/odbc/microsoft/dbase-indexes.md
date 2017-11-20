---
title: dBASE-Indizes | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase indexes [ODBC]
- DBase driver [ODBC], indexes
ms.assetid: fdfa56f5-e324-4ec2-9267-fdf95ab99373
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f2725f312691d3cb644f9a096b5f469f1356c55
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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

