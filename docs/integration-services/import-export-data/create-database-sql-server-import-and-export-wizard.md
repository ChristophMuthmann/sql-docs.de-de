---
title: Datenbank erstellen (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9887db04ab04d6d78af9cecee96a1be12c58a42d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>Datenbank erstellen (SQL Server-Import/Export-Assistent)
Wenn Sie auf der Seite **Ziel auswählen** die Option **Neu** auswählen, um eine neue SQL Server Zieldatenbank zu erstellen, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent das Dialogfeld **Datenbank erstellen** an. Auf dieser Seite geben Sie einen Namen für die neue Datenbank ein. Optional können Sie auch die Einstellungen für die anfängliche Größe und die automatische Vergrößerung der neuen Datenbank und der zugehörigen Protokolldatei ändern. 

Das Dialogfeld **Datenbank erstellen** des Assistenten bietet nur die grundlegenden Optionen, die zum Erstellen einer neuen SQL Server-Datenbank verfügbar sind. Um alle Optionen für eine neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank anzuzeigen und zu konfigurieren, verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zum Erstellen der Datenbank, oder um sie zu konfigurieren, nachdem der Assistent sie erstellt hat. 

> [!NOTE]
> Wenn Sie Informationen zur [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung CREATE DATABASE und nicht zum Dialogfeld **Datenbank erstellen** des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistenten suchen, lesen Sie den Artikel [CREATE DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  

## <a name="screen-shot-of-the-create-database-page"></a>Screenshot der Seite „Datenbank erstellen“  
Der folgende Screenshot zeigt das Dialogfeld **Datenbank erstellen** des Assistenten an.  

![Seite „Datenbank erstellen“ des Import/Export-Assistenten](../../integration-services/import-export-data/media/create-database.png "Seite „Datenbank erstellen“ des Import/Export-Assistenten")  

## <a name="provide-a-name-for-the-new-database"></a>Angeben eines Namens für die neue Datenbank  
**Name**  
 Geben Sie einen Namen für die SQL Server-Zieldatenbank an.
 
### <a name="naming-requirements"></a>Benennungsanforderungen
Beachten Sie beim Benennen dieser Datenbank die entsprechenden Konventionen von SQL Server.  
  
-   Der Datenbankname muss innerhalb einer Instanz von SQL Server eindeutig sein.  
  
-   Der Datenbankname darf maximal 123 Zeichen lang sein. (SQL Server fügt 5 Zeichen lange Suffixe an die Datendatei und die Protokolldatei an, sodass die Maximallänge des gesamten Datenbanknamens 128 Zeichen beträgt.)  
  
-   Der Datenbankname muss den Regeln für Bezeichner in SQL Server entsprechen. Hier sind die wichtigsten Anforderungen.  
  
    -   Das erste Zeichen muss ein Buchstabe, ein Unterstrich (_), das at-Zeichen (@) oder das Nummernzeichen (#) sein.  
  
    -   Nachfolgende Zeichen können Buchstaben, Ziffern, das at-Zeichen, das Dollarzeichen ($), das Nummernzeichen oder ein Unterstrich sein.  
  
    -   Leerzeichen oder Sonderzeichen dürfen nicht verwendet werden.  
  
Ausführliche Informationen zu diesen Anforderungen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  

## <a name="optionally-specify-data-file-and-log-file-options"></a>Optionales Angeben von Datendatei- und Protokolldateioptionen

> [!TIP]
> Sie müssen im Feld **Name** einen Namen für die neue Datenbank angeben, die Einstellungen für Dateigröße und Dateivergrößerung können Sie auf den Standardwerten belassen.

### <a name="data-file-options"></a>Optionen für Datendateien  
 **Anfangsgröße**  
 Geben Sie die Anzahl der Megabytes für die Anfangsgröße der Datendatei an.  
  
 **Keine Vergrößerung zulässig**  
 Geben Sie an, ob die Datendatei die Größe der angegebenen Anfangsgröße übersteigen kann.  
  
 **Vergrößerung nach Prozent**  
 Geben Sie einen Prozentsatz an, um den die Datendatei wachsen kann.  
  
 **Vergrößerung nach Größe**  
 Geben Sie die Anzahl der Megabytes an, um die die Datendatei wachsen kann.  
  
### <a name="log-file-options"></a>Protokolldateioptionen  
 **Anfangsgröße**  
 Geben Sie die Anzahl der Megabytes für die Anfangsgröße der Protokolldatei an.  
  
 **Keine Vergrößerung zulässig**  
 Geben Sie an, ob die Protokolldatei die Größe der angegebenen Anfangsgröße übersteigen kann.  
  
 **Vergrößerung nach Prozent**  
 Geben Sie einen Prozentsatz an, um den die Protokolldatei wachsen kann.  
  
 **Vergrößerung nach Größe**  
 Geben Sie die Anzahl der Megabytes an, um die die Protokolldatei wachsen kann.  

### <a name="more-info"></a>Weitere Informationen
Weitere Informationen zu den Optionen für die Dateigröße, die auf dieser Seite angezeigt werden, finden Sie unter [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md). 

## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie einen Namen für die neue Datenbank angegeben und auf **OK**geklickt haben, wechselt das Dialogfeld **Datenbank erstellen** wieder zurück zur Seite **Ziel auswählen** . Weitere Informationen finden Sie unter [Ziel auswählen](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).  

