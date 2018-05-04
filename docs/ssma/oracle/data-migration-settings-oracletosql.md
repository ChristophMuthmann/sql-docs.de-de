---
title: Daten-Migrationseinstellungen (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2b90d81e07eecf97dc2e8c6f058ae7a278ecef64
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-migration-settings-oracletosql"></a>Daten-Migrationseinstellungen (OracleToSQL)
  
## <a name="data-migration-settings"></a>Einstellungen für die Migration von Daten  
**Einstellungen für die Migration von Daten** ermöglicht es dem Benutzer, benutzerdefinierte Abfragen für die Datenmigration zu schreiben.  
  
-   Diese Registerkarte ist verfügbar, wenn **erweiterte Optionen für die Migration von Daten** festgelegt ist, um **anzeigen** und wird ausgeblendet, wenn die Einstellung, um festgelegt ist **ausblenden** in den Projekteinstellungen. Weitere Informationen zu Projekteinstellungen für die Migration, finden Sie unter [Projekteinstellungen (Migration)](http://msdn.microsoft.com/en-us/fcd6b988-633b-4b2b-9f36-6368b5e86b60) .  
  
-   Analysieren von benutzerdefinierten SQL-Anweisungen in implementiert **migrationseinstellungen Daten** Table-Knoten auf der Registerkarte.  
  
-   Es folgen zwei Kontrollkästchen Dialogfeldern, die in der **Daten Migrationseinstellungen** begrenzt.:  
  
    1.  Schneiden Sie SQL Server-Tabelle  
  
    2.  Verwenden Sie benutzerdefinierte auswählen  
  
1.  **Schneiden Sie die SQL Server-Tabelle:**  
     Diese Option ermöglicht dem Benutzer, eine klare Sicht der migrierten Daten an die Zieldatenbank haben.  
  
    -   Standardmäßig wird dieses Textfeld überprüft.  
  
    -   Wenn dieses Textfeld deaktiviert ist, werden die Daten, die migriert werden an die vorhandenen Daten auf der Zieldatenbank hinzugefügt werden.  
  
2.  **Verwenden Sie benutzerdefinierte auswählen:**  
     Diese Option ermöglicht dem Benutzer zum Ändern der **wählen** Anweisung vorhanden (**wählen** Anweisung ermöglicht den Benutzern zur Auswahl der Daten in die Zieldatenbank angezeigt werden).  
  
    1.  Dieses Textfeld ist standardmäßig deaktiviert.  
  
    2.  Wenn dieses Textfeld aktiviert ist, ermöglicht Benutzern das Ändern der **wählen** Anweisung vorhanden.  
  
Es begrenzt sind zwei Schaltflächen vorhanden.:  
  
-   **Übernehmen:** klicken Sie auf **übernehmen** zum Anwenden der Einstellungen, die geändert wurden.  
  
-   **"Abbrechen":** klicken Sie auf **"Abbrechen"** vorhanden wiederhergestellt, bevor die Änderungen wurden vorgenommen wird.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Daten in SQLServer](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)  
  
