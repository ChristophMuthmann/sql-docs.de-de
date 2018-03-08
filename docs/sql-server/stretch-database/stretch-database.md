---
title: Stretch Database | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database
ms.assetid: ce6db775-21a5-40bc-95a1-f560376d4ee2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 30361d4466b7495945a7dae857bbcd52fd86103a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="stretch-database"></a>Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Mithilfe von Stretch Database werden Ihre kalten Daten transparent und sicher in die Microsoft Azure-Cloud migriert.  
  
 Wenn Sie möglichst schnell und einfach mit Stretch Database starten möchten, lesen Sie [Erste Schritte durch Ausführen des Assistenten zum Aktivieren von Stretch für eine Datenbank](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md).  
  
## <a name="what-are-the-benefits-of-stretch-database"></a>Welche Vorteile bietet Stretch Database?  
 Stretch Database bietet die folgenden Vorteile:  
  
 **Kostengünstige Verfügbarkeit für kalte Daten**  
 Dynamische Ausdehnung von warmen und kalten Transaktionsdaten von SQL Server auf Microsoft Azure mit SQL Server Stretch Database. Im Gegensatz zu typischen Speicherlösungen für kalte Daten sind Ihre Daten online und stehen stets für Abfragen zur Verfügung. Sie können längere Zeitziele für die Datenaufbewahrung erreichen, ohne mit großen Tabellen, wie einem Kundenbestellungsverlauf, die Bank zu sprengen. Nutzen Sie die niedrigen Kosten von Azure, statt Geld in die Skalierung von teurem, lokalem Speicher zu investieren. Indem Sie die Preisstufe auswählen und Einstellungen im Azure-Portal konfigurieren, behalten Sie die Kontrolle über Preise und Kosten. Skalieren Sie ganz nach Bedarf hoch oder herunter. Details dazu finden Sie unter [SQL Server Stretch Database – Preise](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/) .  
  
 **Keine Änderungen an Abfragen oder Anwendungen erforderlich**  
 Greifen Sie nahtlos auf Ihre SQL Server-Daten zu, unabhängig davon, ob diese lokal oder per Stretching in der Cloud gespeichert sind.  Sie legen die Richtlinie fest, die bestimmt, wo Daten gespeichert werden, und SQL Server übernimmt die Verschiebung der Daten im Hintergrund. Die gesamte Tabelle ist ständig online und kann jederzeit abgefragt werden. Und für Stretch Database sind keine Änderungen an vorhandenen Abfragen oder Anwendungen erforderlich – der Speicherort der Daten ist für die Anwendung vollständig transparent.  
  
 **Optimiert die lokale Wartung von Daten**  
 Reduzieren Sie den Aufwand für die lokale Verwaltung und Speicherung Ihrer Daten. Sicherungen für Ihre lokalen Daten werden schneller ausgeführt und innerhalb des Wartungsfensters abgeschlossen. Sicherungen des Cloudanteils Ihrer Daten werden automatisch ausgeführt. Der lokale Speicherbedarf wird erheblich reduziert. Azure-Speicher kann bis zu 80 % günstiger als das Hinzufügen lokaler SSDs sein.  
  
 **Ihre Daten bleiben selbst während der Migration sicher**  
 Bleiben Sie gelassen, wenn Sie für Ihre wichtigsten Anwendungen ein sicheres Stretching in die Cloud durchführen. Das Always Encrypted-Feature von SQL Server bietet Schutz für Ihre Daten während des Verschiebens. Sicherheit auf Zeilenebene, (RLS, Row Level Security) und andere hoch entwickelte Sicherheitsfeatures von SQL Server funktionieren auch in Kombination mit Stretch Database und schützen Ihre Daten.  
  
## <a name="what-does-stretch-database-do"></a>Wie funktioniert Stretch Database?  
 Nachdem Sie Stretch Database für eine SQL Server-Instanz, eine Datenbank und mindestens eine Tabelle aktiviert haben, beginnt Stretch Database in Hintergrund, Ihre kalten Daten nach Azure zu migrieren.  
  
-   Wenn Sie kalte Daten in einer separaten Tabelle speichern, können Sie die gesamte Tabelle migrieren.  
  
-   Wenn Ihre Tabelle sowohl heiße als auch kalte Daten enthält, können Sie eine Filterfunktion zum Auswählen der zu migrierenden Zeilen angeben.

**Vorhandene Abfragen und Client-Apps müssen nicht geändert werden.** Sie haben auch weiterhin nahtlosen Zugriff sowohl auf lokale als auch auf Remotedaten, sogar während der Datenmigration. Bei Remoteabfragen tritt eine geringfügige Latenz auf, diese Wartezeit macht sich jedoch nur beim Abfragen der kalten Daten bemerkbar.

