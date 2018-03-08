---
title: "Neuheiten bei SSMA für die Access(AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 03/01/2018
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
caps.latest.revision: 
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 487fa165ce29ae2ae2a7fffe4463e88fb45001c6
ms.sourcegitcommit: 6a5b80cac78fe5c2d2567a391daa335f9b4b3637
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2018
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>Was ist neu in SSMA für Access (AccessToSQL)
In diesem Thema werden die SSMA für Access-Änderungen in jeder Version aufgelistet.  

## <a name="ssma-v77"></a>SSMA v7.7
Die v7.7-Version von SSMA für Access umfasst die folgenden Änderungen:
- SSMA für Access wurde mit den entsprechenden Updates verbessert, die Qualität und Konvertierung Metriken zu verbessern.
- Basierend auf der großen Nachfrage ist die 32-Bit-Version von SSMA für Access zurück. Im Vergleich zu die vorherige Implementierung (vor v7.4), es gibt zwei Installationspakete, aber sie können nicht nebeneinander installiert werden. Daher müssen Sie die am besten geeignete Version basierend auf die Konnektivitätskomponenten verwaltungsstufe auswählen. Es ist immer vorzuziehen, nach Möglichkeit die 64-Bit-Version zu verwenden.

> [!IMPORTANT]
> SSMA v7.4 und höheren Versionen ist .net 4.5.2 eine Installation Voraussetzung.

## <a name="ssma-v76"></a>SSMA v7.6
Die v7.6-Version von SSMA für Access wurde verbessert, mit der targeted Korrekturen, die Qualität und Konvertierung Metriken zu verbessern und Unterstützung für SQL Server-2017 (öffentliche Vorschau). Unterstützung für SQL Server-2017 auf Windows- und Linux ist als öffentliche Vorschau verfügbar und sollte nicht für die Produktionsmigrationen verwendet werden.

> [!IMPORTANT]
> SSMA v7.4 und höhere Versionen .net 4.5.2 ist eine Voraussetzung für Installation, und die 32-Bit-Version des Tools wurde eingestellt.

## <a name="ssma-v75"></a>SSMA v7.5
Die Version 7.5 von SSMA für Access wurde verbessert, mit zahlreiche Verbesserungen, um größere Barrierefreiheit für Personen mit behinderungen sicherzustellen.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA 7.5. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.

## <a name="ssma-v74"></a>SSMA v7.4
Die v7.4-Version von SSMA für Access umfasst die folgenden Änderungen:
- Die **Abfragetimeout** Option ist während der Ermittlung an Quelle und Ziel Schema verfügbar.
![Option Timeout für Remoteabfragen](../media/query-timeout_red.png)

- Die Qualität und Konvertierung Metrik wurde mit targeted Fehlerbehebungen, aufgrund von Kundenfeedback verbessert.

> [!IMPORTANT]
> .NET 4.5.2 ist eine Voraussetzung für die Installation von SSMA v7.4. Darüber hinaus wird v7.4 ab, die 32-Bit-Version von SSMA nicht mehr unterstützt wird.

## <a name="ssma-v73"></a>SSMA v7.3
Die V7. 3-Version von SSMA für Access umfasst die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- SSMA Extensibility Framework verfügbar gemacht werden, über die folgenden Elemente:
  - Exportieren Sie zu einem SQL Server Data Tools (SSDT)-Projekt bereit.
    -   Sie können jetzt Schemaskripts von SSMA in ein SSDT-Projekt exportieren. Die Schemaskripts können Sie zusätzliche Schemas ändern und Bereitstellen der Datenbank.
