---
title: "Hinzufügen einer Datenquelle Visual FoxPro | Microsoft Docs"
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
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e60681b7a3f30a83c2a1227c466b663b1b4d8a7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="adding-a-visual-foxpro-data-source"></a>Fügen Sie eine Visual FoxPro-Datenquelle
Um Visual FoxPro-Daten aus Ihrer Anwendung zuzugreifen, müssen Sie eine Datenquelle verfügen. Sie können eine Datenquelle wie folgt erstellen:  
  
-   In einer Anwendung, z. B. Microsoft® Word, Microsoft Excel oder Microsoft Access verwendet, ODBC-Treiber.  
  
-   Außerhalb der Anwendung mithilfe der Microsoft Windows® 95, Microsoft Windows 98 oder Microsoft Windows/Windows 2000-Systemsteuerung.  
  
 Nachdem eine Datenquelle auf dem System vorhanden ist, können Sie die gleiche Datenquelle jedes Mal erneut, die Sie auf der Visual FoxPro-Daten zugreifen möchten. Wenn Sie mehrere verschiedene Datenbanken oder Tabellen, auf die Sie zugreifen möchten, können Sie eine anderen Datenquelle für jede Datenbank oder ein Verzeichnis erstellen.  
  
 Die folgende Prozedur erstellt eine Datenquelle mithilfe der Systemsteuerung. Weitere Informationen zur Vorgehensweise beim Erstellen einer Datenquelle aus einer Anwendung finden Sie unter [Zugriff auf Visual FoxPro-Daten aus Microsoft Office](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md).  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>So fügen Sie eine Visual FoxPro-Datenquelle hinzu  
  
1.  Öffnen Sie auf Computern, auf denen Windows 2000 ausgeführt werden die Windows-Systemsteuerung, und doppelklicken Sie auf Verwaltung.  
  
2.  Doppelklicken Sie auf Datenquellen (ODBC) um das Dialogfeld ODBC-Datenquellen-Administrator zu öffnen. Dieses Symbol ist verfügbar, nachdem Sie der Visual FoxPro-ODBC-Treiber oder alle ODBC-Treiber-Software installiert haben.  
  
    > [!NOTE]  
    >  Wenn Sie eine frühere Version von Windows ausgeführt werden, öffnen Sie die Windows-Systemsteuerung, und doppelklicken Sie auf 32-Bit-ODBC- oder ODBC zum Öffnen des Dialogfelds für die ODBC-Datenquellen-Administrator.  
  
3.  Klicken Sie auf Hinzufügen.  
  
4.  Klicken Sie im Dialogfeld "neue Datenquelle erstellen" Wählen Sie Microsoft Visual FoxPro-Treiber aus, und klicken Sie dann auf ' Fertig stellen '.  
  
5.  In der [ODBC Visual FoxPro einrichten (Dialogfeld)](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md), geben Sie den Datenquellennamen und die Beschreibung, wählen Sie den Datenbanktyp, wählen Sie die Datenbank oder das Verzeichnis, und klicken Sie dann auf OK.  
  
     Der neue Name der Datenquelle wird in der Liste der Datenquellen für Benutzer in der Registerkarte "Benutzer-DSN" im Dialogfeld ODBC-Datenquellen-Administrator angezeigt.  
  
6.  Klicken Sie auf OK, um die neue Datenquelle zu speichern und schließen das Dialogfeld ODBC-Datenquellen-Administrator.
