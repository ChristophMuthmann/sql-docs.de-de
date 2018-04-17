---
title: Visual FoxPro-Daten in Microsoft Access importieren | Microsoft Docs
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
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0e6b2e882ae81c4c6faaebd550569cd3d5b73e38
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Visual FoxPro-Daten importieren in Microsoft Access
Sie können in einer Visual FoxPro-Datenbank in eine Microsoft Access-Datenbank mithilfe der Importoption gespeicherte Daten importieren.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Visual FoxPro-Daten in einer Microsoft Access-Datenbank importieren  
  
1.  Öffnen Sie eine Microsoft Access-Datenbank.  
  
2.  Wählen Sie, dass dann importieren Sie externe Daten abrufen, über das Menü Datei.  
  
3.  Wählen Sie im Dialogfeld "Importieren" ODBC-Datenbanken in der Liste aus.  
  
4.  Wählen Sie im Dialogfeld SQL-Datenquellen der Visual FoxPro-Datenquelle, die auf die Daten FoxPro, die Sie verwenden möchten verbindet, Fragen, und klicken Sie auf OK.  
  
5.  Wählen Sie im Dialogfeld Objekte importieren einer oder mehreren Tabellen, die Sie importieren möchten und klicken Sie auf OK. Die Namen der Visual FoxPro-Tabellen, die Sie importiert haben, werden auf der Registerkarte "Tabellen" der Microsoft Access-Datenbank angezeigt.  
  
 Microsoft Access können jetzt um die Daten in den importierten Visual FoxPro-Tabellen zu bearbeiten. Die zu importierenden Daten ist eine Momentaufnahme der Daten in der Visual FoxPro gespeichert. Änderungen auf die importierten Daten werden nicht in der Visual FoxPro-Datenquelle gesendet.  
  
 Wenn Sie Änderungen möchten, stellen Sie in Microsoft Access zum Ändern der Daten in der Visual FoxPro-Datenquelle finden Sie unter [Abfragen und Aktualisieren von Visual FoxPro-Daten aus Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).