![Speichern Sie als SSDT-Befehl "Projekt"](../media/export-schema-scripts_red.png)

  - Bibliotheken, die zum Ausführen von benutzerdefinierter Konvertierungen von SSMA genutzt werden können.
    - Jetzt können Sie Code erstellen, die benutzerdefinierte Syntax Konvertierungen und Konvertierungen, die zuvor vom SSMA verarbeitet wurden nicht verarbeiten kann.
      - Anweisungen zum Erstellen eines benutzerdefinierten Konverters stehen in diesem Blogbeitrag [Erweitern von SQL Server Migration Assistant Funktionen](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Beispielprojekt für die Konvertierung herunterladen dies [Blogbeitrag](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2
Die V7. 2-Version von SSMA für Access umfasst die folgenden Änderungen:
- Verbesserte Qualität und Konvertierung Metrik mit dem Ziel Korrekturen, die basierend auf Kundenfeedback.
- Telemetrie-Erweiterungen bieten eine bessere Datenpunkte, um Kundenprobleme zu beheben und zu verbessern SSMAs-Wechselkurse.

## <a name="ssma-v71"></a>SSMA v7.1
Die v7.1-Version von SSMA für Access umfasst die folgenden Änderungen:
- SQL Server-2017 auf Windows- und Linux CTP1 ist jetzt eine unterstützte Zielplattform für die Migration. Dieses Feature ist in der technischen Vorschau und Verschieben von Schema und Daten an SQL-Zielserver unterstützt.
- SSMA unterstützt jetzt die automatische Updates, um die neueste Version von SSMA herunterladen, sobald es verfügbar ist.
- Installierbare SSMA-Binärdateien werden jetzt über Windows Installer-Paket-Dateien (.msi) übermittelt.

**Ressourcen**

[Erweitern von SQL Server Migration Assistant Funktionen](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>Mai 2016  
Die Mai 2016-Version von SSMA für Access umfasst die folgenden Änderungen:  
  
-  Offizielle Unterstützung für SQL Server 2016
-  Überprüfen Sie Installationsprogramm für .net 2.0 wird entfernt.
-  Feste "Speichern" Projekt"und"Projekt öffnen"-Befehle für SSMA-Konsole.
-  Feste "Securepassword"-Befehl für SSMA-Konsole.
-  Korrektur von Objekten für das erstmalige laden zählen.
-  Feste Tabellen Laden von Daten für die UI-Registerkarten für den Zugriff.
-  Korrektur von Bug in den globalen Einstellungen. 
   
## <a name="march-2016"></a>März 2016  
März 2016 Preview-Version von SSMA für Access umfasst die folgenden Änderungen:  
  
-  Unterstützung für die Migration zu SQL Server 2016.  
   
## <a name="january-2016"></a>Januar 2016  
Die Januar 2016 Wartung-Version von SSMA für Access umfasst die folgenden Änderungen:  
  
-  Feste Funktion ist ungültig für standardmäßig einen GUID-Felds (RFC 3894811).  
-  Feste hängt zum Importieren von Datensätzen mit SQL-Datenbank (Azure) (RFC 4919573).  
-  Hinzugefügte Ansicht der Protokoll-Menüelement zu SSMA (RFC 5706203).  
-  Hinzugefügte Telemetrie.  
  
## <a name="july-2014"></a>Juli 2014  
Die Juli 2014-Version von SSMA für Access umfasst die folgenden Änderungen:  
  
-   Verbesserte codekonvertierung für Azure SQL-Datenbank.  
-   Erweiterung Pack-Funktion zum Schema zur Unterstützung von Azure SQL-Datenbank verschoben.  
-   Getestete leistungsverbesserungen für Datenbanken mit mehr als 10 k-Objekten.  
-   UI-Verbesserungen für den Umgang mit einer großen Anzahl von Objekten hinzugefügt.  
-   Unterstützung für die Hervorhebung von "bekannte" LOB-Schemas (damit sie bei der Konvertierung ignoriert werden können).  
-   Geschwindigkeitsverbesserungen Konvertierung wird hinzugefügt.
-   Unterstützung für das Objekt anzeigen zählt in der Benutzeroberfläche.
-   Reduzierte Berichtsgröße von mehr als 25 %.
-   Verbesserte Fehlermeldungen für nicht verarbeitete Konstrukte.  
  
## <a name="april-2014"></a>April 2014  
Die Version April 2014 von SSMA für Access umfasst die folgenden Änderungen:  
  
-   Unterstützung für die MS SQL Server 2014 hinzugefügt.  
-   Korrigierte Fehler hinsichtlich Konvertierung in Azure.  
-   Korrigierte Fehler bezüglich unsichtbar Berichtsseiten in Internet Explorer 10.  
  
## <a name="january-2012"></a>Januar 2012  
Die Januar 2012-Version von SSMA für Access umfasst die folgenden Änderungen:  
  
-   Die Möglichkeit, den Benutzernamen und das Kennwort nicht bestehen, für die MS Access verknüpfte Tabellen nach der Migration wird bereitgestellt.  
-   Legen Sie die Cascade-Aktionen für Zirkuläre Verweise auf No Action.  
-   Sofern die richtige Nachrichten, der angibt, Cascade-Aktionen für Zirkuläre Verweise auf No Action festgelegt wurden.  
  
## <a name="july-2011"></a>Vom Juli 2011  
Die vom Juli 2011-Version von SSMA für Access umfasst die folgenden Änderungen:  
  
-   Verbesserte fehlerberichterstellung während der Datenmigration.  
  
## <a name="april-2011"></a>April 2011  
Die April 2011-Version von SSMA für Access umfasst die folgenden Änderungen:  
  
-   Hinzugefügt von einem einzelnen installierbaren "SSMA für Access", die unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" und SQL Azure.  
-   Die Fähigkeit zum Verbinden hinzugefügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"  
-   Hinzugefügte SSMA für Access-Konsole Version für die Abwärtskompatibilität unterstützen. Öffnen Sie die Projekte, die von früheren Versionen SSMA V5. 0 erstellt.
-   Wurde die Möglichkeit zur Installation von SSMA V5. 0-Produkts parallel dazu (SxS) mit älteren Versionen von SSMA-Produkt hinzugefügt.  
  
## <a name="july-2010"></a>Juli 2010  
Die Version vom Juli 2010 von SSMA für Access umfasst die folgenden Änderungen:  
  
-   Unterstützung für die Migration zu SQL Server 2008 R2 und SQL Azure hinzugefügt.
-   SQL Server und SQL Azure hinzugefügt eine sichere Verbindung.  
-   Unterstützung für Access 2010-Datenbanken hinzugefügt.
-   Eine neue Konsolenanwendung von SSMA, für die Ausführung über die Befehlszeile wird hinzugefügt.
-   Unterstützung für die SQL Server-Datentyp DateTime2 hinzugefügt.
  
## <a name="june-2008"></a>Juni 2008  
Die Juni 2008-Version von SSMA für Access umfasst die folgenden Änderungen:  
  
-   Unterstützung für Access 2007-Datenbanken hinzugefügt.  
  
## <a name="may-2007"></a>Mai 2007  
Die Version Mai 2007 von SSMA für Access umfasst die folgenden Änderungen:  
  
-   Unterstützung für den Zugriff auf Datenbanken, die Arbeitsgruppe Richtlinien verwenden.  
-   Die Möglichkeit, löschen konvertierte Objekte aus dem Metadaten-Explorer von SQL Server wird bereitgestellt.  
-   Unterstützung für die eingegebenen Kommentare in der SQL Server formatiert SQL-Modus.  
-   Verbesserungen im Objekt-Konvertierung hinzugefügt.  
  
## <a name="november-2006"></a>November 2006  
Vom November 2006 von SSMA für Access umfasst die folgenden Änderungen:  
  
-   Ein neue-Datenbankmigrations-Assistent, der Sie während der Migration einer einzelnen Datenbank aus den Zugriff auf führt hinzugefügt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
-   Eine neue konvertieren, laden, hinzugefügt und migrieren-Befehl, der konvertiert Access-Datenbanken, lädt die konvertierten Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und Migrieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in einem Schritt.  
-   Verbesserte Migration. Fragen Sie die Migration nun konvertiert mehr Abfragen mit Ansichten auswählen. Weitere Informationen finden Sie unter [den Zugriff auf Datenbankobjekte konvertieren](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c).  
-   Die Möglichkeit zum Bearbeiten von Tabellen- und Eigenschaften für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Tabelle** Registerkarte.  
-   Hinzugefügte neue globale Einstellungen:  
    -   Wahlweise können Sie zum Anzeigen von Zeilennummern im Editor-Fenstern.  
    -   Sie können konfigurieren SSMA aufgefordert werden, um doppelt vorhandene Objekte zu ersetzen, oder Sie können immer oder niemals ersetzen doppelte Objekte während der schemakonvertierung.  
-   Eine neue Konvertierungsoption, mit dem Sie angeben, ob SSMA eine Warnung angezeigt, wenn eine komplexe Abfrage einen Platzhalter enthält hinzugefügt.  
  
## <a name="july-2006"></a>Juli 2006  
Die Version von Juli 2006 von SSMA für Access war die erste Version.
