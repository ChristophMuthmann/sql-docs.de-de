---
title: Bewertungsbericht (SybaseToSQL) | Microsoft Docs
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
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69d452d3403f46a423fd3a55195f40efb2aae74f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="assessment-report-sybasetosql"></a>Bewertungsbericht (SybaseToSQL)
Assessment Berichtfenster zeigt die Ergebnisse der Konvertierung von Datenbankobjekten zu [!INCLUDE[tsql](../../includes/tsql_md.md)] Syntax, und kann ebenfalls dazu beitragen, die Sie schätzen, die Komplexität und Kosten der Migrationsprojekte.  
  
Zugriff auf den Assessment-Bericht ausgewählten Objekten, die für die Konvertierung in Quelle Metadaten-Explorer Maustaste **Datenbanken**, und wählen Sie dann **Bericht erstellen**.  
  
## <a name="options"></a>enthalten  
**Konvertierungsstatistiken**  
Zeigt die Konvertierungsstatistiken vom Typ der Anweisung an. In diesem Bereich ist nur sichtbar, wenn ein Gruppenobjekt, z. B. ein Schema oder ein Objekt ohne Code im linken Bereich ausgewählt ist.  
  
**Objekte nach Kategorie**  
Zeigt die Konvertierungsstatistiken nach Objekttyp. In diesem Bereich ist nur sichtbar, wenn ein Gruppenobjekt, z. B. ein Schema oder ein Objekt ohne Code im linken Bereich ausgewählt ist.  
  
**Statistik**  
Zeigt die Konvertierungsstatistiken für das ausgewählte Objekt an. In diesem Bereich ist sichtbar, nur, wenn ein einzelnes Objekt mit dem Code im linken Bereich ausgewählt ist. Möglicherweise müssen Sie erweitern **Statistiken** um diesen Bereich anzuzeigen.  
  
**Source-navigation**  
Zeigt den ASE-Code für das ausgewählte Objekt und hervorgehoben, Code, der nicht in konvertiert wurde [!INCLUDE[tsql](../../includes/tsql_md.md)]. In diesem Bereich ist sichtbar, nur, wenn ein einzelnes Objekt mit dem Code im linken Bereich ausgewählt ist.  
  
Klicken Sie auf die Zeilennummern, um festzulegen, oder deaktivieren Sie Lesezeichen. Verwenden Sie die Schaltflächen zum Navigieren durch den Code am Anfang des Bereichs.  
  
**Ziel-navigation**  
Zeigt die Konvertierung des resultierenden [!INCLUDE[tsql](../../includes/tsql_md.md)] Code für das ausgewählte Objekt und Fehlermeldungen für Code, der nicht konvertiert wurden. In diesem Bereich ist sichtbar, nur, wenn ein einzelnes Objekt mit dem Code im linken Bereich ausgewählt ist.  
  
Klicken Sie auf die Zeilennummern, um festzulegen, oder deaktivieren Sie Lesezeichen. Verwenden Sie die Schaltflächen zum Navigieren durch den Code am Anfang des Bereichs.  
  
**Meldungsbereich**  
Zeigt die Fehler, Warnungen und informationsmeldungen, die beim Erstellen des Bewertungsberichts generiert werden. Nachrichten werden nach Anzahl gruppiert. Um den Code anzuzeigen, die den Fehler verursacht hat, klicken Sie auf **Fehler**, **Warnung**, oder **Info**, erweitern Sie die Kategorie der Nachrichten, und klicken Sie dann auf eine Nachricht.  
  
