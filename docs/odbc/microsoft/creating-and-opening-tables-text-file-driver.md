---
title: "Erstellen und Öffnen von Tabellen (Text-Datei-Treiber) | Microsoft Docs"
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
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 41190a0a3eabda2f73c8f6046a64b7b7db929fa1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="creating-and-opening-tables-text-file-driver"></a>Erstellen und Öffnen von Tabellen (Text-Datei-Treiber)
Wenn der Text-Treiber verwendet wird, wird eine neue Tabelle erstellt, mit dem Format, das in "Odbcinst.ini" angegeben. Wenn nicht angegeben, werden die Tabellen in CSVDELIMITED Format erstellt. Standardmäßig Ganzzahlspalten standardmäßig 11 Zeichen und "float" Standardspalten bis 22 Zeichen. Datumsspalten verwenden Sie das Format JJJJ-MM-TT. CHAR und LONGCHAR Spalten sind die Breite, die in der CREATE-Anweisung angegeben.
