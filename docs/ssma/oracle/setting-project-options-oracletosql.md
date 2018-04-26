---
title: Festlegen von Optionen für Projekt (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Configuration Options and Modes
ms.assetid: a324d07d-cfdf-43bd-98a0-acf332c5a4db
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 6e3f796e4681f7eb8a5f3c8b1b00d8ab9f552b13
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="setting-project-options-oracletosql"></a>Einstellungsoptionen für Projekt (OracleToSQL)
Für jedes SSMA-Projekt können Sie Optionen für Projekt festlegen. Diese Optionen geben Objekt Konvertierung, Objekt laden, Benutzeroberflächen- und Migration benutzereinstellungen. Bevor Sie Objekte konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Migrieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], stellen Sie sicher, dass die Konfigurationsoptionen für das Projekt geeignet sind.  
  
SSMA können Sie die Standardoptionen für alle Projekte zu konfigurieren. Diese Optionen werden auf jedem neuen Projekt angewendet, die Sie erstellen. Sie können dann die Optionen für jedes Projekt anpassen.  
  
## <a name="configuration-options-and-modes"></a>Modi "und"-Konfigurationsoptionen  
SSMA verfügt über fünf Mengen von projekteinstellungen:  
  
-   Projektinformationen  
  
-   Allgemein (Konvertierung, Migration, Laden von Objekten)  
  
-   Synchronization  
  
-   GUI  
  
-   Typzuordnung  
  
Es sind auch vier Modi für diese Einstellungen konfigurieren:  
  
-   Standardwert  
  
-   Optimistisch  
  
-   Vollständig  
  
-   Benutzerdefiniert  
  
Der Standardmodus ist für die meisten Benutzer empfohlen. Der optimistische hält mehrere der Syntax für die aktuelle Oracle und einfacher zu lesen. Jedoch behalten die aktuelle Syntax genau möglicherweise nicht. Wenn die Oracle-Syntax muss, in entsprechende konvertiert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax, die der Vollmodus die beste Konvertierung durchgeführt, aber möglicherweise ist des resultierenden Codes schwieriger zu lesen. In den benutzerdefinierten Modus legen Sie die Optionen an.  
  
Weitere Informationen zu den Einstellungen und wie die Einstellungen in jedem Modus angewendet werden finden Sie unter den folgenden Themen:  
  
-   [Projekteinstellungen &#40;Konvertierung&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)  
  
-   [Projekteinstellungen &#40;Migration&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)  
  
-   [Projekteinstellungen&#40;Synchronisierung&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)  
  
-   [Projekteinstellungen &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)  
  
-   [Projekteinstellungen &#40;Typzuordnung&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)  
  
## <a name="setting-project-options"></a>Einstellung Projektoptionen  
In SSMA können Sie die Standardeinstellungen für alle Projekte konfigurieren. Diese Einstellungen sind der SSMA-Konfigurationsdatei gespeichert und angewendet wird, zu einem neuen Projekt, das Sie erstellen.  
  
**Zum Festlegen von standardmäßigen Projektoptionen**  
  
1.  Auf der **Tools** Menü klicken Sie auf **Projekt Standardeinstellungen**.  
  
2.  In der **Projekt Standardeinstellungen** (Dialogfeld), verwenden Sie eine der folgenden Verfahren:  
  
    -   Wählen Sie die Migration-Projekttyp, die für die Einstellungen sind erforderlich, angezeigt oder geändert werden **Migration Zielversion** Dropdown-Liste auf **allgemeine** am unteren Rand der Links, und wählen Sie dann Konvertierung oder Migration.  
  
    -   Wählen Sie einen vordefinierten Modus in den **Modus** wählen Sie im Dropdown- **Standard**, **Optimistic**, oder **vollständige**.  
  
    -   Um benutzerdefinierte Einstellungen festzulegen, wählen Sie aus, oder geben Sie den neuen Einstellungen oder Werten.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
Sie können auch die Einstellungen für das aktuelle Projekt anpassen. Diese Einstellungen werden in der aktuellen Projektdatei gespeichert.  
  
**Einstellungen für das aktuelle Projekt anpassen**  
  
1.  Auf der **Tools** Menü klicken Sie auf **Projekteinstellungen**.  
  
2.  In der **Projekteinstellungen** (Dialogfeld), verwenden Sie eine der folgenden Verfahren:  
  
    -   Wählen Sie einen vordefinierten Modus in den **Modus** wählen Sie im Dropdown- **Standard**, **Optimistic**, oder **vollständige**.  
  
    -   Angeben einen benutzerdefinierten Modus, in der **Modus** wählen Sie im **benutzerdefinierte**, und wählen Sie dann die richtigen projekteinstellungen.  
  
3.  Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
## <a name="next-steps"></a>Nächste Schritte  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnung Oracle und SQL Server-Datentypen &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   Konvertieren Sie Sie andernfalls die Oracle-Datenbank-Objektdefinitionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Objektdefinitionen. Weitere Informationen finden Sie unter [Oracle-Schemas konvertieren &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Zuordnen von Oracle und SQL Server-Datentypen &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)  
  
