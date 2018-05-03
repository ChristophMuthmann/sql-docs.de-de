---
title: Erstellen einer Serverüberwachung und einer Serverüberwachungsspezifikation | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.SWB.SQLAUDIT.FILTER.F1
- sql13.swb.sqlaudit.general.f1
- sql13.swb.sqlaudit.srvaudit.general.f1
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
ms.assetid: 6624b1ab-7ec8-44ce-8292-397edf644394
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2e02bcddc94f5e5e82e48e4f8fab245e62e2b9b5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-server-audit-and-server-audit-specification"></a>Erstellen einer Serverüberwachung und einer Serverüberwachungsspezifikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie eine Serverüberwachung und Serverüberwachungsspezifikation in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)]erstellt wird. Bei der*Überwachung* einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank werden Ereignisse im System verfolgt und protokolliert. Das *SQL Server Audit* -Objekt listet eine einzelne Instanz an Aktionen oder Aktionsgruppen auf Server- oder Datenbankebene auf, die überwacht werden soll. Die Überwachung wird auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanzebene ausgeführt. Es können mehrere Überwachungen pro [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz vorliegen. Das *Serverüberwachungsspezifikation* -Objekt gehört zu einer Überwachung. Sie können eine Serverüberwachungsspezifikation pro Überwachung erstellen, da beide im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanzbereich erstellt werden. Weitere Informationen finden Sie unter [SQL Server Audit &#40;Datenbankmodul&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Security](#Security)  
  
-   **So erstellen Sie eine Serverüberwachung und eine Serverüberwachungsspezifikation mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Eine Überwachung muss vorhanden sein, bevor Sie eine Serverüberwachungsspezifikation für sie erstellen. Wenn eine Serverüberwachungsspezifikation erstellt wird, befindet sie sich im deaktivierten Zustand.  
  
-   Die CREATE SERVER AUDIT-Anweisung liegt im Bereich einer Transaktion. Wird ein Rollback für die Transaktion ausgeführt, so wird auch für die Anweisung ein Rollback durchgeführt.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
-   Um eine Serverüberwachung zu erstellen, zu ändern oder zu löschen, benötigen Prinzipale die ALTER ANY SERVER AUDIT-Berechtigung oder die CONTROL SERVER-Berechtigung.  
  
-   Benutzer mit der Berechtigung ALTER ANY SERVER AUDIT können Serverüberwachungsspezifikationen erstellen und diese an eine beliebige Überwachung binden.  
  
-   Sobald eine Serverüberwachungsspezifikation erstellt wurde, kann sie von Prinzipalen mit den folgenden Berechtigungen eingesehen werden: CONTROL SERVER oder ALTER ANY SERVER AUDIT. Außerdem kann sie von Prinzipalen eingesehen werden, die über das „sysadmin“-Konto oder expliziten Zugriff auf die Überwachung verfügen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>So erstellen Sie eine Serverüberwachung  
  
