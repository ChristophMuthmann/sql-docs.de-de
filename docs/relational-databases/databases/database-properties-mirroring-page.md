---
title: Datenbankeigenschaften (Seite Wird gespiegelt) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.databaseproperties.mirroring.f1
ms.assetid: 5bdcd20f-532d-4ee6-b2c7-18dbb7584a87
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1dece952a9aba10ef1dff5fe92d7747ae11f711
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="database-properties-mirroring-page"></a>Datenbankeigenschaften (Seite Wird gespiegelt)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Greifen Sie von der Prinzipaldatenbank aus auf diese Seite zu, und verwenden Sie sie zum Konfigurieren und Ändern der Eigenschaften der Datenbankspiegelung für eine Datenbank. Verwenden Sie die Seite auch, um den Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung zu starten, um den Status einer Spiegelungssitzung anzuzeigen und um die Datenbank-Spiegelungssitzung anzuhalten oder zu entfernen.  
  
> **WICHTIG!** Die Sicherheit muss konfiguriert werden, bevor die Spiegelung gestartet werden kann. Wenn die Spiegelung noch nicht gestartet wurde, müssen Sie zunächst den Assistenten verwenden. Die Textfelder der Seite **Spiegelung** sind deaktiviert, bis der Assistent abgeschlossen wurde.  
  
 **Konfigurieren der Datenbankspiegelung mithilfe von SQL Server Management Studio**  
  
