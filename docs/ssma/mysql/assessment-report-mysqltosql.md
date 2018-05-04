---
title: Bewertungsbericht (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5525d989-024c-402d-9e84-faa4721cc5b9
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1c591815fc1d32405c0cc63f735fee24d03ce17f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="assessment-report-mysqltosql"></a>Bewertungsbericht (MySQLToSQL)
Assessment Berichtfenster zeigt die Ergebnisse der Konvertierung von Datenbankobjekten zu [!INCLUDE[tsql](../../includes/tsql_md.md)] Syntax, und kann ebenfalls dazu beitragen, die Sie schätzen, die Komplexität und Kosten der Migrationsprojekte.  
  
Zugriff auf den Assessment-Bericht ausgewählten Objekten, die für die Konvertierung in Quelle Metadaten-Explorer Maustaste **Schemas**, und wählen Sie dann **Bericht erstellen**.  
  
## <a name="options"></a>enthalten  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Konvertierungsstatistiken**|Zeigt die Konvertierungsstatistiken vom Typ der Anweisung an. In diesem Bereich ist sichtbar, wenn ein Gruppenobjekt, z. B. ein Schema oder ein Objekt ohne Code im linken Bereich ausgewählt ist.|  
|**Objekte nach Kategorien**|Zeigt die Anzahl der Objekte nach Kategorie. In diesem Bereich ist nur sichtbar, wenn ein Gruppenobjekt, z. B. ein Schema oder ein Objekt ohne Code im linken Bereich ausgewählt ist.|  
|**Statistik**|Zeigt die Konvertierungsstatistiken für das ausgewählte Objekt an. In diesem Bereich ist sichtbar, nur, wenn ein einzelnes Objekt mit dem Code im linken Bereich ausgewählt ist. Möglicherweise müssen Sie erweitern **Statistiken**, also direkt oberhalb der **Quelle** Bereich, um diesen Bereich anzuzeigen.|  
|**Quelle**|Zeigt den MySQL-Code für das ausgewählte Objekt und hervorgehoben, Code, der nicht in konvertiert wurde [!INCLUDE[tsql](../../includes/tsql_md.md)]. In diesem Bereich ist sichtbar, nur, wenn ein einzelnes Objekt mit dem Code im linken Bereich ausgewählt ist.<br /><br />Klicken Sie auf die Zeilennummern, um festzulegen, oder deaktivieren Sie Lesezeichen. Verwenden Sie die Schaltflächen zum Navigieren durch den Code am Anfang des Bereichs.|  
|**Target**|Zeigt die Konvertierung des resultierenden [!INCLUDE[tsql](../../includes/tsql_md.md)] Code für das ausgewählte Objekt und Fehlermeldungen für Code, der nicht konvertiert wurden. In diesem Bereich ist sichtbar, nur, wenn ein einzelnes Objekt mit dem Code im linken Bereich ausgewählt ist.<br /><br />Klicken Sie auf die Zeilennummern, um festzulegen, oder deaktivieren Sie Lesezeichen. Verwenden Sie die Schaltflächen zum Navigieren durch den Code am Anfang des Bereichs.|  
|**Meldungsbereich**|Zeigt die Fehler, Warnungen und informationsmeldungen, die beim Erstellen des Bewertungsberichts generiert wurden. Nachrichten werden nach Anzahl gruppiert. Um den Code anzuzeigen, die den Fehler verursacht hat, klicken Sie auf **Fehler**, **Warnungen**, oder **Info**, erweitern Sie die Kategorie der Nachrichten, und klicken Sie dann auf eine Nachricht.|  
  