1.  Erweitern Sie im Objekt-Explorer den Ordner **Sicherheit** .  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Überwachungen** , und wählen Sie dann **Neue Überwachung**aus.  
  
     Die folgenden Optionen befinden sich im Dialogfeld **Überwachung erstellen** auf der Seite **Allgemein** :  
  
     **Überwachungsname**  
     Der Name der Überwachung. Der Name wird automatisch generiert, wenn Sie eine neue Überwachung erstellen, er kann jedoch bearbeitet werden.  
  
     **Warteschlangenverzögerung (in Millisekunden)**  
     Gibt in Millisekunden den Zeitraum an, der verstreichen kann, bevor die Verarbeitung von Überwachungsaktionen erzwungen wird.  Der Wert 0 steht für eine synchrone Übermittlung. Der standardmäßige Mindestwert beträgt **1000** (1 Sekunde). Der maximale Wert beträgt 2.147.483.647 (2.147.483,647 Sekunden oder 24 Tage, 20 Stunden, 31 Minuten und 23,647 Sekunden).  
  
     **Bei Überwachungsprotokollfehler:**  
     **Continue**  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Vorgänge werden fortgesetzt. Überwachungsdatensätze werden nicht beibehalten. Die Überwachung versucht weiterhin, Ereignisse zu protokollieren und wird fortgesetzt, wenn die Fehlerbedingung aufgelöst wurde. Durch Auswählen der **Continue** -Option können unter Umständen unüberwachte Aktivitäten ausgeführt werden, die gegen Ihre Sicherheitsrichtlinien verstoßen. Wählen Sie diese Option aus, wenn die weitere Verwendung von [!INCLUDE[ssDE](../../../includes/ssde-md.md)] wichtiger als die Beibehaltung einer vollständigen Überwachung ist. Dies ist die Standardauswahl.  
  
     **Herunterfahren des Servers**  
     Erzwingt, dass ein Server heruntergefahren wird, wenn die Serverinstanz, die in das Ziel schreiben soll, keine Daten in das Überwachungsziel schreiben kann. Die Anmeldung, die dies ausgibt, muss über die **SHUTDOWN** -Berechtigung verfügen. Wenn die Anmeldung nicht über diese Berechtigung verfügt, schlägt diese Funktion fehl, und es wird eine Fehlermeldung ausgegeben. Es treten keine überwachten Ereignisse auf. Wählen Sie diese Option aus, wenn ein Überwachungsfehler die Sicherheit oder die Integrität des Systems beeinträchtigen konnte.  
  
     **Fehler bei Vorgang**  
     In Fällen, in denen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit keine Informationen in das Überwachungsprotokoll schreiben kann, bewirkt diese Option, dass Datenbankaktionen fehlschlagen, wenn sie andernfalls überwachte Ereignisse verursachen würden. Es treten keine überwachten Ereignisse auf. Aktionen, die keine überwachten Ereignisse verursachen, können fortgesetzt werden. Die Überwachung versucht weiterhin, Ereignisse zu protokollieren und wird fortgesetzt, wenn die Fehlerbedingung aufgelöst wurde. Wählen Sie diese Option aus, wenn die Beibehaltung einer vollständigen Überwachung wichtiger als der Vollzugriff auf [!INCLUDE[ssDE](../../../includes/ssde-md.md)]ist.  
  
    > [!IMPORTANT]  
    >  Wenn sich die Überwachung in einem fehlerhaften Status befindet, kann die dedizierte Administratorverbindung weiterhin überwachte Ereignisse ausführen.  
  
     **Überwachungsziel** (Liste)  
     Gibt das Ziel für die Überwachungsdaten an. Die verfügbaren Optionen sind eine Binärdatei, das Windows-Anwendungsprotokoll oder das Windows-Sicherheitsprotokoll. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] kann nicht in das Windows-Sicherheitsprotokoll schreiben, ohne zusätzliche Einstellungen in Windows zu konfigurieren. Weitere Informationen finden Sie unter [Schreiben von SQL-Serverüberwachungsereignissen in das Sicherheitsprotokoll](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md).  
  
     **Dateipfad**  
     Gibt den Speicherort des Ordners an, in den Überwachungsdaten geschrieben werden, wenn das **Überwachungsziel** eine Datei ist.  
  
     **Auslassungspunkte (…)**  
     Öffnet das Dialogfeld **Ordner suchen –***server_name*, um einen Dateipfad anzugeben oder einen Ordner zu erstellen, in den die Überwachungsdatei geschrieben wird.  
  
     **Maximale Grenze für Überwachungsdatei:**  
     **Maximale Anzahl Rolloverdateien**  
     Wenn die maximale Anzahl von Überwachungsdateien erreicht wird, werden die ältesten Überwachungsdateien durch neuen Dateiinhalt überschrieben.  
  
     **Maximale Dateien**  
     Wenn die maximale Anzahl von Überwachungsdateien erreicht wird, tritt bei jeder Aktion, durch die zusätzliche Überwachungsereignisse verursacht werden, ein Fehler auf.  
  
     **Unbegrenzt** (Kontrollkästchen)  
     Wenn das Kontrollkästchen **Unbegrenzt** unter **Maximale Anzahl Rolloverdateien** aktiviert ist, kann eine unbegrenzte Anzahl von Rolloverdateien erstellt werden. Das Kontrollkästchen **Unbegrenzt** ist standardmäßig aktiviert und gilt sowohl für **Maximale Anzahl Rolloverdateien** als auch für **Maximale Dateien** .  
  
     **Anzahl der Dateien** (Feld)  
     Gibt die Anzahl von Überwachungsdateien an, die erstellt werden können, und zwar bis zu 2.147.483.647. Diese Option ist nur verfügbar, wenn **Unbegrenzt** deaktiviert ist.  
  
     **Maximale Dateigröße**  
     Gibt die maximale Größe für eine Überwachungsdatei entweder in Megabyte (MB), Gigabyte (GB) oder Terabyte (TB) an. Sie können zwischen 1024 MB und 2.147.483.647 TB angeben. Durch Aktivieren des Kontrollkästchen **Unbegrenzt** gibt es keine Begrenzung der Dateigröße. Die Angabe eines Werts kleiner 1024 MB löst einen Fehler aus. Das Kontrollkästchen **Unbegrenzt** ist standardmäßig aktiviert.  
  
     **Speicherplatz reservieren** (Kontrollkästchen)  
     Gibt an, dass der auf dem Datenträger vorab zugeordnete Speicherplatz der festgelegten maximalen Dateigröße entspricht. Diese Einstellung kann nur verwendet werden, wenn das Kontrollkästchen **Unbegrenzt** unter **Maximale Dateigröße** deaktiviert ist. Dieses Kontrollkästchen ist standardmäßig deaktiviert.  
  
