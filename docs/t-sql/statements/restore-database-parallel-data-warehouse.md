---
title: RESTORE DATABASE (Parallel Data Warehouse) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ba8aa12f38fce6ac00f88f0015008da25a59b88
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="restore-database-parallel-data-warehouse"></a>RESTORE DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Wiederherstellen einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Benutzerdatenbank von einer Datenbanksicherung auf einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Appliance. Die Datenbank wird von einer Sicherung wiederhergestellt, die zuvor mithilfe des [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Befehls [BACKUP DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md) erstellt wurde. Mit BACKUP- und RESTORE-Vorgängen können Sie einen Notfallwiederherstellungsplan erstellen oder Datenbanken von einer Appliance zur anderen verschieben.  
  
> [!NOTE]  
>  Zum Wiederherstellen der Masterdatenbank müssen die Anmeldeinformationen der Appliance wiederhergestellt werden. Verwenden Sie zum Wiederherstellen der Masterdatenbank im Tool **Configuration Manager** die Seite [Wiederherstellen der Masterdatenbank &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md). Dieser Vorgang kann von einem Administrator mit Zugriff auf den Steuerknoten ausgeführt werden.  
  
 Weitere Informationen zu [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Datenbanksicherungen finden Sie unter „Sichern und Wiederherstellen“ in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      Restore the master database  
-- Use the Configuration Manager tool.  
  
Restore a full user database backup.  
RESTORE DATABASE database_name   
    FROM DISK = '\\UNC_path\full_backup_directory'  
[;]  
  
Restore a full user database backup and then a differential backup.  
RESTORE DATABASE database_name  
    FROM DISK = '\\UNC_path\differential_backup_directory'   
    WITH [ ( ] BASE = '\\UNC_path\full_backup_directory' [ ) ]   
[;]  
  
Restore header information for a full or differential user database backup.  
RESTORE HEADERONLY   
    FROM DISK = '\\UNC_path\backup_directory'  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 RESTORE DATABASE *database_name*  
 Gibt an, dass eine Benutzerdatenbank in einer Datenbank mit dem Namen *database_name* wiederhergestellt wird. Die wiederhergestellte Datenbank kann anders benannt werden als die Quelldatenbank, die gesichert wurde. *database_name* darf nicht bereits als Datenbank auf der Zielappliance vorhanden sein. Weitere Informationen zu zulässigen Datenbanknamen finden Sie in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] unter „Objektbenennungsregeln“.  
  
 Beim Wiederherstellen einer Benutzerdatenbank wird eine vollständige Datenbanksicherung wiederhergestellt. Anschließend kann optional eine differenzielle Sicherung auf der Appliance wiederhergestellt werden. Das Wiederherstellen einer Benutzerdatenbank beinhaltet das Wiederherstellen von Datenbankbenutzern und Datenbankrollen.  
  
 FROM DISK = '\\\\*UNC_path*\\*backup_directory*'  
 Netzwerkpfad und Verzeichnis, aus denen [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] die Sicherungsdateien wiederherstellt. Ein Beispiel: FROM DISK = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup‘.  
  
 *backup_directory*  
 Gibt den Namen eines Verzeichnisses an, das die vollständige oder differenzielle Sicherung enthält. Beispielsweise kann für eine vollständige oder differenzielle Sicherung ein RESTORE HEADERONLY-Vorgang ausgeführt werden.  
  
 *full_backup_directory*  
 Gibt den Namen eines Verzeichnisses an, das die vollständige Sicherung enthält.  
  
 *differential_backup_directory*  
 Gibt den Namen eines Verzeichnisses an, das die differenzielle Sicherung enthält.  
  
-   Pfad und Sicherungsverzeichnis müssen bereits vorhanden sein und als vollqualifizierter UNC-Pfad (Universal Naming Convention) angegeben werden.  
  
-   Beim Pfad zum Sicherungsverzeichnis darf es sich nicht um einen lokalen Pfad handeln, und der Speicherort darf sich nicht auf einem [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Applianceknoten befinden.  
  
-   Die maximale Länge des UNC-Pfads und des Sicherungsverzeichnisnamens beträgt 200 Zeichen.  
  
-   Der Server oder Host muss als IP-Adresse angegeben werden.  
  
 RESTORE HEADERONLY  
 Gibt an, dass nur die Headerinformationen für die Sicherung einer Benutzerdatenbank zurückgegeben werden sollen. Der Header enthält u.a. die Textbeschreibung für die Sicherung und den Sicherungsnamen. Der Sicherungsname und der Name des Verzeichnisses, in dem die Sicherungsdateien gespeichert werden, müssen nicht identisch sein.  
  
 Die RESTORE HEADERONLY-Ergebnisse entsprechen dem Muster der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-RESTORE HEADERONLY-Ergebnisse. Das Ergebnis enthält mehr als 50 Spalten, die nicht alle von [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verwendet werden. Eine Beschreibung der Spalten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-RESTORE HEADERONLY-Ergebnisse finden Sie unter [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **CREATE ANY DATABASE**-Berechtigung.  
  
 Es ist ein Windows-Konto mit der Berechtigung erforderlich, auf das Sicherungsverzeichnis zuzugreifen und es zu lesen. Der Name des Windows-Kontos und das Kennwort müssen in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] gespeichert werden.  
  
1.  Überprüfen Sie mit [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md), ob die Anmeldeinformationen bereits vorhanden sind.  
  
2.  Verwenden Sie [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) zum Hinzufügen oder Aktualisieren der Anmeldeinformationen.  
  
3.  Mit [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) können Sie Anmeldeinformationen aus [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] entfernen.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Der RESTORE DATABASE-Befehl führt unter den folgenden Bedingungen zu einem Fehler:  
  
-   Der Name der Datenbank, die wiederhergestellt werden soll, ist auf der Zielappliance bereits vorhanden. Wählen Sie daher einen eindeutigen Datenbanknamen, oder löschen Sie die vorhandene Datenbank, bevor Sie die Wiederherstellung ausführen.  
  
-   Im Sicherungsverzeichnis befinden sich mehrere ungültige Sicherungsdateien.  
  
-   Die Anmeldeberechtigungen reichen zum Wiederherstellen einer Datenbank nicht aus.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verfügt nicht über die erforderlichen Berechtigungen für den Netzwerkspeicherort, an dem die Sicherungsdateien gespeichert sind.  
  
-   Der Netzwerkspeicherort für das Sicherungsverzeichnis ist nicht vorhanden oder nicht verfügbar.  
  
-   Es ist nicht genügend Speicherplatz auf den Computeknoten oder auf dem Steuerknoten vorhanden. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] bestätigt nicht, dass auf der Appliance genügend Speicherplatz vorhanden ist, bevor das Wiederherstellen gestartet wird. Daher kann beim Ausführen der RESTORE DATABASE-Anweisung ein Fehler wegen unzureichendem Speicherplatz generiert werden. Wenn nicht genügend Speicherplatz vorhanden ist, führt [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ein Rollback für die Wiederherstellung aus.  
  
-   Die Zielappliance, auf der die Datenbank wiederhergestellt wird, verfügt über weniger Computeknoten als die Quellappliance, von der die Datenbank gesichert wurde.  
  
-   Die Wiederherstellung der Datenbank wird aus einer Transaktion heraus ausgeführt.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verfolgt, ob die Wiederherstellung der Datenbank erfolgreich ist. Vor dem Wiederherstellen einer differenziellen Datenbanksicherung wird durch [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] überprüft, ob die vollständige Datenbankwiederherstellung erfolgreich abgeschlossen wurde.  
  
 Nach der Wiederherstellung verfügt die Benutzerdatenbank über einen Datenbank-Kompatibilitätsgrad von 120. Dies gilt für alle Datenbanken, unabhängig vom ursprünglichen Kompatibilitätsgrad.  
  
 **Wiederherstellen auf einer Appliance mit einer größeren Anzahl von Computeknoten**  
Führen Sie nach dem Wiederherstellen einer Datenbank von einer kleineren auf eine größere Appliance [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) aus, da das Transaktionsprotokoll durch die Umverteilung vergrößert wird.  

Beim Wiederherstellen einer Sicherung auf einer Appliance mit einer größeren Anzahl von Computeknoten wächst die Größe der zugeordneten Datenbank entsprechend der Anzahl der Computeknoten.  
  
Beispiel: Wenn Sie eine 60-GB-Datenbank von einer 2-Knoten-Appliance (30 GB pro Knoten) auf einer 6-Knoten-Appliance wiederherstellen, erstellt [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] auf der 6-Knoten-Appliance eine 180-GB-Datenbank (6 Knoten à 30 GB). Zunächst stellt [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] die Datenbank entsprechend der Quellkonfiguration auf 2 Knoten wieder her und verteilt sie anschließend auf alle 6 Knoten.  
  
 Nach der Umverteilung enthält jeder Computeknoten weniger tatsächliche Daten und mehr freien Speicherplatz als die einzelnen Computeknoten auf der kleineren Quellappliance. Dank des zusätzlichen Speicherplatzes können Sie der Datenbank weitere Daten hinzufügen. Ist die wiederhergestellte Datenbank größer als erforderlich, können Sie mit [ALTER DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md) die Größe der Datenbank verringern.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Für diese Einschränkungen gilt: Die Quellappliance ist die Appliance, von der aus die Sicherung der Datenbank erstellt wurde, und die Zielappliance ist die Appliance, auf der die Datenbank wiederhergestellt wird.  
  
 Beim Wiederherstellen einer Datenbank wird nicht automatisch die Statistik neu erstellt.  
  
 Auf der Appliance kann nur eine RESTORE DATABASE- oder BACKUP DATABASE-Anweisung gleichzeitig ausgeführt werden. Werden mehrere BACKUP- und RESTORE-Anweisungen gleichzeitig gesendet, werden sie in eine Warteschlange eingereiht und nacheinander verarbeitet.  
  
 Eine Datenbanksicherung kann nur auf einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Zielappliance wiederhergestellt werden, die eine gleiche oder höhere Anzahl von Computeknoten besitzt wie die Quellappliance. Die Zielappliance darf nicht über weniger Computeknoten verfügen als die Quellappliance.  
  
 Es ist nicht möglich, eine Sicherung, die auf einer Appliance mit SQL Server 2012 PDW-Hardware erstellt wurde, auf einer Appliance mit SQL Server 2008 R2-Hardware wiederherzustellen. Dies gilt auch, wenn die Appliance ursprünglich mit der SQL Server 2008 R2-PDW-Hardware gekauft wurde und mittlerweile mit SQL Server 2012 PDW-Software ausgeführt wird.  
  
## <a name="locking"></a>Sperren  
 Sperrt exklusiv das DATABASE-Objekt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-restore-examples"></a>A. Einfache Beispiele für RESTORE  
 Im folgenden Beispiel wird eine vollständige Sicherung auf einer `SalesInvoices2013`-Datenbank wiederhergestellt. Die Sicherungsdateien werden im Verzeichnis „\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full“ gespeichert. Die Datenbank „SalesInvoices2013“ darf auf der Zielappliance nicht bereits vorhanden sein. Andernfalls erzeugt dieser Befehl einen Fehler.  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. Wiederherstellen einer vollständigen und differenziellen Sicherung  
 Im folgenden Beispiel wird zunächst eine vollständige, anschließend eine differenzielle Sicherung auf der Datenbank „SalesInvoices2013“ wiederhergestellt.  
  
 Die vollständige Sicherung der Datenbank wird von der vollständigen Sicherung im Verzeichnis „\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full“ wiederhergestellt. Nach der erfolgreichen Wiederherstellung wird die differenzielle Sicherung auf der Datenbank „SalesInvoices2013“ wiederhergestellt.  Die differenzielle Sicherung wird im Verzeichnis „\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff“ gespeichert.  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. Wiederherstellen des Sicherungsheaders  
 In diesem Beispiel werden die Headerinformationen für die Datenbanksicherung „\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full“ wiederhergestellt. Der Befehl ergibt eine Zeile mit Informationen für die Sicherung von „Invoices2013Full“.  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 Sie können die Headerinformationen verwenden, um den Inhalt einer Sicherung zu überprüfen. Sie können damit auch sicherstellen, dass die Zielappliance für die Wiederherstellung mit der Quellappliance der Sicherung kompatibel ist, bevor Sie mit dem Wiederherstellen der Sicherung beginnen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BACKUP DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  
