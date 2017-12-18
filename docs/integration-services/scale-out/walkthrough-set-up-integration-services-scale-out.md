---
title: 'Exemplarische Vorgehensweise: Einrichten von SQL Server Integration Services Scale Out | Microsoft-Dokumentation'
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ec9744a1efb0e78aca55e85e7f9f3eca007de5a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>Exemplarische Vorgehensweise: Einrichten von horizontaler Hochskalierung für Integration Services
Richten Sie Scale Out für [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] ein, indem Sie die folgenden Aufgaben ausführen. 

> [!NOTE]
> Wenn Sie Scale Out auf einem Computer installieren, installieren Sie gleichzeitig die Funktionen „Scale Out-Master “ und „Scale Out-Worker“. Wenn Sie die Komponenten gleichzeitig installieren, wird automatisch der Endpunkt generiert, über den eine Verbindung mit Master für horizontales Hochskalieren hergestellt wird. 

* [Installieren von Master für horizontales Hochskalieren](#InstallMaster)

* [Installieren von Worker für horizontales Hochskalieren](#InstallWorker)

* [Installieren des Clientzertifikats für Worker für horizontales Hochskalieren](#InstallCert)

* [Öffnen des Firewallports](#Firewall)

* [Starten der SQL Server-Dienste Master und Worker für horizontales Hochskalieren](#Start)

* [Aktivieren von Master für horizontales Hochskalieren](#EnableMaster)

* [Aktivieren des SQL Server-Authentifizierungsmodus](#EnableAuth)

* [Aktivieren von Worker für horizontales Hochskalieren](#EnableWorker)

## <a name="InstallMaster"></a> Installieren von Master für horizontales Hochskalieren

Sie müssen beim Einrichten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Datenbankmoduldienste, [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] und die Funktion „Scale Out-Master“ installieren, um die Funktionalität des Scale Out-Masters zu aktivieren. 

Informationen zum Einrichten von Database Engine Services und [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], finden Sie unter [Installieren des SQL Server-Datenbankmoduls](../../database-engine/install-windows/install-sql-server-database-engine.md) und [Installieren von Integration Services](../install-windows/install-integration-services.md).
> [!NOTE]
> Wählen Sie während der Installation des Datenbankmoduls „Gemischter Modus“ als Authentifizierungsmodus auf der Seite „Datenbankmodulkonfiguration“ aus, um das Standardauthentifizierungskonto für die SQL Scale Out-Protokollierung zu verwenden. Weitere Informationen finden Sie unter [Change the account for Scale Out logging (Ändern des Kontos für die Scale Out-Protokollierung)](change-logdb-account.md).

**Um die Komponente „Master für horizontales Hochskalieren“ zu installieren, verwenden Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] oder die Eingabeaufforderung.**

- Schritte für den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  Aktivieren Sie auf der Seite **Funktionsauswahl** die Option **Scale Out-Master**, die unter [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aufgeführt wird.   
  ![Komponentenauswahl Master](media/feature-select-master.PNG)
  
  2.  Wählen Sie auf der Seite **Serverkonfiguration** das Konto aus, unter dem der Dienst **Master für horizontales Hochskalieren von SQL Server Integration Service** ausgeführt werden soll, und wählen Sie den **Starttyp**aus.  
  ![Serverkonfiguration](media/server-config.PNG)
  3.  Geben Sie auf der Seite **Masterkonfiguration für horizontales Hochskalieren von Integration Services** die Portnummer an, über die Master für horizontales Hochskalieren und Worker für horizontales Hochskalieren kommunizieren. Die Standardportnummer ist 8391.  
  ![Konfiguration von Scale Out-Master](media/master-config.PNG "Master Config")
  4.  Geben Sie das SSL-Zertifikat, mit dem die Kommunikation zwischen dem Scale Out-Master und dem Scale Out-Worker geschützt wird, mit einer der folgenden folgendermaßen an.
    * Lassen Sie durch den Setupvorgang ein selbstsigniertes SSL-Standardzertifikat erstellen, indem Sie auf **Neues SSL-Zertifikat erstellen** klicken.  Das Standardzertifikat wird unter „Vertrauenswürdige Stammzertifizierungsstellen“, „Lokaler Computer“ installiert. Sie können die allgemeinen Namen in diesem Zertifikat angeben. Der Hostname des Masterendpunkts sollte in den allgemeinen Namen enthalten sein. Standardmäßig sind der Computername und die IP-Adresse des Masterknotens nicht enthalten.
    * Wählen Sie ein vorhandenes SSL-Zertifikat auf dem lokalen Computer aus, indem Sie auf **Vorhandenes SSL-Zertifikat verwenden** und dann auf **Durchsuchen** klicken. Der Fingerabdruck des Zertifikats wird im Textfeld angezeigt. Nach Klicken auf **Durchsuchen** werden Zertifikate angezeigt, die in „Vertrauenswürdige Stammzertifizierungsstellen“, „Lokaler Computer“ gespeichert sind. Das Zertifikat, das Sie auswählen, muss hier gespeichert sein.       
![Konfiguration von Scale Out-Master (2)](media/master-config-2.PNG "Master Config 2")
  5.  Schließen Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ab.
- Schritte für die Eingabeaufforderung

    Führen Sie die Anweisungen aus, die unter [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) angegeben sind. Legen Sie die zu Master für horizontales Hochskalieren gehörenden Parameter wie folgt fest.
  1.  Fügen Sie „IS_Master“ zum Parameter „/FEATURES“ hinzu.
  2.  Konfigurieren Sie den Scale Out-Master, indem Sie folgende Parameter und deren Werte angeben: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMasterSVCSSLCertCN (optional), /ISMASTERSVCTHUMBPRINT (optional).

> [!Note]
> Wenn der Scale Out-Master nicht zusammen mit dem Datenbankmodul installiert wurde und dieses eine benannte Instanz darstellt, müssen Sie „SqlServerName“ nach der Installation in der Dienstkonfigurationsdatei des Scale Out-Masters konfigurieren. Weitere Informationen finden Sie im Artikel zum [Scale Out-Master](integration-services-ssis-scale-out-master.md).

## <a name="InstallWorker"></a> Installieren von Worker für horizontales Hochskalieren
 
Um die Funktionalität von Worker für horizontales Hochskalieren zu aktivieren, müssen Sie [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] und deren Komponente „Worker für horizontales Hochskalieren“ in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Setup installieren.

**Um die Komponente „Worker für horizontales Hochskalieren“ zu installieren, verwenden Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] oder die Eingabeaufforderung.**

- Schritte für den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  Aktivieren Sie auf der Seite **Funktionsauswahl** die Option **Scale Out-Worker**, die unter [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aufgeführt wird.   
  ![Komponentenauswahl Worker](media/feature-select-worker.PNG)
  2. Wählen Sie auf der Seite **Serverkonfiguration** das Konto aus, unter dem der Dienst **Worker für horizontales Hochskalieren von SQL Server Integration Services** ausgeführt werden soll, und wählen Sie den **Starttyp**aus.    
  ![Serverkonfiguration (2)](media/server-config-2.PNG "Server Config 2")
  3. Geben Sie auf der Seite **Workerkonfiguration für horizontales Hochskalieren von Integration Services** den Endpunkt an, über den eine Verbindung mit Master für horizontales Hochskalieren hergestellt wird. 
      > [!Note]
      > Sie können die Konfiguration des Workerknotens (Schritt 3 und 4) hier überspringen und den [Scale Out-Manager](integration-services-ssis-scale-out-manager.md) verwenden, um den Scale Out-Worker und den Scale Out-Master einander zuzuordnen.

    - Für eine Umgebung mit **einem Computer** wird der Endpunkt automatisch generiert, wenn der Scale Out-Master und der Scale Out-Worker gleichzeitig installiert werden. 
    - Für eine Umgebung mit **mehreren Computern** besteht der Endpunkt aus dem Namen oder der IP-Adresse des Computers, auf dem der Scale Out-Master installiert ist, und der Portnummer, die während der Installation des Scale Out-Masters angegeben wurde.    
   ![Konfiguration von Scale Out-Worker (1)](media/worker-config.PNG "Worker Config 1")    

  4. Geben Sie für eine Umgebung mit **mehreren Computern** das Client-SSL-Zertifikat an, das zum Überprüfen des Scale Out-Masters verwendet wird. Bei einer Umgebung mit **einem Computer** ist es nicht erforderlich, das Client-SSL-Zertifikat anzugeben. 
  
     > [!NOTE]
     > Ist das vom Scale Out-Master verwendete SSL-Zertifikat selbstsigniert, muss auf dem Computer mit dem Scale Out-Master ein entsprechendes Client-SSL-Zertifikat installiert sein. Wenn Sie auf der Seite **Integration Services Scale Out Worker Configuration (Konfiguration für den Integration Services Scale Out-Worker)** den Dateipfad für das Client SSL-Zertifikat bereitstellen, wird es automatisch installiert. Andernfalls müssen Sie das Zertifikat später manuell installieren. 
     
     Klicken Sie auf **Durchsuchen** , um nach der Zertifikatdatei (*.cer) zu suchen. Soll das SSL-Standardzertifikat verwendet werden, wählen Sie die Datei „SSISScaleOutMaster.cer“ aus, die sich unter \<Laufwerk\>:\Programme\Microsoft SQL Server\140\DTS\Binn auf dem Computer befindet, auf dem Scale Out-Master installiert ist.   
   ![Konfiguration von Scale Out-Worker (2)](media/worker-config-2.PNG "Worker Config 2")
  5. Schließen Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ab.
- Schritte für die Eingabeaufforderung

    Führen Sie die Anweisungen aus, die unter [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) angegeben sind. Legen Sie die zu Worker für horizontales Hochskalieren gehörenden Parameter wie folgt fest.
    1.  Fügen Sie „IS_Worker“ zum Parameter „/FEATURES“ hinzu.
    2. Konfigurieren Sie den Scale Out-Worker, indem Sie folgende Parameter und deren Werte angeben: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER (optional), /ISWORKERSVCCERT (optional).

 
## <a name="InstallCert"></a> Installieren des Clientzertifikats für Worker für horizontales Hochskalieren

Während der Installation des Scale Out-Workers wird automatisch ein Workerzertifikat auf dem Computer installiert. Außerdem wird unter „ \<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn“ ein entsprechendes Clientzertifikat (SSISScaleOutWorker.cer) installiert. Damit der Scale Out-Worker vom Scale Out-Master authentifiziert werden kann, müssen Sie dieses Clientzertifikat zum Stammspeicher des lokalen Computers mit dem Scale Out-Master hinzufügen.
  
Um das Clientzertifikat zum Stammspeicher hinzuzufügen, doppelklicken Sie auf die CER-Datei, und klicken Sie dann im Dialogfeld „Zertifikat“ auf **Zertifikat installieren** . Der **Zertifikatimport-Assistent** wird angezeigt.  

## <a name="Firewall"></a> Öffnen des Firewallports

Öffnen Sie mithilfe der Windows-Firewall auf dem Computer mit dem Scale Out-Master den Port, der während der Installation des Scale Out-Masters angegeben wurde sowie den Port von SQL Server (standardmäßig 1433).
    
## <a name="Start"></a> Starten der SQL Server-Dienste Master und Worker für horizontales Hochskalieren

Wenn der Starttyp der Dienste während der Installation nicht auf „Automatisch“ festgelegt wurde, starten Sie folgende Dienste: SQL Server Integration Services Scale Out-Master 14.0 (SSISScaleOutMaster140) und SQL Server Integration Services Scale Out-Worker 14.0 (SSISScaleOutWorker140). 

> [!Note]
> Nachdem Sie den Firewallport geöffnet haben, müssen Sie den Dienst für den Scale Out-Worker neu starten.
   
## <a name="EnableMaster"></a> Aktivieren von Master für horizontales Hochskalieren

Klicken Sie im Dialogfeld **Katalog erstellen** auf **Diesen Server als SSIS-Master für horizontales Hochskalieren aktivieren**, wenn Sie den SSISDB-Katalog in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)] erstellen. Alternativ kann der Scale Out-Master mit dem [Scale Out-Manager](integration-services-ssis-scale-out-manager.md) aktiviert werden, nachdem der Katalog erstellt wurde.

## <a name="EnableAuth"></a> Aktivieren des SQL Server-Authentifizierungsmodus
Wenn die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Authentifizierung während der Installation des Datenbankmoduls nicht aktiviert wurde, aktivieren Sie den SQL Server-Authentifizierungsmodus für die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz, die den SSISDB-Katalog hostet. 

Paketausführung wird nicht blockiert, wenn SQL Server-Authentifizierung deaktiviert ist. Allerdings ist es nicht möglich, für das Ausführungsprotokoll in SSISDB zu schreiben.

## <a name="EnableWorker"></a> Aktivieren von Worker für horizontales Hochskalieren

Der Scale Out-Worker kann wie im Folgenden dargestellt über gespeicherte Prozeduren oder über den [Scale Out-Manager](integration-services-ssis-scale-out-manager.md) aktiviert werden, der die grafische Benutzeroberfläche bereitstellt.

Um einen Worker für horizontales Hochskalieren zu aktivieren, führen Sie die gespeicherte Prozedur *[catalog].[enable_worker_agent]* mit **WorkerAgentId** als Parameter aus. 

Sie erhalten den **WorkerAgentId** -Wert aus der *[catalog].[worker_agents]* -Datenbanksicht in SSISDB, nachdem Worker für horizontales Hochskalieren bei Master für horizontales Hochskalieren registriert ist. Die Registrierung dauert einige Minuten, sobald die Dienste für Worker für horizontales Hochskalieren und Master für horizontales Hochskalieren gestartet wurden.

#### <a name="example"></a>Beispiel
In diesem Beispiel wird der Scale Out-Worker auf „ComputerA“ aktiviert.
```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>Nächste Schritte
Das Einrichten des Features für horizontale Hochskalierung ist abgeschlossen. Sie können jetzt Pakete in Scale Out ausführen. Weitere Informationen finden Sie unter [Ausführen von Paketen in horizontaler Hochskalierung für Integration Services (SSIS)](run-packages-in-integration-services-ssis-scale-out.md).
