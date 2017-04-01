---
title: "Exemplarische Vorgehensweise: Einrichten von horizontaler Hochskalierung f&#252;r Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cabb78a2-f234-46c3-842d-53aa2df8dfb3
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Exemplarische Vorgehensweise: Einrichten von horizontaler Hochskalierung f&#252;r Integration Services

Sie richten horizontale Hochskalierung für [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] ein, indem Sie die folgenden Aufgaben ausführen. 

> [!NOTE] Wenn Sie horizontale Hochskalierung auf einem Computer installieren, empfiehlt es sich, dass Sie die Komponenten „Master für horizontales Hochskalieren“ und „Worker für horizontales Hochskalieren“ gleichzeitig installieren. Wenn Sie die Komponenten gleichzeitig installieren, wird automatisch der Endpunkt generiert, über den eine Verbindung mit Master für horizontales Hochskalieren hergestellt wird. 

* [Installieren von Master für horizontales Hochskalieren](#InstallMaster)

* [Installieren von Worker für horizontales Hochskalieren](#InstallWorker)

* [Installieren des Clientzertifikats für Worker für horizontales Hochskalieren](#InstallCert)

* [Öffnen des Firewallports](#Firewall)

* [Starten der SQL Server-Dienste Master und Worker für horizontales Hochskalieren](#Start)

* [Aktivieren von Master für horizontales Hochskalieren](#EnableMaster)

* [Aktivieren des SQL Server-Authentifizierungsmodus](#EnableAuth)

* [Aktivieren von Worker für horizontales Hochskalieren](#EnableWorker)

## <a name="a-nameinstallmastera-install-scale-out-master"></a><a name="InstallMaster"></a> Installieren von Master für horizontales Hochskalieren

Um die Funktionalität von Master für horizontales Hochskalieren zu aktivieren, müssen Sie Database Engine Services, [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] und deren Komponente „Master für horizontales Hochskalieren“ installieren, wenn Sie [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] einrichten. 

Informationen zum Einrichten von Database Engine Services und [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)], finden Sie unter [Installieren des SQL Server-Datenbankmoduls](../database-engine/install-windows/install-sql-server-database-engine.md) und [Installieren von Integration Services](../integration-services/install-windows/install-integration-services.md).
> [!NOTE]
> Wählen Sie bei der Installation des Datenbankmoduls auf der Seite „Datenbankmodulkonfiguration“ für „Authentifizierung“ den Modus „Gemischter Modus“ aus. 

**Um die Komponente „Master für horizontales Hochskalieren“ zu installieren, verwenden Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] oder die Eingabeaufforderung.**

- Schritte für den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]
  1.  Aktivieren Sie auf der Seite **Funktionsauswahl** die Option **Master für horizontales Hochskalieren**, die unter [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] aufgeführt wird.   
  ![Komponentenauswahl Master](../integration-services/media/feature-select-master.PNG)
  
  2.  Wählen Sie auf der Seite **Serverkonfiguration** das Konto aus, unter dem der Dienst **Master für horizontales Hochskalieren von SQL Server Integration Service** ausgeführt werden soll, und wählen Sie den **Starttyp** aus.  
  ![Serverkonfiguration](../integration-services/media/server-config.PNG)
  3.  Geben Sie auf der Seite **Masterkonfiguration für horizontales Hochskalieren von Integration Services** die Portnummer an, über die Master für horizontales Hochskalieren und Worker für horizontales Hochskalieren kommunizieren. Die Standardportnummer ist 8391.  
  ![Master Config](../integration-services/media/master-config.PNG "Master Config")
  4.  Geben Sie das SSL-Zertifikat, mit dem die Kommunikation zwischen Master für horizontales Hochskalieren und Worker für horizontales Hochskalieren geschützt wird, mit einer der folgenden Vorgehensweisen an.
    * Lassen Sie durch den Setupvorgang ein standardmäßiges selbstsigniertes SSL-Zertifikat erstellen, indem Sie auf **Neues SSL-Zertifikat erstellen** klicken. Das Standardzertifikat wird unter „Vertrauenswürdige Stammzertifizierungsstellen“, „Lokaler Computer“ installiert.
    * Wählen Sie ein vorhandenes SSL-Zertifikat auf dem lokalen Computer aus, indem Sie auf **Vorhandenes SSL-Zertifikat verwenden** und dann auf **Durchsuchen** klicken. Der Fingerabdruck des Zertifikats wird im Textfeld angezeigt. Nach Klicken auf **Durchsuchen** werden Zertifikate angezeigt, die in „Vertrauenswürdige Stammzertifizierungsstellen“, „Lokaler Computer“ gespeichert sind. Das Zertifikat, das Sie auswählen, muss hier gespeichert sein.       
![Master Config 2](../integration-services/media/master-config-2.PNG "Master Config 2")
  5.  Schließen Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] ab.
- Schritte für die Eingabeaufforderung

    Führen Sie die Anweisungen aus, die unter [Installieren von SQL Server von der Eingabeaufforderung](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) angegeben sind. Legen Sie die zu Master für horizontales Hochskalieren gehörenden Parameter wie folgt fest.
  1.  Fügen Sie „IS_Master“ zum Parameter „/FEATURES“ hinzu.
  2.  Konfigurieren Sie Master für horizontales Hochskalieren mit Parametern: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMASTERSVCTHUMBPRINT (optional).
  
## <a name="a-nameinstallworkera-install-scale-out-worker"></a><a name="InstallWorker"></a> Installieren von Worker für horizontales Hochskalieren
 
Um die Funktionalität von Worker für horizontales Hochskalieren zu aktivieren, müssen Sie [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] und deren Komponente „Worker für horizontales Hochskalieren“ in [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]-Setup installieren.

**Um die Komponente „Worker für horizontales Hochskalieren“ zu installieren, verwenden Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] oder die Eingabeaufforderung.**

- Schritte für den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]
  1.  Aktivieren Sie auf der Seite **Funktionsauswahl** die Option **Worker für horizontales Hochskalieren**, die unter [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] aufgeführt wird.   
  ![Komponentenauswahl Worker](../integration-services/media/feature-select-worker.PNG)
  2. Wählen Sie auf der Seite **Serverkonfiguration** das Konto aus, unter dem der Dienst **Worker für horizontales Hochskalieren von SQL Server Integration Services** ausgeführt werden soll, und wählen Sie den **Starttyp** aus.    
  ![Server Config 2](../integration-services/media/server-config-2.PNG "Server Config 2")
  3. Geben Sie auf der Seite **Workerkonfiguration für horizontales Hochskalieren von Integration Services** den Endpunkt an, über den eine Verbindung mit Master für horizontales Hochskalieren hergestellt wird. 
    - Für eine **Ein-Computer**-Umgebung wird der Endpunkt automatisch generiert, wenn Master für horizontales Hochskalieren und Worker für horizontales Hochskalieren gleichzeitig installiert werden. 
    - Für eine **Multi-Computer**-Umgebung besteht der Endpunkt aus dem Namen oder der IP-Adresse des Computers, auf dem Master für horizontales Hochskalieren installiert ist, und der Portnummer, die während der Installation von Master für horizontales Hochskalieren angegeben wurde.    
   ![Worker Config 1](../integration-services/media/worker-config-1.PNG "Worker Config 1")
    
  4. Geben Sie für eine **Multi-Computer**-Umgebung das Client-SSL-Zertifikat an, das zum Überprüfen von Master für horizontales Hochskalieren verwendet wird. Für eine **Ein-Computer**-Umgebung besteht keine Notwendigkeit, das Client-SSL-Zertifikat anzugeben. 
  
     > [!NOTE] Ist das von Master für horizontales Hochskalieren verwendete SSL-Zertifikat selbstsigniert, muss auf dem Computer mit Master für horizontales Hochskalieren ein entsprechendes Client-SSL-Zertifikat installiert sein. Wenn Sie auf der Seite **Workerkonfiguration für horizontales Hochskalieren von Integration Services** den Dateipfad für das Client SSL-Zertifikat bereitstellen, wird es automatisch installiert. Andernfalls müssen Sie das Zertifikat später manuell installieren. 
     
     Klicken Sie auf **Durchsuchen**, um nach der Zertifikatdatei (*.cer) zu suchen. Soll das standardmäßige SSL-Zertifikat verwendet werden, wählen Sie die „SSISScaleOutMaster.cer“-Datei aus, die sich in „\<Laufwerk\>:\Programme\Microsoft SQL Server\140\DTS\Binn“ auf dem Computer befindet, auf dem Master für horizontales Hochskalieren installiert ist.   
   ![Worker Config 2](../integration-services/media/worker-config-2.PNG "Worker Config 2")
  5. Schließen Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] ab.
- Schritte für die Eingabeaufforderung

    Führen Sie die Anweisungen aus, die unter [Installieren von SQL Server von der Eingabeaufforderung](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) angegeben sind. Legen Sie die zu Worker für horizontales Hochskalieren gehörenden Parameter wie folgt fest.
    1.  Fügen Sie „IS_Worker“ zum Parameter „/FEATURES“ hinzu.
    2. Konfigurieren Sie Worker für horizontales Hochskalieren mit Parametern: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER (optional), /ISWORKERSVCCERT (optional).

 
## <a name="a-nameinstallcerta-install-scale-out-worker-client-certificate"></a><a name="InstallCert"><a/> Installieren des Clientzertifikats für Worker für horizontales Hochskalieren

Während der Installation von Worker für horizontales Hochskalieren wird automatisch ein Workerzertifikat auf dem Computer installiert. Außerdem wird unter „\<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn“ ein entsprechendes Clientzertifikat (SSISScaleOutWorker.cer) installiert. Damit Worker für horizontales Hochskalieren von Master für horizontales Hochskalieren authentifiziert werden kann, müssen Sie dieses Clientzertifikat zum Stammspeicher des lokalen Computers mit Master für horizontales Hochskalieren hinzufügen.
  
Um das Clientzertifikat zum Stammspeicher hinzuzufügen, doppelklicken Sie auf die CER-Datei, und klicken Sie dann im Dialogfeld „Zertifikat“ auf **Zertifikat installieren**. Der **Zertifikatimport-Assistent** wird angezeigt.  

## <a name="a-namefirewalla-open-firewall-port"></a><a name="Firewall"><a/> Öffnen des Firewallports

Öffnen Sie auf dem Computer, auf dem sich Master für horizontales Hochskalieren befindet, mit „Windows-Firewall“ den Port, den Sie während der Installation von Master für horizontales Hochskalieren angegeben haben.
    
## <a name="a-namestarta-start-sql-server-scale-out-master-and-worker-services"></a><a name="Start"></a> Starten der SQL Server-Dienste Master und Worker für horizontales Hochskalieren

Wenn der Starttyp der Dienste während der Installation nicht auf „Automatisch“ festgelegt wurde, starten Sie die Dienste: Master für horizontales Hochskalieren von SQL Server Integration Services 14.0 (SSISScaleOutMaster140) und Worker für horizontales Hochskalieren von SQL Server Integration Services 14.0 (SSISScaleOutWorker140). 

> [!NOTE]
>Nachdem Sie den Firewallport geöffnet haben, müssen Sie den Dienst für Worker für horizontales Hochskalieren neu starten.
   
## <a name="a-nameenablemastera-enable-scale-out-master"></a><a name="EnableMaster"></a> Aktivieren von Master für horizontales Hochskalieren

Klicken Sie im Dialogfeld **Katalog erstellen** auf **Diesen Server als SSIS-Master für horizontales Hochskalieren aktivieren**, wenn Sie den SSISDB-Katalog in [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)] erstellen.

