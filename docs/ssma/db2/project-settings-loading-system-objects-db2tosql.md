---
title: Projekteinstellungen (Laden von Systemobjekte) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6fa389cfe6dea25a8974a47a4c77024720da312
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>Projekteinstellungen (Laden von Systemobjekte) (DB2ToSQL)
Die Seite Laden von Systemobjekten der **Projekteinstellungen** Dialogfeld können Sie die DB2-Systemobjekte SSMA konvertiert sowie lädt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Das Laden von Systemobjekten Bereich finden Sie in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder:  
  
-   Zum Angeben von Einstellungen für alle SSMA-Projekte, auf die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, wählen Sie die Migration-Projekttyp, die für die Einstellungen sind erforderlich, angezeigt oder geändert werden **Migration Zielversion** Dropdown-Liste auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Systemobjekte laden**.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, klicken Sie auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Systemobjekte laden**.  
  
## <a name="default-settings"></a>Standardeinstellungen  
Konvertieren von Systemobjekten Ressourcen beansprucht und zeitaufwändig. Um die Leistung zu verbessern, wählt der SSMA nur die am häufigsten verwendeten Systemobjekte, wie in der folgenden Liste gezeigt:  
  
-   SYS.DBMS_OUTPUT  
  
-   SYS.DBMS_PIPE  
  
-   SYS.DBMS_UTILITY  
  
-   SYS.STANDARD  
  
-   SYS.UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS.DBMS_SESSION  
  
Die DB2-Datenbankobjekte auf zusätzliche Systemobjekte zu verweisen, müssen Sie diese Objekte auswählen. Wenn Sie nicht die Systemobjekte anzeigen auswählen, die von der DB2-Datenbankobjekte verwiesen wird, meldet SSMA Konvertierungsfehler. Wenn Sie durch fehlende Systemobjekte verursacht Fehler bei der Konvertierung erhalten, wählen Sie die fehlenden Objekte in diesem Dialogfeld. Wiederholen Sie dann die Konvertierung nach Bedarf.  
  
