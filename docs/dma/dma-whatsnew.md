---
title: Neuheiten bei Data Migration Assistant (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 10/03/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, new features
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07d72eb6c4d40c3e61f4292616f9eda99d6d4742
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="whats-new-in-data-migration-assistant"></a>Neuigkeiten im Daten-Migrations-Assistent

In diesem Thema werden die Ergänzungen in jeder Version von Data Migration Assistant (DMA) aufgelistet.

## <a name="dma-v33"></a>DMA v3. 3
Die v3. 3-Version von DMA ermöglicht die Migration einer lokalen SQL Server-Instanz auf die neue Version von SQL Server 2017 unter Windows und Linux. Während der gesamten Migrationsworkflow für Windows und Linux identisch ist, sind das Verschieben in SQL Server-2017 für Linux einige zusätzliche Überlegungen erforderlich.

### <a name="specifying-the-back-up-path"></a>Angeben des Pfads sichern
Linux und Windows verwenden unterschiedliche pfadformate. Migrieren zu SQL Server-2017 unter Linux folglich erfordert, dass der Benutzer auf dem Windows- und Linux-Versionen des Pfads zum Speicherort der physischen Datei angeben. Dies geschieht auf unterschiedliche Weise je nach Speicherort der physischen Datei.
Wenn der physische Datei sichern auf einem Computer ausgeführt wird:
- Linux, verwenden Sie freigeben einer "Samba" um die Datei mit anderen Computern im Netzwerk freizugeben.
-   Windows, verwenden Sie den Befehl "Mnt" Bereitstellen die Freigabe auf dem Computer, auf dem Linux ausgeführt wird.

> [!NOTE]
> Details der Verwendung einer Freigabe "Samba" oder den Befehl "Mnt" sind nicht Gegenstand dieses Artikels.

### <a name="migrating-windows-logins"></a>Migrieren von Windows-Anmeldenamen
Während die Migration von Active Directory (AD)-Anmeldungen von SQL Server-2017 unter Linux offiziell unterstützt wird, benötigt er zusätzliche Konfiguration ordnungsgemäß funktioniert. Finden Sie unter [Active Directory-Authentifizierung mit SQL Server on Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-active-directory-authentication) für ausführliche Informationen zum Einrichten von Active Directory-Anmeldungen auf SQL Server-2017 unter Linux. Danach das Setup abgeschlossen ist, können Sie die Active Directory-Anmeldungen wie gewohnt migrieren. Standard-SQL-Authentifizierung funktioniert erwartungsgemäß ohne dass eine zusätzliche Konfiguration.

## <a name="dma-v32"></a>DMA v3. 2
Die v3. 2-Version von DMA umfasst die folgenden Hinzufügungen:

- Migration von Schema und Daten werden mit Azure SQL-Datenbank aus einer lokalen SQL Server-Datenbanken aktiviert, wobei ein neuer Migrationsworkflow für die.

- DMA während der Migration zu Azure SQL-Datenbank Schema Skripts Datenbankobjekte für die Quelle, bietet Anleitungen, mögliche Kompatibilitätsprobleme zu beheben und anschließend wird das Schema auf Azure bereitgestellt.

## <a name="dma-v31"></a>DMA v3. 1
Die v3. 1-Version von DMA umfasst die folgenden Hinzufügungen:

- Verbesserte Assessment-Empfehlungen für Azure SQL-Datenbanken in Bezug auf die datenbanksortierungen, die Verwendung von nicht unterstützten gespeicherten Systemprozeduren und CLR-Objekte.

- Assessment-Anleitung für Kompatibilitätsgrad 130 zur Verfügung, die 120, 110 und 100, bei der Migration zu Azure SQL-Datenbanken.

## <a name="dma-v30"></a>DMA v3. 0
Die v3. 0-Version von DMA erweitert die Bewertung der Azure SQL-Datenbank um eine umfassende Empfehlungen zum Beheben von Problemen im Zusammenhang mit bereitzustellen:

- Migration von Blockierungsproblemen.

- Teilweise oder nicht unterstützte Features und Funktionen.

## <a name="dma-v21"></a>DMA v2. 1
Die v2. 1-Version von DMA umfasst die folgenden Hinzufügungen:
- Befehlszeilen-Unterstützung zum Ausführen von Bewertungen in einem unbeaufsichtigten Modus, was dabei hilft, Bewertungen Größenordnungen ausführen. Weitere Einzelheiten finden Sie unter [ausführen Daten Migrations-Assistenten über die Befehlszeile](dma-commandline.md).

- Leistungsverbesserungen beim Starten von Benutzern und DMA zu schließen.

- Die Fähigkeit zum Konfigurieren von SQL-Verbindungstimeout. Weitere Einzelheiten finden Sie unter [Konfigurationseinstellungen für Daten Migration Assistant](dma-configurationsettings.md).

## <a name="dma-v20"></a>DMA v2. 0
Die v2. 0-Version von DMA enthält verbesserte Stretch-Datenbank Feature Empfehlungen zur richtige priorisierte Tabellen enthalten, die die speichereinsparungen zu maximieren.

## <a name="dma-v10"></a>DMA v1. 0
Die v1. 0-Version von DMA ist die erste Version, und bietet für:
- Ermittlung von Problemen, die ein Upgrade auf eine lokale Version von SQL Server betreffen können. Alle Ergebnisse werden als Kompatibilitätsprobleme beschrieben, und sie werden in der folgenden Bereiche kategorisiert:
    -   Wichtige Änderungen
    - Verändertes Programmverhalten
    - Als veraltet markierte Funktionen

- Ermittlung von neuen Funktionen in der Ziel-SQL Server-Plattform, die ein Upgrade die Datenbank profitieren kann. Alle Ergebnisse werden als Funktion Empfehlungen beschrieben, und sie werden in der folgenden Bereiche kategorisiert:
    - Leistung
    - Security
    - Speicherung

-   Moderne Benutzeroberfläche, um Bewertungen ausführen.

## <a name="see-also"></a>Siehe auch

[Übersicht über Data-Migrations-Assistenten](../dma/dma-overview.md)
