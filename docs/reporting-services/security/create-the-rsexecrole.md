---
title: Erstellen der Rolle RSExecRole | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RSExecRole
ms.assetid: 7ac17341-df7e-4401-870e-652caa2859c0
caps.latest.revision: 23
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c5830b59420268d58f6425f8a2ce52fc4a3be12e
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---

# <a name="create-the-rsexecrole"></a>Erstellen der Rolle RSExecRole

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet eine vordefinierte Datenbankrolle namens **RSExecRole** , um Berichtsserverberechtigungen für die Berichtsserver-Datenbank zu gewähren. Die Rolle **RSExecRole** wird automatisch mit der Berichtsserver-Datenbank erstellt. Als Faustregel gilt, dass Sie sie nie ändern und ihr keine anderen Benutzer zuweisen sollten. Wenn Sie die Berichtsserver-Datenbank jedoch auf ein neues oder anderes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]verlagern, müssen Sie die Rolle in den Systemdatenbanken Master und MSDB neu erstellen.  
  
 Mithilfe der folgenden Anweisungen führen Sie die folgenden Schritte aus:  
  
-   Erstellen Sie die Rolle **RSExecRole** , und stellen Sie sie in der Systemdatenbank Master bereit.  
  
-   Erstellen Sie die Rolle **RSExecRole** , und stellen Sie sie in der Systemdatenbank MSDB bereit.  
  