**Stretch Database stellt sicher, dass keine Daten verloren gehen** , falls bei der Migration ein Fehler auftritt. Sie weist außerdem Logik für Wiederholungsversuche zur Behandlung von Verbindungsproblemen auf, die möglicherweise während der Migration auftreten. Eine dynamische Verwaltungsansicht gibt über den Status der Migration Auskunft.

**Sie können die Datenmigration anhalten** , um Probleme auf dem lokalen Server zu beheben oder die verfügbare Netzwerkbandbreite zu maximieren.  
  
 ![Überblick über Stretch-Datenbank](../../sql-server/stretch-database/media/stretch-overview.png "Überblick über Stretch-Datenbank")  
  
## <a name="is-stretch-database-for-you"></a>Ist Stretch Database die richtige Wahl für Sie?  
 Wenn die folgenden Aussagen auf Sie zutreffen, kann Stretch Database Ihnen vielleicht beim Erfüllen Ihrer Anforderungen und beim Lösen Ihrer Probleme helfen.  
  
|Wenn Sie ein Entscheidungsträger sind|Wenn Sie ein Datenbankadministrator sind|  
|--------------------------------|---------------------|  
|Ich muss Transaktionsdaten über einen langen Zeitraum aufbewahren.|Die Größe meiner Tabellen ist nicht mehr praktikabel zu verwalten.|  
|Manchmal müssen die kalten Daten abgefragt werden.|Meine Benutzer geben an, dass sie Zugriff auf die kalten Daten wünschen, sie nutzen sie jedoch nur selten.|  
|Ich verfüge über Apps, einschließlich älterer, die ich nicht aktualisieren möchte.|Ich muss weiterhin Speicher kaufen und hinzufügen.|  
|Ich suche nach einer Möglichkeit, Geld für Speicher zu sparen.|Ich kann derart große Tabellen nicht innerhalb des SLAs sichern oder wiederherstellen.|  
  
## <a name="what-kind-of-databases-and-tables-are-candidates-for-stretch-database"></a>Welche Arten von Datenbanken und Tabellen bilden die Kandidaten für Stretch Database?  
 Stretch Database ist auf Transaktionsdatenbanken ausgerichtet, bei denen großen Mengen von kalten Daten normalerweise in einer kleinen Anzahl von Tabellen gespeichert sind. Diese Tabellen können mehr als eine Milliarde Zeilen enthalten.  
  
 Wenn Sie das Feature für temporale Tabellen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwenden, nutzen Sie Stretch Database, um die zugeordnete Verlaufstabelle ganz oder teilweise zum kostengünstigen Speicher in Azure zu migrieren. Weitere Informationen finden Sie unter [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md).  
  
 Verwenden Sie den Stretch Database-Ratgeber, ein Feature des Aktualisierungsratgebers für SQL Server 2016, um Datenbanken und Tabellen für Stretch Database zu identifizieren. Weitere Informationen finden Sie unter [Identifizieren von Datenbanken und Tabellen für Stretch Database durch Ausführen des Ratgebers für Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md). Informationen zu möglicherweise blockierenden Problemen finden Sie unter [Einschränkungen für Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md).  

## <a name="test-drive-stretch-database"></a>Machen Sie eine Probefahrt mit Stretch Database  
 **Testen Sie Stretch Database mit der AdventureWorks-Beispieldatenbank.** Laden Sie zum Abrufen der AdventureWorks-Beispieldatenbank zumindest die Datenbankdatei und die Beispiel- und Skriptdatei [here](https://www.microsoft.com/en-us/download/details.aspx?id=49502). Nach der Wiederherstellung der Beispieldatenbank auf einer Instanz von SQL Server 2016, entpacken Sie die Beispieldateien, und öffnen Sie die Datei „Stretch DB Samples“ im Stretch DB-Ordner. Führen Sie die Skripts in dieser Datei aus, um den von den Daten genutzten Speicherplatz zu überprüfen, bevor und nachdem Sie Stretch Database aktivieren, um den Fortschritt der Datenmigration nachzuverfolgen und um zu bestätigen, dass Sie weiterhin vorhandene Daten abfragen und neue Daten während und nach der Datenmigration einfügen können.  
  
## <a name="next-step"></a>Nächster Schritt  
 **Identifizieren Sie Datenbanken und Tabellen, die für Stretch Database infrage kommen.** Herunterladen des Aktualisierungsratgebers für SQL Server 2016 und Ausführen des Ratgebers für Stretch Database, um Datenbanken und Tabellen als Kandidaten für Stretch Database zu identifizieren. Der Ratgeber für Stretch Database ermittelt auch Blockierungsprobleme. Weitere Informationen finden Sie unter [Identifizieren von Datenbanken und Tabellen für Stretch Database durch Ausführen des Ratgebers für Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md).  
  
  