3.  Geben Sie auf der Seite **Filter** optional ein Prädikat oder eine `WHERE` -Klausel für die Serverüberwachung ein, um Optionen anzugeben, die auf der Seite **Allgemein** nicht verfügbar sind. Schließen Sie das Prädikat in Klammern ein; z. B.: `(object_name = 'EmployeesTable')`.  
  
4.  Nachdem Sie alle Optionen ausgewählt haben, klicken Sie auf **OK**.  
  
#### <a name="to-create-a-server-audit-specification"></a>So erstellen Sie eine Serverüberwachungsspezifikation  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um den Ordner **Sicherheit** zu erweitern.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Serverüberwachungsspezifikationen** und dann auf **Neue Serverüberwachungsspezifikation**.  
  
     Die folgenden Optionen sind im Dialogfeld **Serverüberwachungsspezifikation erstellen** verfügbar.  
  
     **Name**  
     Der Name der Serverüberwachungsspezifikation. Er wird automatisch generiert, wenn Sie eine neue Serverüberwachungsspezifikation erstellen, er kann jedoch bearbeitet werden.  
  
     **Überwachung**  
     Der Name einer vorhandenen Serverüberwachung. Geben Sie den Namen der Überwachung ein, oder wählen Sie ihn aus der Liste aus.  
  
     **Überwachungsaktionstyp**  
     Gibt die aufzuzeichnenden Überwachungsaktionsgruppen auf Serverebene und Überwachungsaktionen an. Eine Liste der Überwachungsaktionsgruppen auf Serverebene und Überwachungsaktionen sowie eine Beschreibung der darin enthaltenen Ereignisse finden Sie unter [SQL Server Audit-Aktionsgruppen und -Aktionen](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
     **Objektschema**  
     Zeigt das Schema für den angegebenen **Objektnamen**an.  
  
     **Objektnamen**  
     Der Name des zu überwachenden Objekts. Das Objekt ist nur für Überwachungsaktionen verfügbar, es gilt nicht für Überwachungsgruppen.  
  
     **Auslassungspunkte (…)**  
     Öffnet das Dialogfeld **Objekte auswählen** , in dem Sie anhand des angegebenen **Überwachungsaktionstyps**nach einem verfügbaren Objekt suchen und es auswählen können.  
  
     **Prinzipalname**  
     Das Konto, anhand dessen die Überwachung für das zu überwachende Objekt gefiltert wird.  
  
     **Auslassungspunkte (…)**  
     Öffnet das Dialogfeld **Objekte auswählen** , in dem Sie nach einem verfügbaren Objekt anhand des angegebenen **Objektnamens**suchen und es auswählen können.  
  
3.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>So erstellen Sie eine Serverüberwachung  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Creates a server audit called "HIPPA_Audit" with a binary file as the target and no options.  
    CREATE SERVER AUDIT HIPAA_Audit  
        TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
    ```  
  
#### <a name="to-create-a-server-audit-specification"></a>So erstellen Sie eine Serverüberwachungsspezifikation  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    /*Creates a server audit specification called "HIPPA_Audit_Specification" that audits failed logins for the SQL Server audit "HIPPA_Audit" created above.  
    */  
  
    CREATE SERVER AUDIT SPECIFICATION HIPPA_Audit_Specification  
    FOR SERVER AUDIT HIPPA_Audit  
        ADD (FAILED_LOGIN_GROUP);  
    GO  
    -- Enables the audit.   
  
    ALTER SERVER AUDIT HIPAA_Audit  
    WITH (STATE = ON);  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md) und [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md).  
  
  
