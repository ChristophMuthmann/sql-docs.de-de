---
title: Projekteinstellungen (Laden von Systemobjekte) (OracleToSQL) | Microsoft Docs
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
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 598f7726c2bb01b2b57cc98817716821b9112ca1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="project-settingsloading-system-objects-oracletosql"></a>Projekteinstellungen (Laden von Systemobjekte) (OracleToSQL)
Die Seite Laden von Systemobjekten der **Projekteinstellungen** Dialogfeld können Sie die Oracle-Systemobjekte SSMA konvertiert sowie lädt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
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
  
Die Oracle-Objekte auf zusätzliche Systemobjekte zu verweisen, müssen Sie diese Objekte auswählen. Wenn Sie nicht die Systemobjekte anzeigen auswählen, die von Oracle-Datenbankobjekte verwiesen wird, meldet SSMA Konvertierungsfehler. Wenn Sie durch fehlende Systemobjekte verursacht Fehler bei der Konvertierung erhalten, wählen Sie die fehlenden Objekte in diesem Dialogfeld. Wiederholen Sie dann die Konvertierung nach Bedarf.  
  
