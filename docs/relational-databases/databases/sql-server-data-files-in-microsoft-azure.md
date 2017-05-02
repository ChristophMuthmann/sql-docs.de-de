---
title: SQL Server-Datendateien in Microsoft Azure | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 38ffd9c2-18a5-43d2-b674-e425addec4e4
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f04f47c6230a65140c405db039ce737ad3aa7762
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-data-files-in-microsoft-azure"></a>SQL Server-Datendateien in Microsoft Azure
  ![Datendateien in Azure](../../relational-databases/databases/media/data-files-on-azure.png "Data files on Azure")  
  
 Die SQL Server-Datendateien in Microsoft Azure ermöglichen die native Unterstützung von SQL Server-Datenbankdateien, die als Microsoft Azure-Blobs gespeichert sind. Mit der Funktion können Sie eine Datenbank in SQL Server erstellen, die lokal oder auf einem virtuellen Computer in Microsoft Azure ausgeführt wird, wobei ein dedizierter Speicherort für Ihre Daten im Microsoft Azure Blob Storage bereitgestellt wird. Diese Erweiterung vereinfacht insbesondere das Verschieben von Datenbanken zwischen Computern mithilfe von Trenn- und Anfügevorgängen. Darüber hinaus bietet sie einen alternativen Speicherort für Datenbank-Sicherungsdateien, da Wiederherstellungen im oder aus dem Microsoft Azure Storage ermöglicht werden. Mit erweiterten Funktionen für das Virtualisieren und Verschieben von Daten sowie für Sicherheit und Verfügbarkeit unterstützt sie verschiedene Hybridlösungen und bietet zusätzlich kostengünstige, einfache Verwaltungsfunktionen für hohe Verfügbarkeit und flexible Skalierung.
 
