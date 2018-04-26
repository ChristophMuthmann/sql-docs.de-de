---
title: Globale Einstellungen (Protokollierung) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
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
ms.assetid: 0d033492-5ec3-473a-8de1-821894ec9518
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07b857c7fbd9d303eb100e6bf7df5785f1ec3f6c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="global-settings-logging--mysqltosql"></a>Globale Einstellungen (Protokollierung) (MySQLToSQL)
Verwenden der **globale Einstellungen** (Dialogfeld), um die protokollierungseinstellungen für SSMA anzugeben. In der Regel ändern Sie diese Einstellungen nur bei der Arbeit mit Microsoft Support Services.  
  
Zum Zugriff auf dieses Dialogfeld, in dem **Tools** klicken Sie im Menü **globale Einstellungen** , und klicken Sie dann auf die **Protokollierung** unten im linken Bereich.  
  
## <a name="options"></a>enthalten  
**Nachrichten-Ebene**  
Die folgenden Optionen sind verfügbar unter **Nachrichten Ebene**:  
  
|Option|Description|  
|----------|---------------|  
|**[alle Kategorien]**|Verwendet, um den Protokolliergrad auf für alle der folgenden Optionen festlegen.|  
|**Collector**|Metadaten über das Quellschema sammelt und speichert es in das Projekt.|  
|**Konverter**|Strukturen der Quell-Datenbankobjekte wie Tabellen und gespeicherte Prozeduren in entsprechende konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Strukturen.|  
|**Daten migrator**|Migration von Daten aus der Quelldatenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|**Formatierer**|Unterkomponente des Konverters, die generiert Skripts für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schema.|  
|**Grafische Benutzeroberfläche**|Nachrichten, die angezeigt werden, wenn Sie das SSMA-Tool verwenden.|  
|**Linker**|Löst SQL-Bezeichner auf und enthält Informationen zu anderen Komponenten.|  
|**Andere**|Alle Nachrichten, die nicht in einer beliebigen anderen Kategorie vorhanden sind.|  
|**Parser**|Analysiert das Quellschema an.|  
|**Für die domänensynchronisierung**|Lädt Datenquelle Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|**TreeConverter**|Konvertiert Objekte in der Quell-Metadaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten.|  
  
Für jede einzelne Option unter **Nachrichten Ebene**, konfigurieren Sie einen der folgenden Protokolliergrade für SSMA:  
  
|||  
|-|-|  
|**Schwerwiegender Fehler**|Geschrieben Sie nur schwerwiegende Meldungen in das Protokoll.|  
|**Fehler**|Geschrieben Sie Fehler und schwerwiegende Meldungen in das Protokoll.|  
|**Warnung**|Geschrieben Sie Warnung, Fehler und schwerwiegende Meldungen in das Protokoll.|  
|**Info**|Geschrieben Sie Information, Warnung, Fehler und schwerwiegende Meldungen in das Protokoll.|  
|**Debuggen**|Alle Nachrichten, einschließlich Debugmeldungen in das Protokoll zu schreiben.|  
  
**Protokolldateipfad**  
Der Dateipfad und der Name der SSMA-Protokolldateien. Um einen anderen Namen anzugeben, klicken Sie auf den aktuellen Pfad aus, und klicken Sie dann auf die Schaltfläche zum Durchsuchen (**...** ) Schaltfläche.  
  
**Die Größe der Protokolldatei**  
Die maximale Größe der Protokolldatei in KB. Die Mindestgröße beträgt 10 KB. Die Standardgröße ist 10240 KB.  
  
**Gesamtanzahl der Protokolldateien**  
Wenn ein Protokoll gefüllt wird, wird SSMA benennen Sie die Log-Datei und einen neuen startet. Geben Sie mit dieser Einstellung die maximale Anzahl von Protokolldateien beibehalten. Der Mindestwert beträgt 2.  
  