## <a name="a-nameenableautha-enable-sql-server-authentication-mode"></a><a name="EnableAuth"></a> Aktivieren des SQL Server-Authentifizierungsmodus
Wenn die [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]-Authentifizierung während der Installation des Datenbankmoduls nicht aktiviert wurde, aktivieren Sie den SQL Server-Authentifizierungsmodus für die [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]-Instanz, die den SSISDB-Katalog hostet. 

Paketausführung wird nicht blockiert, wenn SQL Server-Authentifizierung deaktiviert ist. Allerdings ist es nicht möglich, für das Ausführungsprotokoll in SSISDB zu schreiben.

## <a name="a-nameenableworkera-enable-scale-out-worker"></a><a name="EnableWorker"></a> Aktivieren von Worker für horizontales Hochskalieren
Um einen Worker für horizontales Hochskalieren zu aktivieren, führen Sie die gespeicherte Prozedur *[catalog].[enable_worker_agent]* mit **WorkerAgentId** als Parameter aus. 

Sie erhalten den **WorkerAgentId**-Wert aus der *[catalog].[worker_agents]*-Datenbanksicht in SSISDB, nachdem Worker für horizontales Hochskalieren bei Master für horizontales Hochskalieren registriert ist. Die Registrierung dauert einige Minuten, sobald die Dienste für Worker für horizontales Hochskalieren und Master für horizontales Hochskalieren gestartet wurden.

### <a name="example"></a>Beispiel
In diesem Beispiel wird Worker für horizontales Hochskalieren auf „MachineA“ aktiviert.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>Nächste Schritte
Das Einrichten des Features für horizontale Hochskalierung ist abgeschlossen. Sie können jetzt Pakete in horizontaler Hochskalierung ausführen. Weitere Informationen finden Sie unter [Ausführen von Paketen in horizontaler Hochskalierung für Integration Services (SSIS)](../integration-services/run-packages-in-integration-services-ssis-scale-out.md).

