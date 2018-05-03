---
title: Importieren von Daten in Microsoft Excel aus einer Visual FoxPro-Datenbank | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa6da8abaca5b3b14c48bc4324a50301d5a36d87
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importieren von Daten in Microsoft Excel aus einer Visual FoxPro-Datenbank
Sie können Visual FoxPro-Daten in Microsoft Excel-Arbeitsblatt importieren, wenn Sie eine Datenquelle für sie definiert haben. Informationen zum Erstellen einer Visual FoxPro-Datenquelle finden Sie unter [Zugriff auf eine Visual FoxPro-Datenquelle aus Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Visual FoxPro-Daten in einem Microsoft Excel-Arbeitsblatt importieren  
  
1.  Öffnen Sie Microsoft Excel-Arbeitsblatt an.  
  
2.  Wählen Sie im Menü Data externe Daten abrufen. Microsoft Query wird geöffnet.  
  
3.  Klicken Sie im Dialogfeld Auswählen einer Datenquelle wählen Sie eine Visual FoxPro-Datenquelle, und klicken Sie dann auf verwenden.  
  
4.  Wenn die Datenbank zugegriffen wird, von der Datenquelle Tabellen enthält, wählen Sie eine Tabelle aus dem Dialogfeld Tabellen hinzufügen. Microsoft Query hinzugefügte Tabelle in der oberen Hälfte des Abfrage-Designers angezeigt.  
  
    > [!NOTE]  
    >  Die Liste der Besitzer ist nicht in diesem Dialogfeld verfügbar, da der Treiber Besitzer nicht unterstützt. Die Datenbankliste ist nicht verfügbar, da der Treiber nicht über mehrere Datenbanken in einer Datenquelle unterstützt.  
  
5.  Wählen Sie Felder für die Abfrage durch Ziehen sie aus der Tabelle auf der unteren Hälfte des Designers.  
  
6.  Schließen Sie Microsoft-Abfrage. Die Daten, die Sie ausgewählt haben, werden in Microsoft Excel-Arbeitsblatt importiert.
