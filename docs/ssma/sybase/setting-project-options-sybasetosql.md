---
title: Festlegen von Optionen für Projekt (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Project Options Setting
ms.assetid: 97b70fc8-1f68-4f15-8e22-db5b784ea4ec
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 626fb48e030f1bf1d78bc0ff0391cc5748fe78f9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="setting-project-options-sybasetosql"></a>Einstellungsoptionen für Projekt (SybaseToSQL)
Für jedes SSMA-Projekt können Sie Optionen für Projekt festlegen. Diese Optionen geben Objekt Konvertierung, Objekt laden, SQL Azure, Benutzeroberfläche und Einstellungen für die Migration von Daten. Bevor Sie Objekte konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure oder Migrieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, stellen Sie sicher, dass die Konfigurationsoptionen für das Projekt geeignet sind.  
  
SSMA können Sie die Standardoptionen für alle Projekte zu konfigurieren. Diese Optionen werden auf jedem neuen Projekt angewendet, die Sie erstellen. Sie können dann die Optionen für jedes Projekt anpassen.  
  
## <a name="configuration-options-and-modes"></a>Modi "und"-Konfigurationsoptionen  
SSMA verfügt über fünf Mengen von projekteinstellungen:  
  
1.  Projektinformationen  
  
2.  Allgemein (Konvertierung, Migration und das Sammeln von Daten)  
  
3.  Synchronization  
  
4.  GUI  
  
5.  Typzuordnung  
  
Es sind auch vier Modi für diese Einstellungen konfigurieren:  
  
1.  Standardwert  
  
2.  Optimistisch  
  
3.  Vollständig  
  
4.  Benutzerdefiniert  
  
Der Standardmodus ist für die meisten Benutzer empfohlen. Der optimistische hält mehrere der Syntax für die aktuelle Sybase Adaptive Server Enterprise (ASE) und einfacher zu lesen. Jedoch behalten die aktuelle Syntax genau möglicherweise nicht. Wenn die ASE-Syntax muss, in entsprechende konvertiert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax, die Vollmodus führt eine Konvertierung abgeschlossene, aber möglicherweise ist des resultierenden Codes schwieriger zu lesen. In den benutzerdefinierten Modus legen Sie die Optionen an.  
  
Die Einstellungen werden in der Referenz zur Benutzeroberfläche Teil dieser Dokumentation beschrieben. Weitere Informationen zu den Einstellungen und wie die Einstellungen in jedem Modus angewendet werden finden Sie unter den folgenden Themen:  
  
-   [Projekteinstellungen &#40;Konvertierung&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
-   [Projekteinstellungen &#40;Migration&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)  
  
-   [Projekteinstellungen &#40;Synchronisierung&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)  
  
-   [Projekteinstellungen &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)  
  
-   [Projekteinstellungen &#40;Typzuordnung&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)  
  
-   [Projekteinstellungen &#40;Azure SQL-Datenbank &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)  
  
## <a name="setting-project-options"></a>Einstellung Projektoptionen  
In SSMA können Sie die Standardeinstellungen für alle Projekte konfigurieren. Diese Einstellungen sind der SSMA-Konfigurationsdatei gespeichert und angewendet wird, zu einem neuen Projekt, das Sie erstellen.  
  
**Zum Festlegen von standardmäßigen Projektoptionen**  
  
1.  Auf der **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**.  
  
2.  In der **Projekt Standardeinstellungen** (Dialogfeld), verwenden Sie eine der folgenden Verfahren:  
  
    -   Wählen Sie die Migration-Projekttyp, die für die Einstellungen sind erforderlich, angezeigt oder geändert werden **Migration Zielversion** löschen klicken Sie unten auf allgemeine unten im linken Bereich, und wählen Sie die Konvertierung oder Migration oder SQL Azure.  
  
    -   Wählen Sie einen vordefinierten Modus in den **Modus** wählen Sie im Dropdown- **Standard**, **Optimistic**, oder **vollständige**.  
  
    -   Um benutzerdefinierte Einstellungen festzulegen, wählen Sie oder geben Sie den neuen Einstellungen oder Werten.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
Sie können auch die Einstellungen für das aktuelle Projekt anpassen. Diese Einstellungen werden in der aktuellen Projektdatei gespeichert.  
  
**Einstellungen für das aktuelle Projekt anpassen**  
  
1.  Auf der **Tools** klicken Sie im Menü **Projekteinstellungen**.  
  
2.  In der **Projekteinstellungen** (Dialogfeld), verwenden Sie eine der folgenden Verfahren:  
  
    -   Wählen Sie einen vordefinierten Modus in den **Modus** wählen Sie im Dropdown- **Standard**, **Optimistic**, oder **vollständige**.  
  
    -   Angeben einen benutzerdefinierten Modus, in der **Modus** wählen Sie im Dropdown- **benutzerdefinierte**, wählen Sie eine Option im linken Bereich, klicken Sie auf der Einstellung oder Wert im rechten Bereich, und klicken Sie dann wählen, oder geben Sie die neue Einstellung oder einen Wert.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
## <a name="next-steps"></a>Nächste Schritte  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   An benutzerdefinierte die Zuordnung der Quell- und Datentypen, finden Sie unter [Zuordnung Sybase ASE und SQL Server-Datentypen &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Konvertieren Sie Sie andernfalls die Sybase-Datenbank-Objektdefinitionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objektdefinitionen. Weitere Informationen finden Sie unter [Konvertierung von Sybase ASE Datenbankobjekte &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