-   [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="options"></a>Tastatur  
 **Sicherheit konfigurieren**  
 Klicken Sie auf diese Schaltfläche, um den **Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung**zu starten.  
  
 Wenn der Assistent erfolgreich beendet wird, hängt die durchzuführende Aktion auf folgende Weise davon ab, ob die Spiegelung bereits begonnen wurde:  
  
|||  
|-|-|  
|Wenn die Spiegelung nicht begonnen wurde.|Diese Verbindungsinformationen werden in der Eigenschaftenseite zwischengespeichert sowie zusätzlich ein Wert, der anzeigt, ob die Spiegeldatenbank über den entsprechenden Satz von Eigenschaften verfügt.<br /><br /> Bei Abschluss des Assistenten werden Sie aufgefordert, die Datenbankspiegelung mit den standardmäßigen Server-Netzwerkadressen und dem standardmäßigen Betriebsmodus zu starten. Wenn Sie die Adressen oder den Betriebsmodus ändern müssen, klicken Sie auf **Spiegelung nicht starten**.|  
|Wenn die Spiegelung begonnen wurde.|Wenn der Zeugenserver im Assistenten geändert wurde, wird diese Einstellung entsprechend festgelegt.|  
  
 **Server-Netzwerkadressen**  
 Eine entsprechende Option ist für jede Serverinstanz vorhanden: **Prinzipal**, **Spiegel**und **Zeuge**.  
  
 Die Server-Netzwerkadressen der Serverinstanzen werden automatisch angegeben, wenn Sie den Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung abschließen. Nach Abschluss des Assistenten können Sie die Netzwerkadressen bei Bedarf manuell ändern.  
  
 Für die Server-Netzwerkadresse gilt folgende grundlegende Syntax:  
  
 TCP**://***volqualifizierter_Domänenname***:***Port*  
  
 Dabei gilt:  
  
-   *fully_qualified_domain_name* ist der Server, auf dem die Serverinstanz vorhanden ist.  
  
-   *port* ist der Port, der dem Endpunkt der Serverinstanz für die Datenbankspiegelung zugewiesen ist.  
  
     Um an einer Datenbankspiegelung teilnehmen zu können, ist für einen Server ein Datenbankspiegelungs-Endpunkt erforderlich. Wenn Sie den Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung verwenden, um die erste Spiegelungssitzung für eine Serverinstanz einzurichten, wird dieser Endpunkt automatisch vom Assistenten erstellt und für die Verwendung der Windows-Authentifizierung konfiguriert. Informationen zum Verwenden des Assistenten mit zertifikatbasierter Authentifizierung finden Sie unter [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md).  
  
    >**WICHTIG!**  Jede Serverinstanz erfordert genau einen Datenbankspiegelungs-Endpunkt, unabhängig von der Anzahl der zu unterstützenden Spiegelungssitzungen.  
  
 Für eine Serverinstanz auf einem Computersystem namens `DBSERVER9` , dessen Endpunkt den Port `7022`verwendet, ist beispielsweise die folgende Netzwerkadresse möglich:  
  
```  
TCP://DBSERVER9.COMPANYINFO.ADVENTURE-WORKS.COM:7022  
```  
  
 Weitere Informationen finden Sie unter [Angeben einer Servernetzwerkadresse &#40;Datenbankspiegelung&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)verwendet.  
  
> **HINWEIS:** Während einer Datenbank-Spiegelungssitzung können die Prinzipal- und die Spiegelserverinstanzen nicht geändert werden. Die Zeugenserverinstanz kann jedoch auch während einer Sitzung geändert werden. Weitere Informationen finden Sie unter "Hinweise" weiter unten in diesem Thema.  
  
 **Spiegeln starten**  
 Klicken Sie zum Starten der Spiegelung auf diese Schaltfläche, wenn alle der folgenden Bedingungen erfüllt sind:  
  
-   Die Spiegeldatenbank muss vorhanden sein.  
  
     Bevor Sie die Spiegelung starten können, muss die Spiegeldatenbank durch eine aktuelle vollständige Sicherung mit der Option WITH NORECOVERY und ggf. durch Protokollsicherungen der Prinzipaldatenbank auf dem Spiegelserver erstellt worden sein. Weitere Informationen finden Sie unter [Vorbereiten einer Spiegeldatenbank auf die Spiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)verwendet.  
  
-   Die TCP-Adressen der Prinzipal- und Spiegelserverinstanzen sind festgelegt (im Bereich **Server-Netzwerkadressen**).  
  
-   Wenn als Betriebsmodus hohe Sicherheit mit automatischem Failover (synchron) festgelegt ist, ist die TCP-Adresse der Spiegelserverinstanz ebenfalls festgelegt.  
  
-   Die Sicherheit wurde ordnungsgemäß konfiguriert.  
  
 Klicken Sie auf **Spiegeln starten** , um die Sitzung einzuleiten. Vom Datenbankmodul wird versucht, eine automatische Verbindung mit dem Spiegelungspartner herzustellen, um zu überprüfen, ob der Spiegelserver ordnungsgemäß konfiguriert ist, und um die Spiegelungssitzung zu beginnen. Wenn die Spiegelung gestartet werden kann, wird ein Auftrag zum Überwachen der Datenbank erstellt.  
  
 **Anhalten** oder **Fortsetzen**  
 Klicken Sie während einer Datenbank-Spiegelungssitzung auf **Anhalten** , um die Sitzung anzuhalten. Wenn Sie in der Bestätigungsaufforderung auf **Ja**klicken, wird die Sitzung angehalten und die Schaltfläche erhält die Bezeichnung **Fortsetzen**. Klicken Sie zum Fortsetzen der Sitzung auf **Fortsetzen**.  
  
 Informationen über die Auswirkung des Anhaltens einer Sitzung finden Sie unter [Anhalten und Fortsetzen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md).  
  
> **WICHTIG!** Wenn der ursprüngliche Prinzipalserver nach einem erzwungenen Dienst erneut eine Verbindung herstellt, wird die Spiegelung angehalten. Das Fortsetzen der Spiegelung in dieser Situation könnte auf dem ursprünglichen Prinzipalserver zu Datenverlust führen. Informationen zum Verwalten des potenziellen Datenverlusts finden Sie unter [Rollenwechsel während einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).  
  
 **Spiegeln entfernen**  
 Klicken Sie auf der Prinzipalserverinstanz auf diese Schaltfläche, um die Sitzung zu beenden und die Spiegelungskonfiguration aus den Datenbanken zu entfernen. Sie werden zur Bestätigung aufgefordert. Wenn Sie auf **Ja**klicken, wird die Sitzung beendet und das Spiegeln entfernt. Informationen zu den Auswirkungen des Entfernens der Datenbankspiegelung finden Sie unter [Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
> **HINWEIS:** Falls es sich um die einzige gespiegelte Datenbank auf der Serverinstanz handelt, wird der Überwachungsauftrag entfernt.  
  
 **Failover**  
 Klicken Sie hier, um manuell ein Failover der Prinzipaldatenbank zur Spiegeldatenbank ausführen.  
  
> **HINWEIS:** Wenn die Spiegelungssitzung im Modus für hohe Leistung ausgeführt wird, wird das manuelle Failover nicht unterstützt. Zum Ausführen eines manuellen Failovers müssen Sie zuerst den Betriebsmodus in **Hohe Sicherheit ohne automatisches Failover (synchron)**ändern. Nach Abschluss des Failovers können Sie den Modus auf der neuen Prinzipalserverinstanz wieder in **Hohe Leistung (asynchron)** ändern.  
  
 Es wird eine Bestätigungsaufforderung angezeigt. Wenn Sie auf **Ja**klicken, wird versucht, ein Failover auszuführen. Der Prinzipalserver versucht als erstes, mithilfe der Windows-Authentifizierung eine Verbindung mit dem Spiegelserver herzustellen. Wenn die Windows-Authentifizierung nicht funktioniert, zeigt der Prinzipalserver das Dialogfeld **Verbindung mit Server herstellen** an. Wenn der Spiegelserver die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwendet, wählen Sie im Feld **Authentifizierung** die Option **SQL Server-Authentifizierung** aus. Geben Sie im Textfeld **Anmeldename** das Anmeldekonto an, mit dem auf dem Spiegelserver eine Verbindung hergestellt werden soll, und geben Sie im Textfeld **Kennwort** das Kennwort für dieses Konto an.  
  
 Nach erfolgreicher Ausführung des Failovers, wird das Dialogfeld **Datenbankeigenschaften** geschlossen. Die Prinzipal- und Spiegelserverrollen werden gewechselt: die ehemalige Spiegeldatenbank wird zur Prinzipaldatenbank und umgekehrt. Beachten Sie, dass das Dialogfeld **Datenbankeigenschaften** für die bisherige Prinzipaldatenbank sofort nicht mehr verfügbar ist, weil diese zur Spiegeldatenbank wird. Nach dem Failover wird dieses Dialogfeld für die neue Prinzipaldatenbank verfügbar.  
  
 Wenn während des Failovers ein Fehler auftritt, wird eine Fehlermeldung angezeigt, und das Dialogfeld bleibt geöffnet.  
  
> **WICHTIG!** Wenn Sie auf **Failover** klicken, nachdem Sie Eigenschaften im Dialogfeld **Datenbankeigenschaften** geändert haben, gehen diese Änderungen verloren. Um aktuelle Änderungen zu speichern, klicken Sie in der Bestätigungsaufforderung auf **Nein** , und klicken Sie auf **OK** , um die Änderungen zu speichern. Öffnen Sie danach das Dialogfeld für die Datenbankeigenschaften, und klicken Sie auf **Failover**.  
  
 **Betriebsmodus**  
 Sie können optional den Betriebsmodus ändern. Die Verfügbarkeit verschiedener Betriebsmodi hängt davon ab, ob Sie eine TCP-Adresse für einen Zeugen angegeben haben. Folgende Optionen stehen zur Verfügung:  
  
|Option|Zeuge?|Erklärung|  
|------------|--------------|-----------------|  
|**Hohe Leistung (asynchron)**|NULL (falls vorhanden, wird er nicht verwendet, die Sitzung benötigt jedoch ein Quorum)|Um die Leistung zu steigern, befindet sich die Spiegeldatenbank immer in einem gewissen zeitlichen Abstand zur Prinzipaldatenbank und niemals auf dem tatsächlich aktuellen Stand. Die Lücke zwischen den beiden Datenbanken ist üblicherweise aber sehr klein. Der Verlust eines Partners hat folgenden Effekt:<br /><br /> Wenn die Spiegelserverinstanz ausfällt, bleibt die Prinzipalinstanz in Betrieb.<br /><br /> Wenn die Prinzipalserverinstanz nicht mehr zur Verfügung steht, wird der Spiegel beendet. Wenn die Sitzung jedoch keinen Zeugen hat (wie empfohlen) oder der Zeuge mit dem Spiegelserver verbunden ist, ist der Zugriff auf den Spiegelserver als betriebsbereiter Standbyserver weiterhin möglich. Der Datenbankbesitzer kann die Spiegelserverinstanz zur Übernahme des Diensts zwingen, wobei es möglicherweise zu Datenverlusten kommt.|  
|**Hohe Sicherheit ohne automatisches Failover (synchron)**|nein|Für alle Transaktionen, für die ein Commit ausgeführt wird, wird sichergestellt, dass sie auf den Datenträger auf dem Spiegelserver geschrieben werden.<br /><br /> Manuelles Failover ist möglich, wenn die Partner miteinander verbunden sind.<br /><br /> Der Verlust eines Partners hat folgenden Effekt:<br /><br /> Wenn die Spiegelserverinstanz ausfällt, bleibt die Prinzipalinstanz in Betrieb.<br /><br /> Wenn die Prinzipalserverinstanz nicht mehr zur Verfügung steht, wird der Spiegel beendet, ist aber als betriebsbereiter Server verfügbar. Der Datenbankbesitzer kann die Spiegelserverinstanz zur Übernahme des Diensts zwingen, wobei es möglicherweise zu Datenverlusten kommt.|  
|**Hohe Sicherheit mit automatischem Failover (synchron)**|Ja (erforderlich)|Bietet höchste Verfügbarkeit durch Einbindung einer Zeugenserverinstanz zur Unterstützung eines automatischen Failovers. Beachten Sie, dass die Auswahl der Option **Synchron mit automatischem Failover (hohe Verfügbarkeit)** nur möglich ist, wenn Sie zuvor eine Zeugenserveradresse angegeben haben.<br /><br /> Manuelles Failover ist immer möglich, wenn die Partner miteinander verbunden sind.<br /><br /> **\*\* Wichtig \*\*** Wenn der Zeuge getrennt wird, müssen die Partner miteinander verbunden sein, damit die Datenbank verfügbar ist. Weitere Informationen finden Sie unter [Quorum: Auswirkungen eines Zeugen auf die Datenbankverfügbarkeit &#40;Datenbankspiegelung&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).<br /><br /> In den Modi für den synchronen Betrieb wird sichergestellt, dass alle Transaktionen, für die ein Commit ausgeführt wurde, auf den Datenträger des Spiegelservers geschrieben werden. In Anwesenheit eines Zeugen hat der Verlust eines Partners die folgende Auswirkung:<br /><br /> Wenn der Prinzipalserver ausfällt, findet ein automatisches Failover statt. Die Spiegelserverinstanz übernimmt die Rolle des Prinzipals und stellt ihre Datenbank als Prinzipaldatenbank zur Verfügung.<br /><br /> Wenn die Spiegelserverinstanz ausfällt, bleibt die Prinzipalinstanz in Betrieb.<br /><br /> <br /><br /> Weitere Informationen finden Sie unter [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).|  
  
 Nach dem Beginn der Spiegelung können Sie den Betriebsmodus ändern und die Änderung speichern, indem Sie auf **OK**klicken.  
  
 Weitere Informationen zu den Betriebsmodi finden Sie unter [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 **Status**  
 Nach dem Beginn der Spiegelung wird im Bereich **Status** der Status der Spiegelungssitzung angezeigt, sobald Sie die Seite **Spiegelung** auswählen. Um den Bereich **Status** zu aktualisieren, klicken Sie auf die Schaltfläche **Aktualisieren** . Folgende Werte sind für den Status möglich:  
  
|Status|Erklärung|  
|------------|-----------------|  
|**Diese Datenbank wurde nicht für das Spiegeln konfiguriert**|Es ist keine Datenbank-Spiegelungssitzung vorhanden und keine Aktivität auf der Seite **Spiegelung** anzuzeigen.|  
|**Angehalten**|Die Prinzipaldatenbank ist verfügbar, sendet aber keine Protokolle an den Spiegelserver.|  
|**Keine Verbindung**|Die Prinzipalserverinstanz kann keine Verbindung mit ihrem Partner herstellen.|  
|**Wird synchronisiert**|Der Inhalt der Spiegeldatenbank hält mit dem Inhalt der Prinzipaldatenbank nicht Schritt. Die Prinzipalserverinstanz sendet Protokolldatensätze an die Spiegelserverinstanz, die die Änderungen auf die Spiegeldatenbank anwendet, um ein Rollforward dafür auszuführen.<br /><br /> Beim Start einer Datenbank-Spiegelungssitzung befinden sich Spiegel- und Prinzipaldatenbank in diesem Status.|  
|**Failover**|Auf der Prinzipalserverinstanz hat ein manuelles Failover (Rollenwechsel) begonnen, und der Server geht gerade in die Spiegelrolle über. In diesem Status werden Benutzerverbindungen mit der Prinzipaldatenbank schnell beendet, und die Datenbank übernimmt kurze Zeit später die Spiegelrolle.|  
|**Synchronisiert**|Wenn der Spiegelserver den Stand des Prinzipalservers erreicht hat, wechselt der Datenbankstatus zu **Synchronisiert**. Die Datenbank behält diesen Status so lange bei, wie der Prinzipalserver Änderungen an den Spiegelserver sendet und der Spiegelserver Änderungen auf die Spiegeldatenbank anwendet.<br /><br /> Im Modus für hohe Sicherheit ist das Failover ohne Datenverlust möglich.<br /><br /> Im Modus für hohe Leistung ist immer ein gewisser Datenverlust möglich, sogar im Status **Synchronisiert**.|  
  
 Weitere Informationen finden Sie unter [Spiegelungsstatus &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md).  
  
 **Aktualisieren**  
 Klicken Sie auf diese Schaltfläche, um das Feld **Status** zu aktualisieren.  
  
## <a name="remarks"></a>Remarks  
 Wenn Sie sich mit Datenbankspiegelung nicht auskennen, finden Sie Informationen unter [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
### <a name="adding-a-witness-to-an-existing-session"></a>Hinzufügen eines Zeugen zu einer vorhandenen Sitzung  
 Sie können einer vorhandenen Sitzung einen Zeugen hinzufügen oder einen vorhandenen Zeugen ersetzen. Wenn Sie die Server-Netzwerkadresse des Zeugen kennen, können Sie sie manuell in das Feld **Zeuge** eingeben. Wenn Sie die Server-Netzwerkadresse des Zeugen nicht kennen, verwenden Sie den Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung zum Konfigurieren des Zeugen. Nachdem sich die Adresse im Feld befindet, stellen Sie sicher, dass die Option **Hohe Sicherheit mit automatischem Failover (synchron)** ausgewählt ist.  
  
 Nach dem Konfigurieren eines neuen Zeugen müssen Sie auf **OK** klicken, um der Spiegelungssitzung diesen neuen Zeugen hinzuzufügen.  
  
 **So fügen Sie bei der Verwendung der Windows-Authentifizierung einen Zeugen hinzu**  
  
 [Hinzufügen oder Ersetzen eines Datenbank-Spiegelungszeugen &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
### <a name="removing-a-witness"></a>Entfernen eines Zeugen  
 Löschen Sie die Server-Netzwerkadresse aus dem Feld **Zeuge** , um einen Zeugen zu entfernen. Wenn Sie vom Modus für hohe Sicherheit mit automatischem Failover zum Modus zur hohe Leistung wechseln, wird das Feld **Zeuge** automatisch gelöscht.  
  
 Nach dem Löschen des Zeugen müssen Sie auf **Ok** klicken, um ihn aus der Spiegelungssitzung zu entfernen.  
  
### <a name="monitoring-database-mirroring"></a>Überwachen der Datenbankspiegelung  
 Zum Überwachen der gespiegelten Datenbanken auf einer Serverinstanz können Sie entweder den Datenbankspiegelungs-Monitor oder die gespeicherte Systemprozedur „sp_dbmmonitorresults“ verwenden.  
  
 **So überwachen Sie gespiegelte Datenbanken**  
  
-   [Starten des Datenbankspiegelungs-Monitors &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
 Weitere Informationen finden Sie unter [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Angeben einer Servernetzwerkadresse &#40;Datenbankspiegelung&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Starten des Datenbankspiegelungs-Monitors &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Transportsicherheit für Datenbankspiegelung und AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Rollenwechsel während einer Datenbank-Spiegelungssitzung &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Anhalten und Fortsetzen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [Entfernen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [Datenbank-Spiegelungszeuge](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