> [AZURE.IMPORTANT]Das Speichern von Systemdatenbanken in Azure BLOB-Speicher wird nicht empfohlen und nicht unterstützt. 
  
 In diesem Thema werden zentrale Konzepte und Überlegungen zur Speicherung von SQL Server-Datendateien im Microsoft Azure Storage Service eingeführt.  
  
 Ein praktisches Beispiel für die Verwendung dieser neuen Funktion finden Sie unter [Tutorial: Verwenden von Microsoft Azure Blob Storage Service der Datenbank von SQL Server 2016 ](https://msdn.microsoft.com/library/dn466438.aspx).  
  
## <a name="why-use-sql-server-data-files-in-microsoft-azure"></a>Gründe für die Verwendung von SQL Server-Datendateien in Microsoft Azure 
  
-   **Einfache und schnelle Migration:** Diese Funktion vereinfacht den Migrationsprozess, indem jeweils eine Datenbank zwischen Computern in lokalen Umgebungen sowie zwischen lokalen und Cloudumgebungen verschoben wird, ohne dass Änderungen an der Anwendung vorgenommen werden müssen. Auf diese Weise wird eine inkrementelle Migration unterstützt, während Ihre vorhandene lokale Infrastruktur unverändert beibehalten wird. Darüber hinaus vereinfacht der Zugriff auf einen zentralen Datenspeicher die Anwendungslogik, wenn eine Anwendung in einer lokalen Umgebung an mehreren Stellen ausgeführt werden muss. Es kann vorkommen, dass Sie schnell Rechenzentren an geografisch verteilten Standorten einrichten müssen, in denen Daten aus vielen verschiedenen Quellen gesammelt werden. Mit dieser neuen Erweiterung müssen Daten nicht mehr zwischen Speicherorten verschoben werden. Stattdessen können Sie zahlreiche Datenbanken als Microsoft Azure-Blobs speichern und anschließend mithilfe von Transact-SQL-Skripts Datenbanken auf den lokalen oder virtuellen Computern erstellen.  
  
-   **Kostenvorteile und unbegrenzter Speicher:** Mit dieser Funktion profitieren Sie von unbegrenztem Offsite-Speicher in Microsoft Azure, während Sie gleichzeitig die lokalen Serverressourcen nutzen. Wenn Sie Microsoft Azure als Datenspeicher verwenden, können Sie sich problemlos auf die Anwendungslogik konzentrieren, ohne sich um die aufwendige Hardwareverwaltung kümmern zu müssen. Wenn ein lokaler Serverknoten ausfällt, können Sie einen neuen Knoten einrichten, ohne Daten zu verschieben.  
  
-   **Hochverfügbarkeit und Notfallwiederherstellung:** Mithilfe von SQL Server-Datendateien in Microsoft Azure können Lösungen für hohe Verfügbarkeit und Notfallwiederherstellung u.U. vereinfacht werden. Beispiel: Wenn ein virtueller Computer in Microsoft Azure oder eine SQL Server-Instanz abstürzt, können Sie die Datenbanken auf einer neuen SQL Server-Instanz neu erstellen, indem Sie einfach wieder Verknüpfungen zu Microsoft Azure-Blobs herstellen.  
  
-   **Sicherheit:** Durch diese neue Erweiterung können Serverinstanzen von Speicherinstanzen getrennt behandelt werden. Beispielsweise können Sie über eine vollständig verschlüsselte Datenbank verfügen, deren Entschlüsselung ausschließlich auf einer Serverinstanz und nicht auf einer Speicherinstanz stattfindet. Dies bedeutet, dass Sie mit der neuen Erweiterung alle Daten in einer öffentlichen Cloud unter Verwendung von TDE-Zertifikaten (Transparent Data Encryption, transparente Datenverschlüsselung) verschlüsseln können, die physisch von den Daten getrennt sind. Die TDE-Schlüssel können in der Masterdatenbank gespeichert werden, die auf Ihrem physisch sicheren lokalen Computer gespeichert und gesichert wird. Mithilfe dieser lokalen Schlüssel können Sie die Daten verschlüsseln, die sich in Microsoft Azure Storage befinden. Falls Ihre Anmeldeinformationen für das Cloudspeicherkonto ausgespäht werden, sind die Daten trotzdem sicher, da die TDE-Zertifikate immer lokal gespeichert werden.  
  
-   **Momentaufnahmensicherung:**  Diese Funktion ermöglicht es Ihnen, Azure-Momentaufnahmen zu verwenden, um nahezu sofortige Sicherungen und schnellere Wiederherstellungen für Datenbankdateien mithilfe des Azure Blob-Storage-Diensts zu nutzen. Diese Funktion ermöglicht es Ihnen, Ihre Sicherungs- und Wiederherstellungsrichtlinien zu vereinfachen. Weitere Informationen finden Sie unter [Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
## <a name="concepts-and-requirements"></a>Konzepte und Anforderungen  
  
### <a name="azure-storage-concepts"></a>Azure-Speicherkonzepte  
 Bei Verwendung von SQL Server-Datendateien in Windows Azure müssen Sie ein Speicherkonto und einen Container in Windows Azure erstellen. Anschließend müssen Sie SQL Server-Anmeldeinformationen erstellen, die Informationen zur Containerrichtlinie sowie eine SAS (Shared Access Signature, Signatur für gemeinsamen Zugriff) enthalten, die für den Zugriff auf den Container erforderlich ist.  
  
 In [Microsoft Azure](https://azure.microsoft.com)stellt ein [Azure-Speicherkonto](https://azure.microsoft.com/services/storage/) die höchste Namespaceebene für den BLOB-Zugriff dar. Ein Speicherkonto kann eine unbegrenzte Anzahl von Containern enthalten, solange deren Gesamtgröße 500 TB nicht überschreitet. Aktuelle Informationen zu Speichergrößenbeschränkungen finden Sie unter [Azure-Abonnement und Dienstbeschränkungen, Kontingente und Einschränkungen](http://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/). Ein Container stellt eine Gruppierung eines [BLOB](https://azure.microsoft.com/documentation/articles/storage-introduction/#blob-storage)-Satzes bereit. Alle BLOBs müssen sich in einem Container befinden. Ein Konto kann eine unbegrenzte Anzahl von Containern enthalten. Analog dazu kann in einem Container auch eine unbegrenzte Anzahl von BLOBs gespeichert werden. Es gibt zwei Arten von BLOBs, die im Azure-Speicher gespeichert werden können: Blockblobs und Seitenblobs. Für die neue Funktion werden Seitenblobs von bis zu 1 TB verwendet, die effizienter sind, wenn Bytebereiche in einer Datei häufig geändert werden. Sie können mit folgendem URL-Format auf BLOBs zugreifen: `http://storageaccount.blob.core.windows.net/<container>/<blob>`.  
  
### <a name="azure-billing-considerations"></a>Überlegungen zur Abrechnung in Azure  
 Die Schätzung der für die Nutzung der Azure-Dienste anfallenden Kosten ist ein wichtiger Aspekt des Entscheidungs- und Planungsprozesses. Wenn Sie SQL Server-Datendateien im Azure-Speicher speichern, fallen Kosten für die Speicherung und Transaktionen an. Zusätzlich erfordert die Implementierung von SQL Server-Datendateien im Azure-Speicher alle 45 bis 60 Sekunden eine implizite Erneuerung der BLOB-Leasedauer. Auf diese Weise entstehen ebenfalls Transaktionskosten pro Datenbankdatei, z. B. MDF- oder LDF-Datei. Nach unserer Einschätzung würden sich die Kosten für das Erneuern der Leasedauer für zwei Datenbankdateien (MDF und LDF) gemäß dem aktuellen Preismodell auf ca. 2 US-Cent pro Monat belaufen. Die Informationen auf der [Azure-Preisseite](http://azure.microsoft.com/pricing/) sollen helfen, die monatlichen Kosten einzuschätzen, die mit der Nutzung des Azure-Speichers und der virtuellen Azure-Computer verbunden sind.  
  
### <a name="sql-server-concepts"></a>Konzepte von SQL Server  
 Die folgenden Voraussetzungen müssen zur Verwendung der neuen Erweiterung erfüllt sein:  
  
-   Sie erstellen eine Richtlinie für einen Container und generieren zusätzlich einen SAS-Schlüssel.  
  
-   Für jeden Container, der von einer Daten- oder Protokolldatei verwendet wird, erstellen Sie SQL Server-Anmeldeinformationen, deren Name mit dem Containerpfad übereinstimmt.  
  
-   Die Informationen zum Azure-Speichercontainer, der zugehörige Richtlinienname und der SAS-Schlüssel müssen im Anmeldeinformationsspeicher von SQL Server gespeichert werden.  
  
 Im folgenden Beispiel wird vorausgesetzt, dass ein Azure-Speichercontainer sowie eine Richtlinie mit Lese-, Schreib- und Auflistungsrechten erstellt wurde. Beim Erstellen einer Richtlinie für einen Container wird ein SAS-Schlüssel generiert, der gefahrlos unverschlüsselt im Arbeitsspeicher vorgehalten werden kann und von SQL Server für den Zugriff auf die BLOB-Dateien im Container benötigt wird. Ersetzen Sie in den folgenden Codeausschnitt `'your SAS key'` mit einem Eintrag, der dem folgenden ähnelt: `'sr=c&si=<MYPOLICYNAME>&sig=<THESHAREDACCESSSIGNATURE>'`. Weitere Informationen finden Sie unter [Verwalten des anonymen Lesezugriffs auf Container und Blobs](http://azure.microsoft.com/en-us/documentation/articles/storage-manage-access-to-resources/).  
  
```  
  
-- Create a credential  
CREATE CREDENTIAL [https://testdb.blob.core.windows.net/data]  
WITH IDENTITY='SHARED ACCESS SIGNATURE',  
SECRET = 'your SAS key'  
  
-- Create database with data and log files in Windows Azure container.  
CREATE DATABASE testdb   
ON  
( NAME = testdb_dat,  
    FILENAME = 'https://testdb.blob.core.windows.net/data/TestData.mdf' )  
 LOG ON  
( NAME = testdb_log,  
    FILENAME =  'https://testdb.blob.core.windows.net/data/TestLog.ldf')  
  
```  
  
 **Wichtiger Hinweis:** Wenn ein Container aktive Verweise auf Datendateien enthält, schlagen Versuche, die entsprechenden SQL Server-Anmeldeinformationen zu löschen, fehl.  
  
### <a name="security"></a>Security  
 Die folgenden Sicherheitsüberlegungen und -anforderungen sollten beim Speichern von SQL Server-Datendateien im Azure-Speicher berücksichtigt werden.  
  
-   Beim Erstellen eines Containers für den Azure-BLOB-Speicherdienst sollten Sie den Zugriff auf „Privat“ festlegen. Wenn Sie den Zugriff auf „Privat“ festlegen, können die Container- und BLOB-Daten nur vom Besitzer des Azure-Kontos gelesen werden.  
  
-   Wenn Sie SQL Server-Datenbankdateien im Azure-Speicher speichern, müssen Sie eine SAS verwenden, d. h. einen URI, der eingeschränkte Rechte für den Zugriff auf Container, BLOBs, Warteschlangen und Tabellen gewährt. Durch die Verwendung einer SAS ermöglichen Sie SQL Server unter dem Speicherkonto den Zugriff auf Ressourcen, ohne Ihren Schlüssel für das Azure-Speicherkonto offen zu legen.  
  
-   Außerdem wird empfohlen, weiterhin die herkömmlichen Sicherheitsvorkehrungen für lokale Datenbanken zu treffen.  
  
### <a name="installation-prerequisites"></a>Installationsvoraussetzungen  
 Die folgenden Installationsvoraussetzungen gelten beim Speichern von SQL Server-Datendateien in Azure.  
  
-   **SQL Server in einer lokalen Umgebung:** Dieses Feature ist in SQL Server 2016 enthalten. Informationen zum Herunterladen von SQL Server 2016 finden Sie unter [SQL Server 2016](https://www.microsoft.com/en-us/cloud-platform/sql-server).  
  
-   SQL Server auf einem virtuellen Computer in Azure: Wenn Sie [SQL Server auf einem virtuellen Azure-Computer](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)installieren, installieren Sie SQL Server 2016, oder aktualisieren Sie Ihre vorhandene Instanz. Sie können auch einen neuen virtuellen Computer in Azure erstellen, indem Sie ein Plattformimage von SQL Server 2016 verwenden.

  
###  <a name="bkmk_Limitations"></a> Einschränkungen  
  
-   In der aktuellen Version dieser Funktion wird das Speichern von **FileStream** -Daten im Azure-Speicher nicht unterstützt. Sie können **FileStream** -Daten in einer lokalen, in den Azure-Speicher integrierten Datenbank speichern. Es ist jedoch nicht möglich, Filestream-Daten unter Verwendung von Azure-Speicher zwischen Computern zu verschieben. Bei **FileStream** -Daten wird empfohlen, die herkömmlichen Verfahren zu verwenden, die bisher zum Verschieben von Dateien (MDF, LDF) in Verbindung mit Filestream-Daten zwischen verschiedenen Computern eingesetzt werden.  
  
-   Bei Verwendung der neuen Erweiterung kann derzeit nur eine SQL Server-Instanz (nicht mehrere) auf dieselben Datenbankdateien im Azure-Speicher zugreifen. Wenn ServerA mit einer aktiven Datenbankdatei online ist und ServerB versehentlich gestartet wird und auch über eine Datenbank verfügt, die auf dieselbe Datendatei verweist, kann die Datenbank des zweiten Servers nicht gestartet werden und verursacht den Fehlercode **5120 Die physische Datei „%.*ls“ kann nicht geöffnet werden\*. Betriebssystemfehler %d: „%ls“**.  
  
-   Im Azure-Speicher können ausschließlich MDF-, LDF- und NDF-Dateien mithilfe des Features „SQL Server-Datendateien in Azure“ gespeichert werden.  
  
-   Wenn Sie das Feature für SQL Server-Datendateien in Azure nutzen, wird die Georeplikation für Ihr Speicherkonto nicht unterstützt. Wenn für ein Speicherkonto eine Georeplikation ausgeführt wird und ein Geo-Failover auftritt, kann die Datenbank beschädigt werden.  
  
-   Jedes BLOB kann eine maximale Größe von 1 TB aufweisen. Auf diese Weise wird für die Datenbankdaten- und Protokolldateien, die im Azure-Speicher gespeichert werden können, eine Obergrenze festgelegt.  
  
-   Es ist nicht möglich, In-Memory OLTP-Daten mithilfe des Features „SQL Server-Datendateien in Azure“ in einem Azure-BLOB zu speichern. Das liegt daran, dass In-Memory-OLTP von **FileStream** abhängig ist und das Speichern von **FileStream** -Daten im Azure-Speicher von dem Feature in der derzeitigen Version nicht unterstützt wird.  
  
-   Bei Verwendung von SQL Server-Datendateien in Azure führt SQL Server alle URL- oder Dateipfadvergleiche mit der in der **Master** -Datenbank festgelegten Sortierung aus.  
  
-   **Always On-Verfügbarkeitsgruppen** werden unterstützt, solange der primären Datenbank keine neuen Datenbankdateien hinzugefügt werden. Wenn für einen Datenbankvorgang in der primären Datenbank eine neue Datei erstellt werden muss, deaktivieren Sie zuerst Always On-Verfügbarkeitsgruppen im sekundären Knoten. Führen Sie anschließend den Datenbankvorgang in der primären Datenbank aus, und sichern Sie die Datenbank im primären Knoten. Stellen Sie anschließend die Datenbank auf dem sekundären Knoten wieder her, und aktivieren Sie die Always On-Verfügbarkeitsgruppen im sekundären Knoten. Es sollte beachtet werden, dass Always On-Failoverclusterinstanzen bei Verwendung von SQL Server-Datendateien in Azure nicht unterstützt werden.  
  
-   Während des normalen Betriebs verwendet SQL Server temporäre Leasedauern, um BLOBs für den Speicher zu reservieren, wobei jede BLOB-Leasedauer alle 45 bis 60 Sekunden erneuert wird. Wenn ein Server abstürzt und eine andere SQL Server-Instanz gestartet wird, die für die Verwendung derselben BLOBs konfiguriert ist, wartet die neue Instanz bis zu 60 Sekunden, dass die vorhandene Leasedauer für das BLOB abläuft. Wenn Sie die Datenbank an eine andere Instanz anfügen möchten und nicht 60 Sekunden bis zum Ablauf der Leasedauer warten können, können Sie die BLOB-Leasedauer explizit unterbrechen, um Fehler in Anfügevorgängen zu vermeiden.  
  
## <a name="tools-and-programming-reference-support"></a>Unterstützung von Tools und Programmierreferenzen  
 In diesem Abschnitt werden die Tools und Referenzbibliotheken für die Programmierung beschrieben, die beim Speichern von SQL Server-Datendateien im Azure-Speicher verwendet werden können.  
  
### <a name="powershell-support"></a>PowerShell-Unterstützung  
 Verwenden Sie PowerShell-Cmdlets für die Speicherung von SQL Server-Datendateien im Azure-BLOB-Speicherdienst. Dabei wird anstatt auf einen Dateipfad auf den URL-Pfad eines BLOB-Speichers verwiesen. Greifen Sie mit folgendem URL-Format auf BLOBs zu:`: http://storageaccount.blob.core.windows.net/<container>/<blob>` .  
  
### <a name="sql-server-object-and-performance-counters-support"></a>Unterstützung von SQL Server-Objekten und -Leistungsindikatoren  
 In SQL Server 2014 wurde ein neues SQL Server-Objekt eingeführt, das mit SQL Server-Datendateien im Azure-Speicher verwendet werden kann. Das neue SQL Server-Objekt wird als [SQL Server, HTTP_STORAGE_OBJECT](../../relational-databases/performance-monitor/sql-server-http-storage-object.md) aufgerufen und kann vom Systemmonitor verwendet werden, um Aktivitäten bei der Ausführung von SQL Server mit dem Microsoft Azure-Speicher zu überwachen.  
  
### <a name="sql-server-management-studio-support"></a>Unterstützung von SQL Server Management Studio  
 SQL Server Management Studio unterstützt die Verwendung der Funktion in mehreren Dialogfeldern. Geben Sie für den URL-Pfad des Speichercontainers z. B. > https://teststorageaccnt.blob.core.windows.net/testcontainer/:
 
 als **Pfad** in verschiedenen Dialogfeldern ein, z. B. **Neue Datenbank**, **Datenbank anfügen** und **Datenbank wiederherstellen**. Weitere Informationen finden Sie unter [Tutorial: Verwenden des Microsoft Azure BLOB-Speicherdiensts mit SQL Server 2016-Datenbanken](https://msdn.microsoft.com/library/dn466438.aspx).  
  
### <a name="sql-server-management-objects-support"></a>Unterstützung von SQL Server Management Objects  
 Bei Verwendung von SQL Server-Datendateien in Azure werden alle SQL Server Management Objects (SMO) unterstützt. Wenn ein SMO-Objekt einen Dateipfad erfordert, verwenden Sie das BLOB-URL-Format anstelle eines lokalen Dateipfads, beispielsweise `https://teststorageaccnt.blob.core.windows.net/testcontainer/`. Weitere Informationen zu SQL Server Management Objects (SMO) finden Sie unter [SQL Server Management Objects &#40;SMO&#41;-Programmierungshandbuch](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md) in der SQL Server-Onlinedokumentation.  
  
### <a name="transact-sql-support"></a>Unterstützung von Transact-SQL  
 Durch die neue Funktion wurde folgende Änderung in der -Oberfläche eingeführt:  
  
-   Die neue **int** -Spalte **credential_id**in der **sys.master_files** -Systemsicht. Die **credential_id** -Spalte ermöglicht die Rückverweisung von Azure-Speicher-fähigen Datendateien auf sys.credentials, um die zugehörigen Anmeldeinformationen zu identifizieren. Sie können die Spalte zur Problembehandlung verwenden, beispielsweise, wenn Anmeldeinformationen nicht gelöscht werden können, weil sie von einer Datenbankdatei verwendet werden.  
  
##  <a name="bkmk_Troubleshooting"></a> Problembehandlung für SQL Server-Datendateien in Microsoft Azure  
 Um Fehler aufgrund von nicht unterstützten Funktionen oder Einschränkungen zu vermeiden, sollten Sie sich zunächst unter [Einschränkungen](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md#bkmk_Limitations)informieren.  
  
 In der folgenden Liste sind Fehler aufgeführt, die bei Verwendung von SQL Server-Datendateien mit dem Azure-Speicher auftreten können.  
  
 **Authentifizierungsfehler**  
  
-   *Die %.\*ls-Anmeldeinformationen können nicht gelöscht werden, weil sie von einer aktiven Datenbankdatei verwendet werden.*   
    Lösung: Dieser Fehler kann angezeigt werden, wenn Sie versuchen, Anmeldeinformationen zu löschen, die noch von einer aktiven Datenbankdatei im Azure-Speicher verwendet werden. Um die Anmeldeinformationen zu löschen, müssen Sie zuerst das zugeordnete BLOB löschen, das diese Datenbankdatei enthält. Um ein BLOB zu löschen, das über eine aktive Leasedauer verfügt, müssen Sie zunächst die Leasedauer unterbrechen.  
  
-   *Für den Container wurde nicht ordnungsgemäß eine SAS (Shared Access Signature) erstellt.*   
     Lösung: Stellen Sie sicher, dass eine SAS ordnungsgemäß für den Container erstellt wurde. Informieren Sie sich unter [Tutorial: Verwenden des Microsoft Azure BLOB-Speicherdiensts mit SQL Server 2016-Datenbanken ](https://msdn.microsoft.com/library/dn466435.aspx)über die Anweisungen aus Lektion 2.  
  
-   *SQL Server-Anmeldeinformationen wurden nicht ordnungsgemäß erstellt.*   
    Lösung: Vergewissern Sie sich, dass Sie für das Feld **Identität** „Shared Access Signature“ verwendet und ordnungsgemäß einen geheimen Schlüssel erstellt haben. Informieren Sie sich unter [Tutorial: Verwenden des Microsoft Azure BLOB-Speicherdiensts mit SQL Server 2016-Datenbanken](https://msdn.microsoft.com/library/dn466436.aspx)über die Anweisungen aus Lektion 3.  
  
 **Fehler bei BLOB-Leasedauer:**  
  
-   Fehler beim Starten von SQL Server, nachdem eine andere Instanz, die dieselben BLOB-Dateien verwendet, abgestürzt ist. Lösung: Während des normalen Betriebs verwendet SQL Server temporäre Leasedauern, um BLOBs für den Speicher zu reservieren, wobei jede BLOB-Leasedauer alle 45 bis 60 Sekunden erneuert wird. Wenn ein Server abstürzt und eine andere SQL Server-Instanz gestartet wird, die für die Verwendung derselben BLOBs konfiguriert ist, wartet die neue Instanz bis zu 60 Sekunden, dass die vorhandene Leasedauer für das BLOB abläuft. Wenn Sie die Datenbank an eine andere Instanz anfügen möchten und nicht 60 Sekunden bis zum Ablauf der Leasedauer warten können, können Sie die BLOB-Leasedauer explizit unterbrechen, um Fehler in Anfügevorgängen zu vermeiden.  
  
 **Datenbankfehler**  
  
1.  *Fehler beim Erstellen einer Datenbank*   
    Informieren Sie sich unter [Tutorial: Verwenden des Microsoft Azure BLOB-Speicherdiensts mit SQL Server 2016-Datenbanken](https://msdn.microsoft.com/library/dn466431.aspx)über die Anweisungen aus Lektion 4.  
  
2.  *Fehler beim Ausführen der ALTER-Anweisung*   
    Lösung: Stellen Sie sicher, dass die ALTER DATABASE-Anweisung ausgeführt wird, während die Datenbank online ist. Wenn Sie die Datendateien in den Azure-Speicher kopieren, erstellen Sie immer ein Seitenblob und kein Blockblob. Andernfalls erzeugt ALTER DATABASE einen Fehler. Informieren Sie sich unter [Tutorial: Verwenden des Microsoft Azure BLOB-Speicherdiensts mit SQL Server 2016-Datenbanken](https://msdn.microsoft.com/library/dn466438.aspx)über die Anweisungen aus Lektion 7.  
  
3.  *Fehlercode 5120: Die physische Datei „%.\*ls“ kann nicht geöffnet werden. Betriebssystemfehler %d: „%ls“*   
    Lösung: Bei Verwendung der neuen Erweiterung kann derzeit nur eine SQL Server-Instanz (nicht mehrere) auf dieselben Datenbankdateien im Azure-Speicher zugreifen. Wenn ServerA mit einer aktiven Datenbankdatei online ist und ServerB versehentlich gestartet wird und auch über eine Datenbank verfügt, die auf dieselbe Datendatei verweist, kann die Datenbank des zweiten Servers nicht gestartet werden und verursacht den Fehlercode *5120 Die physische Datei „%.*ls“ kann nicht geöffnet werden\*. Betriebssystemfehler %d: „%ls“*.  
  
     Um dieses Problem zu beheben, stellen Sie zuerst fest, ob „ServerA“ auf die Datenbankdatei im Azure-Speicher zugreifen muss oder nicht. Wenn nicht, entfernen Sie einfach jegliche Verbindungen zwischen „ServerA“ und den Datenbankdateien im Azure-Speicher. Führen Sie hierzu folgende Schritte aus:  
  
    1.  Legen Sie den Dateipfad von Server A mit der ALTER DATABASE-Anweisung auf einen lokalen Ordner fest.  
  
    2.  Schalten Sie die Datenbank auf Server A offline.  
  
    3.  Kopieren Sie dann die Datenbankdateien aus Azure Storage im lokalen Ordner auf Server A. Dadurch wird sichergestellt, dass „ServerA“ noch lokal eine Kopie der Datenbank hat.  
  
    4.  Schalten Sie die Datenbank online.  

  
  