> [!NOTE]  
>  Die Anweisungen in diesem Thema sind für Benutzer vorgesehen, die zur Bereitstellung der Berichtsserver-Datenbank kein Skript ausführen oder WMI-Code schreiben möchten. Wenn Sie eine umfangreiche Bereitstellung verwalten und regelmäßig Datenbanken verschieben, sollten Sie ein Skript zur Automatisierung dieser Schritte schreiben. Weitere Informationen finden Sie unter [Zugreifen auf den Reporting Services-WMI-Anbieter](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  
## <a name="before-you-start"></a>Vorbereitungen  
  
-   Sichern Sie die Verschlüsselungsschlüssel, damit Sie sie wiederherstellen können, nachdem die Datenbank verschoben wurde. Dieser Schritt wirkt sich nicht direkt auf die Erstellung oder Bereitstellung der Rolle **RSExecRole**aus. Sie müssen jedoch über eine Sicherung der Schlüssel verfügen, um die durchgeführten Schritte verifizieren zu können. Weitere Informationen finden Sie unter [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
-   Überzeugen Sie sich davon, dass Sie unter einem Benutzerkonto angemeldet sind, das über **sysadmin** -Berechtigungen für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verfügt.  
  
-   Überprüfen Sie, ob der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst installiert wurde und auf der Instanz der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz ausgeführt wird, die Sie verwenden möchten.  
  
-   Fügen Sie die Datenbanken reportservertempdb und reportserver an. Zum Erstellen der Rolle ist das Anfügen der Datenbanken nicht erforderlich. Die Datenbanken müssen jedoch angefügt werden, damit Sie Ihre Implementierung testen können.  
  
 Die Anweisungen zum manuellen Erstellen der Rolle **RSExecRole** sollen im Kontext einer Migration der Berichtsserver-Installation verwendet werden. In diesem Thema wird auf wichtige Aufgaben, wie z. B. das Sichern und Verschieben der Berichtsserver-Datenbank, nicht eingegangen. Diese Aufgaben werden aber in der Dokumentation zum Datenbankmodul beschrieben.  
  
## <a name="create-rsexecrole-in-master"></a>Erstellen der Rolle 'RSExecRole' in 'Master'  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wird durch den Einsatz von erweiterten gespeicherten Prozeduren sichergestellt, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst geplante Vorgänge unterstützt. Die folgenden Schritte erklären, wie der Rolle **RSExecRole** Berechtigungen zum Ausführen der Prozeduren gewährt werden.  
  
#### <a name="to-create-rsexecrole-in-the-master-system-database-using-management-studio"></a>So erstellen Sie die Rolle 'RSExecRole' mit Management Studio in der Systemdatenbank 'Master'  
  
1.  Starten Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , und stellen Sie eine Verbindung mit der [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz her, die als Host für die Berichtsserver-Datenbank fungiert.  
  
2.  Öffnen Sie **Datenbanken**  
  
3.  Öffnen Sie **Systemdatenbanken**.  
  
4.  Öffnen Sie **Master**.  
  
5.  Öffnen Sie **Sicherheit**.  
  
6.  Öffnen Sie **Rollen**.  
  
7.  Klicken Sie mit der rechten Maustaste auf **Datenbankrollen**, und wählen Sie **Neue Datenbankrolle**aus. Die Seite Allgemein wird angezeigt.  
  
8.  Geben Sie im Feld **Rollennamen**den Namen **RSExecRole**ein.  
  
9. Geben Sie im Feld **Besitzer**die Zeichenfolge **DBO**ein.  
  
10. Klicken Sie auf **Sicherungsfähige Elemente**.  
  
11. Klicken Sie auf **Suchen**. Das Dialogfeld **Objekte hinzufügen** wird angezeigt. Standardmäßig ist die Option **Bestimmte Objekte** aktiviert.  
  
12. Klicken Sie auf **OK**. Das Dialogfeld **Objekte auswählen** wird angezeigt.  
  
13. Klicken Sie auf **Objekttypen**.  
  
14. Klicken Sie auf **Erweiterte gespeicherte Prozeduren**.  
  
15. Klicken Sie auf **OK**.  
  
16. Klicken Sie auf **Durchsuchen**.  
  
17. Führen Sie in der Liste erweiterter gespeicherter Prozeduren einen Bildlauf durch, und wählen Sie Folgendes aus:  
  
    1.  xp_sqlagent_enum_jobs  
  
    2.  xp_sqlagent_is_starting  
  
    3.  xp_sqlagent_notify  
  
18. Klicken Sie auf **OK**, und klicken Sie dann nochmals auf **OK** .  
  
19. Klicken Sie in der Zeile **Ausführen** auf das Kontrollkästchen in der Spalte **Erteilen** und dann auf **OK**.  
  
20. Wiederholen Sie diesen Schritt für alle übrigen gespeicherten Prozeduren. Der Rolle**RSExecRole** müssen Berechtigungen zum Ausführen aller drei gespeicherten Prozeduren gewährt werden.  
  
 ![Rolleneigenschaften Datenbankseite](../../reporting-services/security/media/rsexecroledbproperties.gif "Seite "Eigenschaften der Datenbankrolle"")  
  
## <a name="create-rsexecrole-in-msdb"></a>Erstellen der Rolle 'RSExecRole' in 'MSDB'  
 Reporting Services verwendet gespeicherte Prozeduren für den SQL Server-Agent-Dienst und ruft zur Unterstützung geplanter Vorgänge Auftragsinformationen ab. Die folgenden Schritte erklären, wie der Rolle RSExecRole Berechtigungen zum Ausführen der Prozeduren und zum Auswählen der Tabellen gewährt werden.  
  
#### <a name="to-create-rsexecrole-in-the-msdb-system-database"></a>So erstellen Sie die Rolle 'RSExecRole' in der Systemdatenbank 'MSDB'  
  
1.  Wiederholen Sie ähnliche Schritte, um Berechtigungen für gespeicherte Prozeduren und Tabellen in MSDB zu erteilen. Um die Schritte zu vereinfachen, stellen Sie die gespeicherten Prozeduren und die Tabellen getrennt bereit.  
  
2.  Öffnen Sie **MSDB**.  
  
3.  Öffnen Sie **Sicherheit**.  
  
4.  Öffnen Sie **Rollen**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Datenbankrollen**, und wählen Sie **Neue Datenbankrolle**aus. Die Seite Allgemein wird angezeigt.  
  
6.  Geben Sie im Feld **Rollennamen**den Namen RSExecRole ein.  
  
7.  Geben Sie im Feld **Besitzer**die Zeichenfolge DBO ein.  
  
8.  Klicken Sie auf **Sicherungsfähige Elemente**.  
  
9. Klicken Sie auf **Hinzufügen**. Das Dialogfeld **Objekte hinzufügen** wird angezeigt. Standardmäßig ist die Option **Objekte angeben** aktiviert.  
  
10. Klicken Sie auf **OK**.  
  
11. Klicken Sie auf **Objekttypen**.  
  
12. Klicken Sie auf **Gespeicherte Prozeduren**.  
  
13. Klicken Sie auf **OK**.  
  
14. Klicken Sie auf **Durchsuchen**.  
  
15. Führen Sie in der Liste der Elemente einen Bildlauf durch, und wählen Sie Folgendes aus:  
  
    1.  sp_add_category  
  
    2.  sp_add_job  
  
    3.  sp_add_jobschedule  
  
    4.  sp_add_jobserver  
  
    5.  sp_add_jobstep  
  
    6.  sp_delete_job  
  
    7.  sp_help_category  
  
    8.  sp_help_job  
  
    9. sp_help_jobschedule  
  
    10. sp_verify_job_identifiers  
  
16. Klicken Sie auf **OK**, und klicken Sie dann nochmals auf **OK** .  
  
17. Wählen Sie die erste gespeicherte Prozedur aus: sp_add_category.  
  
18. Klicken Sie in der Zeile **Ausführen** auf das Kontrollkästchen in der Spalte **Erteilen** und dann auf **OK**.  
  
19. Wiederholen Sie diesen Schritt für alle übrigen gespeicherten Prozeduren. Der Rolle RSExecRole müssen Berechtigungen zum Ausführen aller zehn gespeicherten Prozeduren gewährt werden.  
  
20. Klicken Sie auf der Registerkarte **Sicherungsfähige Elemente** auf Hinzufügen. Das Dialogfeld **Objekte hinzufügen** wird angezeigt. Standardmäßig ist die Option **Objekte angeben** aktiviert.  
  
21. Klicken Sie auf **OK**.  
  
22. Klicken Sie auf **Objekttypen**.  
  
23. Klicken Sie auf **Tabellen.**  
  
24. Klicken Sie auf **OK**.  
  
25. Klicken Sie auf **Durchsuchen**.  
  
26. Führen Sie in der Liste der Elemente einen Bildlauf durch, und wählen Sie Folgendes aus:  
  
    1.  syscategories  
  
    2.  sysjobs  
  
27. Klicken Sie auf **OK**, und klicken Sie dann nochmals auf **OK** .  
  
28. Wählen Sie die erste Tabelle aus: syscategories.  
  
29. Klicken Sie in der Zeile **Auswählen** auf das Kontrollkästchen in der Spalte **Erteilen** und dann auf **OK**.  
  
30. Wiederholen Sie diesen Schritt für die Tabelle sysjobs. Die Rolle RSExecRole muss Berechtigungen zum Auswählen beider Tabellen erhalten.  
  
## <a name="move-the-report-server-database"></a>Verlagern der Berichtsserver-Datenbank  
 Nachdem Sie die Rollen erstellt haben, können Sie die Berichtsserver-Datenbank auf eine andere SQL Server-Instanz verschieben. Weitere Informationen finden Sie unter [die Berichtsserver-Datenbanken auf einen anderen Computer verschieben](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
 Wenn Sie ein Upgrade der [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu SQL Server 2016 aktualisieren vor oder nach dem Verschieben der Datenbank.  
  
 Die Berichtsserver-Datenbank wird automatisch aktualisiert werden, wenn der Berichtsserver, eine Verbindung herstellt. Zum Aktualisieren der Datenbank müssen keine bestimmten Schritte ausgeführt werden.  
  
## <a name="restore-encryption-keys-and-verify-your-work"></a>Wiederherstellen von Verschlüsselungsschlüsseln und Überprüfen der Arbeit  
 Nachdem die Berichtsserver-Datenbanken angefügt wurden, sollten Sie die folgenden Schritte ausführen können, um Ihre Implementierung zu überprüfen.  
  
#### <a name="to-verify-report-server-operability-after-a-database-move"></a>So überprüfen Sie nach einer Datenbankverschiebung die Funktionsfähigkeit des Berichtsservers  
  
1.  Starten Sie das Reporting Services-Konfigurationstool, und stellen Sie eine Verbindung mit dem Berichtsserver her.  
  
2.  Klicken Sie auf **Datenbank**.  
  
3.  Klicken Sie auf **Datenbank ändern**.  
  
4.  Sie können auch auf **Wählen Sie eine vorhandene Berichtsserver-Datenbank aus**klicken.  
  
5.  Geben Sie den Servernamen des Datenbankmoduls ein. Wenn die Berichtsserver-Datenbanken mit einer benannten Instanz angefügt wurde, müssen Sie den Instanznamen im folgenden Format eingeben: \<Servername >\\< Instancename\>.  
  
6.  Klicken Sie auf **Verbindung testen**.  
  
7.  Klicken Sie auf **Weiter**.  
  
8.  Wählen Sie die Berichtsserver-Datenbank aus.  
  
9. Klicken Sie auf **Weiter** , und beenden Sie den Assistenten.  
  
10. Klicken Sie auf **Verschlüsselungsschlüssel**.  
  
11. Klicken Sie auf **Wiederherstellen**.  
  
12. Wählen Sie die Datei mit starkem Namen (Dateierweiterung .snk) aus, welche die Sicherungskopie des symmetrischen Schlüssel enthält, der zum Entschlüsseln gespeicherter Anmeldeinformationen und Verbindungsinformationen in der Berichtsserver-Datenbank verwendet wird.  
  
13. Geben Sie das Kennwort ein, und klicken Sie auf **OK**.  
  
14. Klicken Sie auf **Berichts-Manager-URL**.  
  
15. Klicken Sie auf den Link zum Öffnen des Berichts-Managers. Daraufhin sollten die Berichtsserver-Elemente aus der Berichtsserver-Datenbank angezeigt werden.  

## <a name="next-steps"></a>Nächste Schritte

[Verschieben von Berichtsserver-Datenbanken auf einen anderen Computer &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)   
[Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
[Erstellen Sie eine Berichtsserver-Datenbank im einheitlichen Modus &#40; SSRS-Konfigurations-Manager &#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
[Sichern und Wiederherstellen von Reporting Services-Verschlüsselungsschlüsseln](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
