---
title: BACKUP DATABASE (Parallel Data Warehouse) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc87423b3444daf6d44f590c283b52ce948da193
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="backup-database-parallel-data-warehouse"></a>BACKUP DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Erstellt eine Sicherungskopie einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Datenbank und speichert die Sicherung nicht auf der Appliance, sondern in einem benutzerdefinierten Netzwerkpfad. Verwenden Sie diese Anweisung mit [RESTORE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md) zur Notfallwiederherstellung oder zum Kopieren einer Datenbank von einer Appliance auf eine andere.  
  
 **Bevor Sie beginnen**, lesen Sie „Erwerb und Konfiguration eines Sicherungsservers“ in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Es gibt zwei Arten von Sicherungen in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Eine *vollständige Datenbanksicherung* ist eine Sicherung einer kompletten [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Datenbank. Bei einer *differenziellen Datenbanksicherung* werden nur die Änderungen seit der letzten vollständigen Datenbanksicherung erfasst. Die Sicherung einer Benutzerdatenbank schließt Datenbankbenutzer und Datenbankrollen ein. Eine Sicherung der Masterdatenbank schließt Anmeldungen ein.  
  
 Weitere Informationen zu [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Datenbanksicherungen finden Sie unter „Sichern und Wiederherstellen“ in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      Create a full backup of a user database or the master database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    [ WITH [ ( ]  <with_options> [ ,...n ]  [ ) ] ]  
[;]  
  
Create a differential backup of a user database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    WITH [ ( ] DIFFERENTIAL   
    [ , <with_options> [ ,...n ] [ ) ]  
[;]  
  
<with_options> ::=  
    DESCRIPTION = 'text'  
    | NAME = 'backup_name'  
  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank, auf der eine Sicherung erstellt werden soll. Die Datenbank kann die Masterdatenbank oder eine Benutzerdatenbank sein.  
  
 TO DISK = '\\\\*UNC_path*\\*backup_directory*'  
 Netzwerkpfad und Verzeichnis, in die [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] die Sicherungsdateien schreibt. Beispiel: '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup'.  
  
-   Der Pfad zum Sicherungsverzeichnisnamen muss bereits vorhanden sein und als vollqualifizierter UNC-Pfad (Universal Naming Convention) angegeben werden.  
  
-   Das Sicherungsverzeichnis *backup_directory* darf nicht vor dem Ausführen des Sicherungsbefehls vorhanden sein. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] erstellt das Sicherungsverzeichnis.  
  
-   Beim Pfad zum Sicherungsverzeichnis darf es sich nicht um einen lokalen Pfad handeln, und der Speicherort darf sich nicht auf einem [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Applianceknoten befinden.  
  
-   Die maximale Länge des UNC-Pfads und des Sicherungsverzeichnisnamens beträgt 200 Zeichen.  
  
-   Der Server oder Host muss als IP-Adresse angegeben werden.  Sie können ihn nicht als Host- oder Servernamen angeben.  
  
 DESCRIPTION = **'***text***'**  
 Gibt eine Textbeschreibung der Datensicherung an. Die maximale Länge des Texts beträgt 255 Zeichen.  
  
 Die Beschreibung wird in den Metadaten gespeichert und angezeigt, wenn der Sicherungsheader mit RESTORE HEADERONLY wiederhergestellt wird.  
  
 NAME = **'***backup _name***'**  
 Gibt den Namen der Sicherung an. Der Sicherungsname kann vom Datenbanknamen abweichen.  
  
-   Namen können maximal 128 Zeichen haben.  
  
-   Sie können keinen Pfad einschließen.  
  
-   An der ersten Stelle muss ein Buchstabe, eine Ziffer oder ein Unterstrich (_) stehen. Zulässige Sonderzeichen sind Unterstrich (\_), Bindestrich (-) oder Leerzeichen ( ). Sicherungsnamen dürfen nicht mit einem Leerzeichen enden.  
  
-   Die Anweisung schlägt fehl, wenn *backup_name* am angegebenen Speicherort bereits vorhanden ist.  
  
 Der Name wird in den Metadaten gespeichert und angezeigt, wenn der Sicherungsheader mit RESTORE HEADERONLY wiederhergestellt wird.  
  
 DIFFERENTIAL  
 Gibt an, dass eine differenzielle Sicherung einer Benutzerdatenbank durchgeführt werden soll. Wenn nicht angegeben, ist die Standardeinstellung eine vollständige Sicherung. Der Name der differenziellen Sicherung muss nicht mit dem Namen der vollständigen Sicherung übereinstimmen. Zum Nachverfolgen der differenziellen Sicherung und der zugehörigen vollständigen Sicherung sollten Sie den gleichen Namen verwenden und "full" oder "diff" anfügen.  
  
 Zum Beispiel:  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **BACKUP DATABASE**-Berechtigung oder die Mitgliedschaft in der festen Datenbankrolle **db_backupoperator**. Die Masterdatenbank kann nur von einem normalen Benutzer gesichert werden, der der festen Datenbankrolle **Db_backupoperator** hinzugefügt wurde. Die Masterdatenbank kann nur durch **sa**, den Fabricadministrator, oder Mitglieder der festen Serverrolle **Sysadmin** gesichert werden.  
  
 Erfordert ein Windows-Konto mit der Berechtigung, auf das Sicherungsverzeichnis zuzugreifen, es zu erstellen und auf es zu schreiben. Sie müssen außerdem den Windows-Kontonamen und das Kennwort in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] speichern. Zum Hinzufügen dieser Netzwerk-Anmeldeinformationen [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verwenden Sie die gespeicherte Prozedur [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
 Weitere Informationen zum Verwalten von Anmeldeinformationen in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] finden Sie im Abschnitt [Sicherheit](#Security).  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 BACKUP DATABASE-Fehler unter den folgenden Bedingungen:  
  
-   Benutzerberechtigungen sind nicht ausreichend, um eine Sicherung auszuführen.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verfügt nicht über die erforderlichen Berechtigungen für den Netzwerkspeicherort, an dem die Sicherungsdateien gespeichert werden.  
  
-   Die Datenbank ist nicht vorhanden.  
  
-   Das Zielverzeichnis ist bereits auf der Netzwerkfreigabe vorhanden.  
  
-   Die Zielnetzwerkfreigabe ist nicht verfügbar.  
  
-   Der Speicherplatz auf der Ziel-Netzwerkfreigabe ist nicht ausreichend für die Sicherung. Der BACKUP DATABASE-Befehl bestätigt nicht, dass genügend freier Speicherplatz vorhanden ist, bevor die Sicherung initiiert wird, wodurch bei Ausführen von BACKUP DATABASE ein Fehler wegen unzureichendem Speicherplatz generiert werden kann. Wenn nicht genügend Speicherplatz vorhanden ist, führt [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ein Rollback für den Befehl BACKUP DATABASE aus. Führen Sie zum Verkleinern Ihrer Datenbank [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) aus.  
  
-   Versuchen Sie, eine Sicherung innerhalb einer Transaktion zu starten.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Verwenden Sie vor dem Ausführen einer Datenbanksicherung [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) zum Verkleinern der Datenbank. 
 
 Eine [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Sicherung wird als Satz von mehreren Dateien im gleichen Verzeichnis gespeichert.  
  
 Eine differenzielle Sicherung nimmt normalerweise weniger Zeit in Anspruch als eine vollständige Sicherung und kann häufiger ausgeführt werden. Wenn mehrere differenzielle Sicherungen auf der gleichen vollständigen Sicherung basieren, enthält jede differenzielle Sicherung alle Änderungen aus der vorherigen differenziellen Sicherung.  
  
 Wenn Sie einen BACKUP-Befehl abbrechen, entfernt [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] das Zielverzeichnis und alle Dateien, die für die Sicherung erstellt wurden. Wenn [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] die Netzwerkkonnektivität mit der Freigabe verliert, kann das Rollback nicht abgeschlossen werden.  
  
 Vollständige und differenzielle Sicherungen werden in separaten Verzeichnissen gespeichert. Benennungskonventionen werden nicht erzwungen, um anzugeben, dass eine vollständige Sicherung und eine differenzielle Sicherung zusammengehören. Sie können dies über Ihre eigenen Benennungskonventionen nachverfolgen. Alternativ können Sie dies nachverfolgen, indem Sie mithilfe der WITH DESCRIPTION-Option eine Beschreibung hinzufügen und diese dann mithilfe der RESTORE HEADERONLY-Anweisung abrufen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Sie können keine differenzielle Sicherung der Masterdatenbank ausführen. Nur vollständige Sicherungen der Masterdatenbank werden unterstützt.  
  
 Die Sicherungsdateien werden in einem Format gespeichert, das nur geeignet ist, um die Sicherung auf einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Appliance unter Verwendung der [RESTORE DATABASE &#40;Parallel Data Warehouse&#41; ](../../t-sql/statements/restore-database-parallel-data-warehouse.md)-Anweisung wiederherzustellen.  
  
 Die Sicherung mit der BACKUP DATABASE-Anweisung kann nicht verwendet werden, um Daten oder Benutzerinformationen an SMP-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbanken zu übertragen. Hierfür können Sie die Remotetabellenkopie-Features verwenden. Weitere Informationen finden Sie unter „Remotetabellenkopie“ in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Technologie zum Sichern und Wiederherstellen von Datenbanken. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sicherungsoptionen sind vorkonfiguriert, um die Komprimierung von Sicherungen zu verwenden. Sie können keine Sicherungsoptionen wie Komprimierung, Prüfsumme, Blockgröße und Pufferanzahl festlegen.  
  
 Nur eine Datenbanksicherung oder -wiederherstellung kann zu einem beliebigen Zeitpunkt auf der Appliance ausgeführt werden. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] stellt Sicherungs- oder Wiederherstellungsbefehle in die Warteschlange, bis der aktuelle Sicherungs-oder Wiederherstellungsbefehl abgeschlossen ist.  
  
 Die Zielappliance für die Wiederherstellung der Sicherung muss mindestens so viele Computeknoten besitzen wie die Quellappliance. Die Zielappliance kann über mehr Computeknoten verfügen als die Quellappliance, darf aber nicht weniger Computeknoten besitzen.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verfolgt Speicherort und Namen von Sicherungen nicht, da die Sicherungen nicht auf der Appliance gespeichert werden.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verfolgt den Erfolg oder Misserfolg von Datenbanksicherungen nicht.  
  
 Eine differenzielle Sicherung ist nur zulässig, wenn die letzte vollständige Sicherung erfolgreich abgeschlossen wurde. Nehmen wir beispielsweise an, dass Sie am Montag eine vollständige Sicherung der Sales-Datenbank erstellen und die Sicherung erfolgreich abgeschlossen wird. Am Dienstag erstellen Sie dann eine vollständige Sicherung der Sales-Datenbank, die fehlschlägt. Nach diesem Fehler können Sie dann keine auf der vollständigen Sicherung vom Montag basierende differenzielle Sicherung erstellen. Sie müssen eine vollständige Sicherung erstellen, bevor Sie eine differenzielle Sicherung erstellen.  
  
## <a name="metadata"></a>Metadaten  
 Diese dynamischen Verwaltungssichten enthalten Informationen über alle Sicherungs-, Wiederherstellungs- und Ladevorgänge. Die Informationen persistieren über Systemneustarts.  
  
-   [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>Leistung  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] führt eine Sicherung aus, indem zuerst die Metadaten gesichert werden und dann eine parallele Sicherung der auf den Computeknoten gespeicherten Datenbankdaten ausgeführt wird. Daten werden direkt aus jedem Computeknoten in das Sicherungsverzeichnis kopiert. Um die bestmögliche Leistung für das Verschieben von Daten von den Computeknoten in das Sicherungsverzeichnis zu erzielen, steuert [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] die Anzahl von Computeknoten, die gleichzeitig Daten kopieren.  
  
## <a name="locking"></a>Sperren  
 Das DATABASE-Objekt wird mit einer ExclusiveUpdate-Sperre gesperrt.  
  
##  <a name="Security"></a> Sicherheit  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Sicherungen werden nicht auf dem Gerät gespeichert. Daher ist Ihr IT-Team zuständig für das Verwalten aller Aspekte der Sicherheit von Sicherungen. Dazu gehört beispielsweise die Verwaltung der Sicherheit der Sicherungsdaten, der Sicherheit der Server, auf denen Sicherungen gespeichert werden, und der Sicherheit der Netzwerkinfrastruktur, die die Sicherungsserver mit der [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Appliance verbinden.  
  
 **Verwalten von Anmeldeinformationen für das Netzwerk**  
  
 Der Netzwerkzugriff auf das Sicherungsverzeichnis basiert auf der Windows-Standarddateifreigabesicherheit. Vor dem Ausführen einer Sicherung müssen Sie ein Windows-Konto erstellen oder reservieren, das für die Authentifizierung von [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] beim Sicherungsverzeichnis verwendet wird. Dieses Windows-Konto benötigt die Berechtigung, auf das Sicherungsverzeichnis zuzugreifen, es zu erstellen und auf es zu schreiben.  
  
> [!IMPORTANT]  
>  Um Sicherheitsrisiken in Verbindung mit Ihren Daten zu reduzieren, empfehlen wir, dass Sie ein Windows-Konto ausschließlich zum Ausführen der Sicherungs- und Wiederherstellungsvorgänge festlegen. Definieren Sie das Konto so, dass es nur Berechtigungen für den Sicherungsspeicherort besitzt.  
  
 Sie müssen den Benutzernamen und das Kennwort in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] speichern, indem Sie die gespeicherte Prozedur [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) ausführen. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verwendet die Windows-Anmeldeinformationsverwaltung zum Speichern und Verschlüsseln von Benutzernamen und Kennwörtern auf dem Steuerknoten und den Computeknoten. Die Anmeldeinformationen werden nicht mit dem Befehl BACKUP DATABASE gesichert.  
  
 Mit [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) können Sie Netzwerkanmeldeinformationen aus [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] entfernen.  
  
 Um alle in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] gespeicherten Netzwerkanmeldeinformationen aufzulisten, verwenden Sie die dynamische Verwaltungssicht [sys.dm_pdw_network_credentials &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. Fügen Sie der Netzwerkanmeldeinformationen für den Sicherungsspeicherort hinzu  
 Zum Erstellen einer Sicherung [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] benötigen Sie die Lese-/Schreibberechtigung für das Sicherungsverzeichnis. Im folgenden Beispiel wird gezeigt, wie die Anmeldeinformationen für einen Benutzer hinzugefügt werden. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] speichert die Anmeldeinformationen und verwendet sie für Sicherungs- und Wiederherstellungsvorgänge.  
  
> [!IMPORTANT]  
>  Aus Sicherheitsgründen wird empfohlen, mindestens ein Domänenkonto ausschließlich zum Zweck der Durchführung von Sicherungen zu erstellen.  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. Entfernen Sie Netzwerkanmeldeinformationen für den Sicherungsspeicherort  
 Im folgenden Beispiel wird gezeigt, wie die Anmeldeinformationen für ein Domänenbenutzerkonto aus [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] entfernt werden.  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. Erstellen Sie eine vollständige Sicherung jeder Benutzerdatenbank  
 Im folgenden Beispiel wird eine vollständige Sicherung der Invoices-Benutzerdatenbank erstellt. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] erstellt das Verzeichnis Invoices2013 und speichert die Sicherungsdateien im Verzeichnis \\\10.192.63.147\backups\yearly\Invoices2013Full.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. Erstellen Sie eine differenzielle Sicherung einer Benutzerdatenbank  
 Das folgende Beispiel erstellt eine differenzielle Sicherung, die alle Änderungen seit der letzten vollständigen Sicherung der Invoices-Datenbank enthält. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] erstellt das Verzeichnis \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff, in dem die Dateien gespeichert werden. Die Beschreibung "Invoices 2013 differential backup" wird mit den Headerinformationen für die Sicherung gespeichert.  
  
 Die differenzielle Sicherung wird nur dann erfolgreich ausgeführt, wenn die letzte vollständige Sicherung von Rechnungen erfolgreich abgeschlossen wurde.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. Erstellen Sie eine vollständige Sicherung der Masterdatenbank  
 Im folgenden Beispiel wird eine vollständige Sicherung der Masterdatenbank erstellt und im Verzeichnis \\\10.192.63.147\backups\2013\daily\20130722\master gespeichert.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. Erstellen Sie eine Sicherung der Appliance-Anmeldeinformationen.  
 Die Masterdatenbank speichert die Anmeldeinformationen für die Appliance. Um die Anmeldeinformationen für die Appliance zu sichern, müssen Sie die Masterdatenbank sichern.  
  
 Im folgenden Beispiel wird eine vollständige Sicherung der Masterdatenbank erstellt.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RESTORE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  
