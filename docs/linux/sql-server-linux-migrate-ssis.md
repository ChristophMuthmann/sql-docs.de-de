---
title: Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS | Microsoft Docs
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7317cad5aa1e77653431c128ce1549bc4349e18
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS

In diesem Thema wird beschrieben, wie SQL Server Integration Services (SSIS)-Pakete auf Linux ausgeführt wird. SSIS löst Probleme bei der Integration von komplexen Daten Laden von Daten aus mehreren Quellen und Formaten, Transformieren und Bereinigen der Daten und mehrere Ziele aktualisieren. 

SSIS-Pakete auf Linux laufende können mit Microsoft SQL Server, die auf Windows lokal oder in der Cloud, die unter Linux oder in Docker verbinden. Sie können auch mit Azure SQL-Datenbank, Azure SQL Data Warehouse und ODBC-Datenquellen verbinden.

Sie können SSIS verwenden, um Pakete auf Linux ausführen, wenn Sie auch zum Erstellen und verwalten Sie Pakete auf einen Windows-Computer verfügen. Die SSIS-Entwurf und die Verwaltungstools sind Windows-Anwendungen. 

## <a name="prerequisites"></a>Erforderliche Komponenten

Um SSIS-Pakete auf einem Linux-Computer auszuführen, müssen Sie zuerst SQL Server Integration Services installieren. Installationsanweisungen finden Sie unter [Installieren von SQL Server Integration Services](sql-server-linux-setup-ssis.md).

## <a name="run-an-ssis-package"></a>Führen Sie ein SSIS-Paket

Um ein SSIS-Paket auf einem Linux-Computer auszuführen, führen Sie folgende Schritte aus:

1.  Kopieren Sie das SSIS-Paket auf dem Linux-Computer.
2.  Führen Sie den folgenden Befehl aus:
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="more-about-ssis-on-linux"></a>Weitere Informationen zum SSIS unter Linux

**ODBC-Verbindungen**. Mit SSIS unter Linux CTP-Version 2.1 aktualisiert und höher können SSIS-Pakete auf Linux ODBC-Verbindungen. Diese Funktion wurde mit SQL Server und die MySQL-ODBC-Treiber getestet, aber auch mit jeder Unicode-ODBC-Treiber arbeiten, die die ODBC-Spezifikation berücksichtigt werden sollen. Zur Entwurfszeit können Sie entweder einen DSN oder eine Verbindungszeichenfolge in die ODBC-Verbindung angeben; Sie können auch Windows-Authentifizierung verwenden. Weitere Informationen finden Sie unter der [Blogbeitrag Ankündigung ODBC-Unterstützung unter Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

**Pfade**. SSIS unter Linux unterstützt keine Pfade für Linux-Format, aber Windows-Stil Pfade Linux-Stil Pfade zur Laufzeit zugeordnet. Geben Sie im Windows-Format Pfade im SSIS-Pakete. Klicken Sie dann, z. B. SSIS unter Linux ordnet den Windows-Stil Pfad `C:\test` auf den Linux-Stil Pfad `/test`.

**Bereitstellen von Paketen**. Sie können nur Pakete im Dateisystem unter Linux in dieser Version speichern. Die SSIS-Katalogdatenbank und die legacy-SSIS-Dienst sind nicht verfügbar unter Linux für die Bereitstellung von Paketen und Speicher.

**Planen von Paketen**. SQL-Agent können für Linux keine um Ausführung in dieser Version des Pakets zu planen.

**Andere Einschränkungen und bekannte Probleme**. Die folgenden Funktionen werden in dieser Version nicht unterstützt, beim Ausführen von SSIS-Pakete auf Linux:
  - SSIS-Katalogdatenbank
  - Geplante paketausführung vom SQL-Agent
  - Windows-Authentifizierung
  - Drittanbieter-Komponenten
  - Change Data Capture (CDC)
  - SSIS für horizontales Skalieren
  - Azure FeaturePack für SSIS
  - Unterstützung für Hadoop und HDFS
  - Microsoft Connector for SAP BW

Andere Einschränkungen und bekannte Probleme mit SSIS unter Linux finden Sie in der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md#ssis).

Weitere Informationen zu SSIS unter Linux finden Sie unter den folgenden Blogbeiträgen:

-   [SSIS unter Linux finden Sie in SQL Server 2017 CTP2. 1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC ist in SSIS unter Linux (SQL Server 2017 CTP-Version 2.1 aktualisiert) unterstützt.](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-about-ssis"></a>Weitere Informationen zum SSIS

Microsoft SQL Server Integration Services (SSIS) ist eine Plattform zum Erstellen von Hochleistungs-datenintegrationslösungen, z. B. extrahieren, Transformieren und laden (ETL) von Paketen für Datawarehousing. Weitere Informationen zu SSIS finden Sie unter [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md).

SSIS umfasst die folgenden Funktionen:
- grafische Tools und Assistenten zum Erstellen und Debuggen von Paketen für Windows
- eine Vielzahl von Aufgaben zum Ausführen von Workflowfunktionen wie z. B. FTP-Vorgänge, Ausführen von SQL-Anweisungen und Senden von e-Mail-Nachrichten
- eine Vielzahl von Datenquellen und Zielen zum Extrahieren und Laden von Daten
- eine Reihe von Transformationen zum Bereinigen, aggregieren, Zusammenführen und Kopieren von Daten
- Anwendungsprogrammierschnittstellen (APIs) für die Erweiterung von SSIS mit Ihren eigenen benutzerdefinierten Skripts und Komponenten

Laden Sie zum Einstieg in SSIS die neueste Version des [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md). Führen Sie dann das Lernprogramm [wie SSIS, zum Erstellen eines ETL-Pakets](https://msdn.microsoft.com/en-us/library/ms169917.aspx).

## <a name="see-also"></a>Siehe auch
- [Erfahren Sie mehr über SQL Server Integration Services](https://msdn.microsoft.com/en-us/library/ms141026.aspx)
- [SQL Server Integration Services (SSIS) Entwicklungs- und Verwaltungstools](https://msdn.microsoft.com/en-us/library/ms140028.aspx)
- [SQL Serverintegration Services-Lernprogramme](https://msdn.microsoft.com/en-us/library/jj720568.aspx)

