---
title: 'Exemplarische Vorgehensweise: Einrichten von SQL Server Integration Services Scale Out | Microsoft-Dokumentation'
ms.description: This article walks you through the setup and configuration of SSIS Scale Out
ms.custom: ''
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: scale-out
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc1308eded686ab6b86a38b3bc700c7d101c8970
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="walkthrough-set-up-integration-services-ssis-scale-out"></a>Exemplarische Vorgehensweise: Einrichten von Scale Out für Integration Services (SSIS)
Richten Sie (SSIS-) Scale Out für [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] ein, indem Sie die folgenden Aufgaben ausführen. 

> [!TIP]
> Wenn Sie Scale Out auf einem einzelnen Computer installieren, installieren Sie gleichzeitig auch die Komponenten „Scale Out-Master “ und „Scale Out-Worker“. Wenn Sie die Komponenten gleichzeitig installieren, wird automatisch der Endpunkt generiert, über den eine Verbindung mit Master für horizontales Hochskalieren hergestellt wird. 

* [Installieren von Master für horizontales Hochskalieren](#InstallMaster)

* [Installieren von Worker für horizontales Hochskalieren](#InstallWorker)

* [Installieren des Clientzertifikats für Worker für horizontales Hochskalieren](#InstallCert)

* [Öffnen des Firewallports](#Firewall)

* [Starten der SQL Server-Dienste Master und Worker für horizontales Hochskalieren](#Start)

* [Aktivieren von Master für horizontales Hochskalieren](#EnableMaster)

* [Aktivieren des SQL Server-Authentifizierungsmodus](#EnableAuth)

* [Aktivieren von Worker für horizontales Hochskalieren](#EnableWorker)

## <a name="InstallMaster"></a> Installieren von Master für horizontales Hochskalieren

Zum Einrichten des Scale Out-Masters müssen Sie die Datenbank-Engine-Dienste [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] installieren. Für die Einrichtung von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] müssen Sie die Komponente „Scale Out-Master“ von SSIS installieren. 

Informationen zum Einrichten der Datenbank-Engine und [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] finden Sie unter [Installieren der SQL Server-Datenbank-Engine](../../database-engine/install-windows/install-sql-server-database-engine.md)und [Installieren von Integration Services](../install-windows/install-integration-services.md).

> [!NOTE]
> Wählen Sie während der Installation der Datenbank-Engine „Gemischter Modus“ als Authentifizierungsmodus auf der Seite **Database Engine Configuration** (Konfiguration der Datenbank-Engine) aus, um das Standardauthentifizierungskonto für SQL Server für die Scale Out-Protokollierung zu verwenden. Weitere Informationen finden Sie unter [Change the account for Scale Out logging (Ändern des Kontos für die Scale Out-Protokollierung)](change-logdb-account.md).

Verwenden Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] oder die Eingabeaufforderung, um die Komponente „Scale Out-Master“ zu installieren.

### <a name="install-scale-out-master-with-the-sql-server-installation-wizard"></a>Installieren des Scale Out-Masters mithilfe des SQL Server-Installations-Assistenten
1.  Aktivieren Sie auf der Seite **Funktionsauswahl** die Option **Scale Out-Master**, die unter [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aufgeführt wird.   
  
    ![Komponentenauswahl „Master“](media/feature-select-master.PNG)
  
2.  Wählen Sie auf der Seite **Serverkonfiguration** das Konto aus, unter dem der Dienst **Master für horizontales Hochskalieren von SQL Server Integration Service** ausgeführt werden soll, und wählen Sie den **Starttyp**aus.  
    ![Serverkonfiguration](media/server-config.PNG)

3.  Geben Sie auf der Seite **Masterkonfiguration für horizontales Hochskalieren von Integration Services** die Portnummer an, über die Master für horizontales Hochskalieren und Worker für horizontales Hochskalieren kommunizieren. Die Standardportnummer ist 8391.  

    ![Konfiguration von Scale Out-Master](media/master-config.PNG "Master Config")

4.  Geben Sie das SSL-Zertifikat, mit dem die Kommunikation zwischen dem Scale Out-Master und dem Scale Out-Worker geschützt wird, mit einer der folgenden folgendermaßen an.
    * Lassen Sie durch den Setupvorgang ein selbstsigniertes SSL-Standardzertifikat erstellen, indem Sie auf **Neues SSL-Zertifikat erstellen** klicken.  Das Standardzertifikat wird unter „Vertrauenswürdige Stammzertifizierungsstellen“, „Lokaler Computer“ installiert. Sie können die allgemeinen Namen in diesem Zertifikat angeben. Der Hostname des Masterendpunkts sollte in den allgemeinen Namen enthalten sein. Standardmäßig sind der Computername und die IP-Adresse des Masterknotens nicht enthalten.
    * Wählen Sie ein vorhandenes SSL-Zertifikat auf dem lokalen Computer aus, indem Sie zuerst auf **vorhandenes SSL-Zertifikat verwenden** und dann auf **Durchsuchen** klicken. Der Fingerabdruck des Zertifikats wird im Textfeld angezeigt. Nach Klicken auf **Durchsuchen** werden Zertifikate angezeigt, die in „Vertrauenswürdige Stammzertifizierungsstellen“, „Lokaler Computer“ gespeichert sind. Das Zertifikat, das Sie auswählen, muss hier gespeichert sein.       

    ![Konfiguration von Scale Out-Master (2)](media/master-config-2.PNG "Master Config 2")
  
5.  Schließen Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ab.

### <a name="install-scale-out-master-from-the-command-prompt"></a>Installieren des Scale Out-Masters über die Eingabeaufforderung

Führen Sie die Anweisungen aus, die unter [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) angegeben sind. Führen Sie die folgenden Schritte aus, um die Parameter für den Scale Out-Master festzulegen:
 
1.  Fügen Sie dem Parameter `/FEATURES` `IS_Master` hinzu

2.  Konfigurieren Sie den Scale Out-Master, indem Sie die folgenden Parameter und deren Werte angeben:
    -   `/ISMASTERSVCACCOUNT`
    -   `/ISMASTERSVCPASSWORD`
    -   `/ISMASTERSVCSTARTUPTYPE`
    -   `/ISMASTERSVCPORT`
    -   `/ISMasterSVCSSLCertCN` (optional)
    -   `/ISMASTERSVCTHUMBPRINT` (optional)

    > [!NOTE]
    > Wenn der Scale Out-Master nicht zusammen mit der Datenbank-Engine installiert wurde und diese eine benannte Instanz darstellt, müssen Sie `SqlServerName` nach der Installation in der Dienstkonfigurationsdatei des Scale Out-Masters konfigurieren. Weitere Informationen finden Sie unter [Scale Out-Master](integration-services-ssis-scale-out-master.md).

## <a name="InstallWorker"></a> Installieren von Worker für horizontales Hochskalieren
 
Installieren Sie [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] und dessen Komponente „Scale Out-Worker“ im [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Setup, um den Scale Out-Worker einzurichten.

Verwenden Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] oder die Eingabeaufforderung, um die Komponente „Scale Out-Worker“ zu installieren.

### <a name="install-scale-out-worker-with-the-sql-server-installation-wizard"></a>Installieren des Scale Out-Workers mithilfe des SQL Server-Installations-Assistenten

1.  Aktivieren Sie auf der Seite **Funktionsauswahl** die Option **Scale Out-Worker**, die unter [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aufgeführt wird.

    ![Komponentenauswahl „Worker“](media/feature-select-worker.PNG)

2.  Wählen Sie auf der Seite **Serverkonfiguration** das Konto aus, unter dem der Dienst **Worker für horizontales Hochskalieren von SQL Server Integration Services** ausgeführt werden soll, und wählen Sie den **Starttyp**aus.

    ![Serverkonfiguration (2)](media/server-config-2.PNG "Server Config 2")

3.  Geben Sie auf der Seite **Workerkonfiguration für horizontales Hochskalieren von Integration Services** den Endpunkt an, über den eine Verbindung mit Master für horizontales Hochskalieren hergestellt wird. 

    - Für eine Umgebung mit **einem einzelnen Computer** wird der Endpunkt automatisch generiert, wenn der Scale Out-Master und der Scale Out-Worker gleichzeitig installiert werden. 

    - Für eine Umgebung mit **mehreren Computern** besteht der Endpunkt aus dem Namen oder der IP-Adresse des Computers, auf dem der Scale Out-Master installiert ist, und der Portnummer, die während der Installation des Scale Out-Masters angegeben wurde.
   
    ![Konfiguration von Scale Out-Worker (1)](media/worker-config.PNG "Worker Config 1")    

    > [!NOTE]
    > Sie können die Konfiguration des Workers an dieser Stelle überspringen und den [Scale Out-Manager](integration-services-ssis-scale-out-manager.md) verwenden, um den Scale Out-Worker und den Scale Out-Master einander zuzuordnen.

4. Geben Sie für eine Umgebung mit **mehreren Computern** das SSL-Zertifikat des Clients an, das zum Überprüfen des Scale Out-Masters verwendet wird. Für eine Umgebung mit nur **einem einzelnen Computer** müssen Sie kein SSL-Zertifikat des Clients angeben. 
  
    Klicken Sie auf **Durchsuchen** , um nach der Zertifikatdatei (*.cer) zu suchen. Wählen Sie die Datei `SSISScaleOutMaster.cer` aus, die sich auf dem Computer, auf dem der Scale Out-Master installiert ist, unter `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn` befindet, um das SSL-Standardzertifikat zu verwenden.   

    ![Konfiguration von Scale Out-Worker (2)](media/worker-config-2.PNG "Worker Config 2")

    > [!NOTE]
    > Ist das vom Scale Out-Master verwendete SSL-Zertifikat selbstsigniert, muss auf dem Computer mit dem Scale Out-Master ein entsprechendes SSL-Zertifikat des Clients installiert sein. Wenn Sie auf der Seite **Integration Services Scale Out Worker Configuration (Konfiguration für den Integration Services Scale Out-Worker)** den Dateipfad für das Client SSL-Zertifikat bereitstellen, wird es automatisch installiert. Andernfalls müssen Sie das Zertifikat später manuell installieren. 
     
5. Schließen Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ab.

### <a name="install-scale-out-worker-from-the-command-prompt"></a>Installieren des Scale Out-Workers über die Eingabeaufforderung

Führen Sie die Anweisungen aus, die unter [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) angegeben sind. Führen Sie die folgenden Schritte aus, um die Parameter für den Scale Out-Worker festzulegen:

1.  Fügen Sie „IS_Worker“ zum Parameter `/FEATURES` hinzu.

2. Konfigurieren Sie den Scale Out-Worker, indem Sie die folgenden Parameter und deren Werte angeben:
    -   `/ISWORKERSVCACCOUNT`
    -   `/ISWORKERSVCPASSWORD`
    -   `/ISWORKERSVCSTARTUPTYPE`
    -   `/ISWORKERSVCMASTER` (optional)
    -   `/ISWORKERSVCCERT` (optional)
 
## <a name="InstallCert"></a> Installieren des Clientzertifikats für Worker für horizontales Hochskalieren

Während der Installation des Scale Out-Workers wird automatisch ein Workerzertifikat auf dem Computer installiert. Außerdem wird unter `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn` ein entsprechendes Clientzertifikat („SSISScaleOutWorker.cer“) installiert. Damit der Scale Out-Master vom Scale Out-Worker authentifiziert werden kann, müssen Sie dieses Clientzertifikat zum Stammspeicher des lokalen Computers mit dem Scale Out-Master hinzufügen.
  
Doppelklicken Sie auf die CER-Datei, und klicken Sie dann im Dialogfeld „Zertifikat“ auf **Zertifikat installieren**, um das Clientzertifikat zum Stammspeicher hinzuzufügen. Der **Zertifikatimport-Assistent** wird geöffnet.  

## <a name="Firewall"></a> Öffnen des Firewallports

Öffnen Sie in der Windows-Firewall auf dem Computer mit dem Scale Out-Master den Port, der während der Installation des Scale Out-Masters angegeben wurde sowie den Port von SQL Server (standardmäßig 1433).

> [!Note]
> Nachdem Sie den Firewallport geöffnet haben, müssen Sie den Dienst für den Scale Out-Worker neu starten.
    
## <a name="Start"></a> Starten der SQL Server-Dienste Master und Worker für horizontales Hochskalieren

Wenn Sie bei der Installation den Starttyp der Dienste nicht auf **Automatisch** festgelegt haben, starten Sie die folgenden Dienste:

-   SQL Server Integration Services Scale Out-Master 14.0 (SSISScaleOutMaster140)

-   SQL Server Integration Services Scale Out-Worker 14.0 (SSISScaleOutWorker140)

## <a name="EnableMaster"></a> Aktivieren von Master für horizontales Hochskalieren

Klicken Sie im Dialogfeld **Katalog erstellen** auf **Diesen Server als SSIS Scale Out-Master aktivieren**, wenn Sie den SSISDB-Katalog in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)] erstellen.

Nach dem Erstellen des Katalogs können Sie den Scale Out-Master mithilfe des [Scale Out-Managers](integration-services-ssis-scale-out-manager.md) aktivieren.

## <a name="EnableAuth"></a> Aktivieren des SQL Server-Authentifizierungsmodus
Wenn Sie die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Authentifizierung während der Installation der Datenbank-Engine nicht aktiviert haben, aktivieren Sie den SQL Server-Authentifizierungsmodus für die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz, die den SSISDB-Katalog hostet. 

Paketausführung wird nicht blockiert, wenn SQL Server-Authentifizierung deaktiviert ist. Allerdings kann das Ausführungsprotokoll nicht in SSISDB schreiben.

## <a name="EnableWorker"></a> Aktivieren von Worker für horizontales Hochskalieren

Sie können den Scale Out-Worker mithilfe des [Scale Out-Managers](integration-services-ssis-scale-out-manager.md), der eine grafische Benutzeroberfläche bereitstellt, oder mithilfe einer gespeicherten Prozedur aktivieren.

Um einen Scale Out-Worker mit einer gespeicherten Prozedur zu aktivieren, führen Sie die gespeicherte Prozedur `[catalog].[enable_worker_agent]` mit **WorkerAgentId** als Parameter aus. 

Sie erhalten den Wert **WorkerAgentId** aus der Ansicht `[catalog].[worker_agents]` in SSISDB, nachdem der Scale Out-Worker beim Scale Out-Master registriert wurde. Die Registrierung dauert einige Minuten, nach dem Starten der Dienste Scale Out-Master und Scale Out-Worker.

#### <a name="example"></a>Beispiel
Im folgenden Beispiel wird der Scale Out-Worker auf `computerA` aktiviert.

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
-   [Ausführen von Paketen in SSIS Scale Out (SQL Server Integration Services)](run-packages-in-integration-services-ssis-scale-out.md)
