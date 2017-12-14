---
title: "DAC-Unterstützung für SQL Server-Objekte und -Versionen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: data-tier-applications
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data-tier application [SQL Server], supported objects
- objects [SQL Server], data-tier applications
ms.assetid: b1b78ded-16c0-4d69-8657-ec57925e68fd
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 939f92fab054aefc60c23500ed6207c3adef0e21
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dac-support-for-sql-server-objects-and-versions"></a>DAC-Unterstützung für SQL Server-Objekte und -Versionen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Eine Datenebenenanwendung (DAC) unterstützt die am häufigsten verwendeten [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Objekte.  
  
 **In diesem Thema**  
  
-   [Unterstützte SQL Server-Objekte](#SupportedObjects)  
  
-   [Unterstützung von Datenebenenanwendungen durch die Versionen von SQL Server](#SupportByVersion)  
  
-   [Beschränkungen für die Datenbereitstellung](#DeploymentLimitations)  
  
-   [Zusätzliche Überlegungen zu Bereitstellungsaktionen](#Considerations)  
  
##  <a name="SupportedObjects"></a> Unterstützte SQL Server-Objekte  
 Beim Erstellen oder Bearbeiten einer Datenebenenanwendung können nur unterstützte Objekte angegeben werden. Sie können keine DACs aus einer bestehenden Datenbank mit Objekten extrahieren, bei dieser registrieren oder in diese importieren, die in einer DAC nicht unterstützt werden. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützt in einer DAC die im Folgenden aufgeführten Objekte.  
  
|||  
|-|-|  
|DATABASE ROLE|FUNCTION: Inline-Tabellenwertfunktion|  
|FUNCTION: Tabellenwertfunktion mit mehreren Anweisungen|FUNCTION: Skalar|  
|INDEX: Gruppiert|INDEX: Nicht gruppiert|  
|INDEX: Räumlich|INDEX: Eindeutig|  
|LOGIN|Berechtigungen|  
|Rollenmitgliedschaften|SCHEMA|  
|Statistik|STORED PROCEDURE: Transact-SQL|  
|Synonyme|TABLE: CHECK-Einschränkung|  
|TABLE: Sortierung|TABLE: Spalte, einschließlich berechneter Spalten|  
|TABLE: Einschränkung, Standard|TABLE: Einschränkung, Fremdschlüssel|  
|TABLE: Einschränkung, Index|TABLE: Einschränkung, Primärschlüssel|  
|TABLE: Einschränkung, Eindeutig|TRIGGER: DML|  
|TYPE: HIERARCHYID, GEOMETRY, GEOGRAPHY|TYPE: Benutzerdefinierter Datentyp|  
|TYPE: Benutzerdefinierter Tabellentyp|USER|  
|VIEW||  
  
##  <a name="SupportByVersion"></a> Unterstützung von Datenebenenanwendungen durch die Versionen von SQL Server  
 Die Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bieten verschiedene Ebenen der Unterstützung für DAC-Vorgänge. Alle DAC-Vorgänge, die von einer Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt werden, werden von allen Editionen dieser Version unterstützt.  
  
 Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] unterstützen die folgenden DAC-Vorgänge:  
  
-   Export und Extrahierung werden von allen unterstützten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Versionen unterstützt.  
  
-   Alle Vorgänge werden von [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] und allen Versionen von [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]und [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]unterstützt.  
  
-   Alle Vorgänge werden von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Service Pack 2 (SP2) oder höher und [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 oder höher unterstützt.  
  
 Das DAC-Framework umfasst die clientseitigen Tools zum Erstellen und Verarbeiten von DAC-Paketen und Exportdateien. Das DAC-Framework ist in den folgenden Produkten enthalten:  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] umfassen DAC Framework 3.0, das alle DAC-Vorgänge unterstützt.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 und Visual Studio 2010 SP1 umfassten DAC-Framework 1.1, das alle DAC-Vorgänge mit Ausnahme des Exports und Imports unterstützt.  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] und Visual Studio 2010 umfassen DAC Framework 1.0, das alle DAC-Vorgänge außer Export, Import und direkte Upgrades unterstützt.  
  
-   Die Clienttools früherer Versionen von SQL Server oder Visual Studio unterstützen keine DAC-Vorgänge.  
  
 Mit einer Version des DAC-Frameworks erstellte DAC-Pakete und Exportdateien können nicht von früheren Versionen des DAC-Frameworks verarbeitet werden. Beispielsweise kann ein DAC-Paket, das mit den [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] -Clienttools extrahiert wurde, nicht mithilfe der [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] -Clienttools bereitgestellt werden.  
  
 Mit einer Version des DAC-Frameworks erstellte DAC-Pakete und Exportdateien können von allen höheren Versionen des DAC-Frameworks verarbeitet werden. Beispielsweise kann ein DAC-Paket, das mit den [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] -Clienttools extrahiert wurde, mit den Clienttools von [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 oder höher bereitgestellt werden.  
  
##  <a name="DeploymentLimitations"></a> Beschränkungen für die Datenbereitstellung  
 Beachten Sie diese Genauigkeitseinschränkungen im DAC Framework-Datenbereitstellungsmodul in SQL Server 2012 SP1. Die Beschränkungen gelten für die folgenden DAC-Framework-Aktionen: Bereitstellen oder Veröffentlichen einer DACPAC-Datei und Importieren einer BACPAC-Datei.  
  
1.  Verlust von Metadaten unter bestimmten Bedingungen und für bestimmte Basistypen innerhalb von sql_variant-Spalten. In den jeweiligen Fällen wird eine Warnung mit folgendem Inhalt angezeigt:  **Bestimmte Eigenschaften für spezifische Datentypen, die innerhalb einer sql_variant-Spalte verwendet werden, werden bei der Bereitstellung durch das DAC-Framework nicht beibehalten**.  
  
    -   Basistypen MONEY, SMALLMONEY, NUMERIC, DECIMAL: Die Genauigkeit wird nicht beibehalten.  
  
        -   Basistypen DECIMAL/NUMERIC mit der Genauigkeit 38: Die sql_variant-Metadaten für "TotalBytes" sind immer auf 21 festgelegt.  
  
    -   Alle Textbasistypen. Die Standardsortierung der Datenbank wird auf sämtlichen Text angewendet.  
  
    -   BINARY-Datentypen: Die MaxLength-Eigenschaft wird nicht beibehalten.  
  
    -   Basistypen TIME, DATETIMEOFFSET: Die Genauigkeit ist immer auf 7 festgelegt.  
  
2.  Verlust von Daten innerhalb von sql_variant-Spalten. In den jeweiligen Fällen wird eine Warnung mit folgendem Inhalt angezeigt: **Wenn DAC-Framework in einer sql_variant-Spalte einen DATETIME2-Wert mit mehr als drei Dezimalstellen bereitstellt, tritt ein Datenverlust auf. Der DATETIME2-Wert ist während der Bereitstellung auf drei Dezimalstellen begrenzt.**  
  
    -   Basistyp DATETIME2 mit mehr als drei Dezimalstellen: Die Anzahl der Dezimalstellen ist auf 3 beschränkt.  
  
3.  Der Bereitstellungsvorgang schlägt unter den folgenden Bedingungen innerhalb von sql_variant-Spalten fehl. In den betreffenden Fällen wird ein Dialogfeld mit folgender Meldung angezeigt:  **Fehler beim Vorgang aufgrund von Datenbeschränkungen in DAC-Framework.**  
  
    -   Basistypen DATETIME2, SMALLDATETIME und DATE: Wenn der Wert außerhalb des DATETIME-Bereichs liegt; die Jahresangabe ist z. B. kleiner als 1753.  
  
    -   Basistypen DECIMAL, NUMERIC: Wenn die Genauigkeit des Werts größer als 28 ist.  
  
##  <a name="Considerations"></a> Zusätzliche Überlegungen zu Bereitstellungsaktionen  
 Beachten Sie Folgendes bei DAC-Framework-Datenbereitstellungsaktionen:  
  
-   **Extrahieren/Exportieren** : Für Aktionen, bei denen mithilfe des DAC-Frameworks ein Paket auf Grundlage einer Datenbank erstellt wird – z.B. Extrahieren einer DACPAC-Datei und Exportieren einer BACPAC-Datei –, gelten diese Beschränkungen nicht. Die im Paket enthaltenen Daten zeichnen sich durch vollständige Datentreue mit den Daten in der Quelldatenbank aus. Falls eine dieser Bedingungen im Paket vorliegt, enthält das Extrahierungs-/Exportprotokoll eine Zusammenfassung der Probleme anhand der oben beschriebenen Meldungen. Das soll den Benutzer vor möglichen Problemen mit der Datenbereitstellung warnen, die beim erstellten Paket auftreten können. Darüber hinaus sieht der Benutzer die folgende Zusammenfassungsmeldung im Protokoll: **Die Genauigkeit der Datentypen und Werte, die in dem von DAC-Framework erstellten DAC-Paket gespeichert sind, wird durch diese Beschränkungen nicht beeinträchtigt; die Beschränkungen gelten nur für die Datentypen und Werte, die sich aus der Bereitstellung eines DAC-Pakets auf einer Datenbank ergeben. Weitere Informationen zu den betroffenen Daten und eine Problemumgehung dieser Beschränkung finden Sie in** [diesem Thema](http://go.microsoft.com/fwlink/?LinkId=267086).  
  
-   **Bereitstellen/Veröffentlichen/Importieren**: Für Aktionen, bei denen mithilfe des DAC-Frameworks ein Paket in einer Datenbank bereitgestellt wird – z.B. Bereitstellen oder Veröffentlichen einer DACPAC-Datei und Importieren einer BACPAC-Datei – sind diese Beschränkungen gültig. Die Daten in der Zieldatenbank entsprechen möglicherweise keiner vollständig datentreuen Ausgabe der im Paket enthaltenen Daten. Das Bereitstellungs-/Importprotokoll enthält für jede Instanz, auf der das Problem auftritt, die oben angegebene Meldung. Der Vorgang wird durch Fehler zwar blockiert (siehe Kategorie 3 oben), anschließend jedoch mit den übrigen Warnungen fortgesetzt.  
  
     Weitere Informationen zu den von diesem Szenario betroffenen Daten und eine Problemumgehung dieser Beschränkung für Bereitstellungs-/Veröffentlichungs-/Importaktionen finden Sie in [diesem Thema](http://go.microsoft.com/fwlink/?LinkId=267087).  
  
-   **Problemumgehungen** : Durch Extrahierungs- und Exportvorgänge werden BCP-Datendateien mit vollständiger Datentreue in die DACPAC- oder BACPAC-Datei geschrieben. Zur Umgehung von Beschränkungen verwenden Sie das SQL Server-Befehlszeilenhilfsprogramm BCP.exe, um eine vollständig datentreue Version der Daten aus einem DAC-Paket in einer Zieldatenbank bereitzustellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenebenenanwendungen](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
