---
title: "Exemplarische Vorgehensweise: Einrichten von SQL Serverintegration Services für horizontales Skalieren | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 685286966599c4dcd3dc2f7029413c77f3ff2689
ms.openlocfilehash: c386b01043764405872365af379cfdedb036b65f
ms.contentlocale: de-de
ms.lasthandoff: 10/20/2017

---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>Exemplarische Vorgehensweise: Einrichten von horizontaler Hochskalierung für Integration Services
Richten Sie [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] horizontal skalieren, indem Sie die folgenden Aufgaben abschließen. 

> [!NOTE]
> Wenn Sie horizontal skalieren auf einem Computer installieren, installieren Sie die Scale-Out-Master "und" Scale-Out-Worker-Funktionen zur gleichen Zeit. Wenn Sie die Komponenten gleichzeitig installieren, wird automatisch der Endpunkt generiert, über den eine Verbindung mit Master für horizontales Hochskalieren hergestellt wird. 

* [Installieren von Master für horizontales Hochskalieren](#InstallMaster)

* [Installieren von Worker für horizontales Hochskalieren](#InstallWorker)

* [Installieren des Clientzertifikats für Worker für horizontales Hochskalieren](#InstallCert)

* [Öffnen des Firewallports](#Firewall)

* [Starten der SQL Server-Dienste Master und Worker für horizontales Hochskalieren](#Start)

* [Aktivieren von Master für horizontales Hochskalieren](#EnableMaster)

* [Aktivieren des SQL Server-Authentifizierungsmodus](#EnableAuth)

* [Aktivieren von Worker für horizontales Hochskalieren](#EnableWorker)

## <a name="InstallMaster"></a> Installieren von Master für horizontales Hochskalieren

Um die Funktionalität des Scale-Out-Master zu aktivieren, installieren Sie Database Engine Services, [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], und seine Scale-Out-Master-Funktion beim Einrichten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. 

Informationen zum Einrichten von Database Engine Services und [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], finden Sie unter [Installieren des SQL Server-Datenbankmoduls](../../database-engine/install-windows/install-sql-server-database-engine.md) und [Installieren von Integration Services](../install-windows/install-integration-services.md).
> [!NOTE]
> Um das Standardkonto für SQL-Authentifizierung für horizontales Skalieren Protokollierung verwenden, wählen Sie im gemischten Modus für den Authentifizierungsmodus auf der Seite "Datenbankmodulkonfiguration" auf, während der Installation des Datenbankmoduls. Finden Sie unter [Ändern des Kontos für horizontales Skalieren Protokollierung](change-logdb-account.md) für Weitere Informationen.

**Um die Komponente „Master für horizontales Hochskalieren“ zu installieren, verwenden Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] oder die Eingabeaufforderung.**

- Schritte für den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  Auf der **Funktionsauswahl** Seite **Scale-Out-Master**, dem wird er unter [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Komponentenauswahl Master](media/feature-select-master.PNG)
  
  2.  Wählen Sie auf der Seite **Serverkonfiguration** das Konto aus, unter dem der Dienst **Master für horizontales Hochskalieren von SQL Server Integration Service** ausgeführt werden soll, und wählen Sie den **Starttyp**aus.  
  ![Serverkonfiguration](media/server-config.PNG)
  3.  Geben Sie auf der Seite **Masterkonfiguration für horizontales Hochskalieren von Integration Services** die Portnummer an, über die Master für horizontales Hochskalieren und Worker für horizontales Hochskalieren kommunizieren. Die Standardportnummer ist 8391.  
  ![Master-Config](media/master-config.PNG "Master-Konfigurationsdatei")
  4.  Geben Sie das SSL-Zertifikat verwendet, um die Kommunikation zwischen Scale-Out-Master "und" Scale-Out-Worker zu schützen, indem Sie eine der folgenden Aktionen ausführen.
    * Führen Sie den Setupvorgang durch Klicken auf eine standardmäßige, selbstsignierte SSL-Zertifikat erstellen **erstellen Sie ein neues SSL-Zertifikat**.  Das Standardzertifikat wird unter „Vertrauenswürdige Stammzertifizierungsstellen“, „Lokaler Computer“ installiert. Sie können den Zertifikatnamen in diesem Zertifikat angeben. Der Hostname des master Endpunkt sollte im allgemeinen Namen enthalten sein. Standardmäßig sind die Computernamen und IP-Adresse der Master-Knoten enthalten.
    * Wählen Sie ein vorhandenes SSL-Zertifikat auf dem lokalen Computer, indem Sie auf **ein vorhandenes SSL-Zertifikat verwenden** und dann auf **Durchsuchen** um ein Zertifikat auszuwählen. Der Fingerabdruck des Zertifikats wird im Textfeld angezeigt. Nach Klicken auf **Durchsuchen** werden Zertifikate angezeigt, die in „Vertrauenswürdige Stammzertifizierungsstellen“, „Lokaler Computer“ gespeichert sind. Das Zertifikat, das Sie auswählen, muss hier gespeichert sein.       
![Master-Config 2](media/master-config-2.PNG "Master Config 2")
  5.  Schließen Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ab.
- Schritte für die Eingabeaufforderung

    Führen Sie die Anweisungen aus, die unter [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) angegeben sind. Legen Sie die zu Master für horizontales Hochskalieren gehörenden Parameter wie folgt fest.
  1.  Fügen Sie „IS_Master“ zum Parameter „/FEATURES“ hinzu.
  2.  Scale-Out-Master zu konfigurieren, indem Sie die folgenden Parameter und deren Werte angeben: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMasterSVCSSLCertCN(optional), /ISMASTERSVCTHUMBPRINT(optional).

> [!Note]
> Wenn Scale-Out-Master nicht zusammen mit Datenbankmodul installiert ist und das Datenbankmodul eine benannte Instanz ist, müssen Sie SQL Server-Name in der Konfigurationsdatei für den Scale-Out-Master-Dienst nach der Installation zu konfigurieren. Finden Sie unter [Scale-Out-Master](integration-services-ssis-scale-out-master.md) Details.

## <a name="InstallWorker"></a> Installieren von Worker für horizontales Hochskalieren
 
Um die Funktionalität von Worker für horizontales Hochskalieren zu aktivieren, müssen Sie [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] und deren Komponente „Worker für horizontales Hochskalieren“ in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Setup installieren.

**Um die Komponente „Worker für horizontales Hochskalieren“ zu installieren, verwenden Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] oder die Eingabeaufforderung.**

- Schritte für den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  Auf der **Funktionsauswahl** Seite **Scale-Out-Worker**, dem wird er unter [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Komponentenauswahl Worker](media/feature-select-worker.PNG)
  2. Wählen Sie auf der Seite **Serverkonfiguration** das Konto aus, unter dem der Dienst **Worker für horizontales Hochskalieren von SQL Server Integration Services** ausgeführt werden soll, und wählen Sie den **Starttyp**aus.    
  ![Serverkonfiguration 2](media/server-config-2.PNG "Serverkonfiguration 2")
  3. Geben Sie auf der Seite **Workerkonfiguration für horizontales Hochskalieren von Integration Services** den Endpunkt an, über den eine Verbindung mit Master für horizontales Hochskalieren hergestellt wird. 
      > [!Note]
      > Hier Überspringen von Worker-Knotenkonfiguration (Schritt 3 und 4) und Zuordnen der Scale-Out-Worker, Scale Out Master mit [Scale-Out-Manager](integration-services-ssis-scale-out-manager.md) nach der Installation.

    - Für eine **einem Computer** Umgebung, der Endpunkt wird automatisch generiert, wenn Scale-Out-Master "und" Scale-Out-Worker zur selben Zeit installiert werden. 
    - Für eine **mehrere Computer** Umgebung, der Endpunkt besteht aus den Namen oder die IP-Adresse des Computers mit Skalierung Out Master installiert und die Portnummer, die während der Installation Scale-Out-Master angegeben.    
   ![Worker Config 1](media/worker-config.PNG "Worker Config 1")    

  4. Für eine **mehrere Computer** Umgebung, geben Sie die Client-SSL-Zertifikat ab, das Scale-Out-Master zu überprüfen. Für eine **einem Computer** -Umgebung besteht keine Notwendigkeit, die Client-SSL-Zertifikat angeben. 
  
     > [!NOTE]
     > Wenn vom Scale-Out-Master verwendete SSL-Zertifikat selbstsigniert ist, muss einem entsprechenden SSL-Clientzertifikat auf dem Computer mit Scale-Out-Worker installiert sein. Wenn Sie den Dateipfad für den Client SSL-Zertifikat angeben, auf die **Scale Out Worker Konfiguration von Integration Services** Seite, das Zertifikat wird automatisch installiert; andernfalls, müssen Sie das Zertifikat manuell zu einem späteren Zeitpunkt zu installieren. 
     
     Klicken Sie auf **Durchsuchen** , um nach der Zertifikatdatei (*.cer) zu suchen. Um das Standard-SSL-Zertifikat verwenden möchten, wählen Sie die SSISScaleOutMaster.cer-Datei befindet sich im \<Laufwerk\>: \Programme\Microsoft SQL Server\140\DTS\Binn auf dem Computer, auf dem Scale-Out-Master installiert ist.   
   ![Worker Config 2](media/worker-config-2.PNG "Worker Config 2")
  5. Schließen Sie den Installations-Assistenten von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ab.
- Schritte für die Eingabeaufforderung

    Führen Sie die Anweisungen aus, die unter [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) angegeben sind. Legen Sie die zu Worker für horizontales Hochskalieren gehörenden Parameter wie folgt fest.
    1.  Fügen Sie „IS_Worker“ zum Parameter „/FEATURES“ hinzu.
    2. Konfigurieren der Skalierung Out Worker die folgenden Parameter und deren Werte angeben: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER(optional), /ISWORKERSVCCERT(optional).

 
## <a name="InstallCert"></a> Installieren des Clientzertifikats für Worker für horizontales Hochskalieren

Während der Installation von Scale-Out-Worker wird ein workerzertifikat automatisch erstellt und auf dem Computer installiert. Außerdem wird unter „ \<Treiber\>:\Programme\Microsoft SQL Server\140\DTS\Binn“ ein entsprechendes Clientzertifikat (SSISScaleOutWorker.cer) installiert. Für Skalierung Out Master auf der Skala, Worker zu authentifizieren müssen Sie dieses Clientzertifikat im Stammspeicher des lokalen Computers mit Scale-Out-Master für hinzufügen.
  
Um das Clientzertifikat zum Stammspeicher hinzuzufügen, doppelklicken Sie auf die CER-Datei, und klicken Sie dann im Dialogfeld „Zertifikat“ auf **Zertifikat installieren** . Der **Zertifikatimport-Assistent** wird angezeigt.  

## <a name="Firewall"></a> Öffnen des Firewallports

Öffnen Sie den Port angegeben werden, während die Scale-Out-Master-Installation und der Port des SQL Server (standardmäßig 1433) verwenden die Windows-Firewall auf dem Computer Scale-Out-Master.
    
## <a name="Start"></a> Starten der SQL Server-Dienste Master und Worker für horizontales Hochskalieren

Wenn der Starttyp der Dienste während der Installation nicht auf Automatic festgelegt ist, starten Sie die Dienste: SQL Server Integration Services Scale Out Master 14.0 (SSISScaleOutMaster140) und SQL Server Integration Services Scale Out Worker 14.0 (SSISScaleOutWorker140). 

> [!Note]
> Nach dem Öffnen des Firewallports müssen Sie auch den Scale-Out-Worker-Dienst neu starten.
   
## <a name="EnableMaster"></a> Aktivieren von Master für horizontales Hochskalieren

Klicken Sie im Dialogfeld **Katalog erstellen** auf **Diesen Server als SSIS-Master für horizontales Hochskalieren aktivieren**, wenn Sie den SSISDB-Katalog in [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)] erstellen. Alternativ kann Scale-Out-Master mit aktiviert [Scale-Out-Manager](integration-services-ssis-scale-out-manager.md) nachdem Katalog erstellt wurde.

## <a name="EnableAuth"></a> Aktivieren des SQL Server-Authentifizierungsmodus
Wenn [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Authentifizierung während der Installation des Datenbankmoduls nicht aktiviert ist, aktivieren Sie SQL Server-Authentifizierungsmodus auf den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] her, die den SSISDB-Katalog hostet. 

Paketausführung wird nicht blockiert, wenn SQL Server-Authentifizierung deaktiviert ist. Allerdings ist es nicht möglich, für das Ausführungsprotokoll in SSISDB zu schreiben.

## <a name="EnableWorker"></a> Aktivieren von Worker für horizontales Hochskalieren

Scale-Out-Worker kann aktiviert werden, über [Scale-Out-Manager](integration-services-ssis-scale-out-manager.md), bietet eine GUI; oder durch die gespeicherte Prozedur aktiviert wird, finden Sie weiter unten.

Um einen Worker für horizontales Hochskalieren zu aktivieren, führen Sie die gespeicherte Prozedur *[catalog].[enable_worker_agent]* mit **WorkerAgentId** als Parameter aus. 

Sie erhalten den **WorkerAgentId** -Wert aus der *[catalog].[worker_agents]* -Datenbanksicht in SSISDB, nachdem Worker für horizontales Hochskalieren bei Master für horizontales Hochskalieren registriert ist. Die Registrierung dauert einige Minuten, sobald die Dienste für Worker für horizontales Hochskalieren und Master für horizontales Hochskalieren gestartet wurden.

#### <a name="example"></a>Beispiel
In diesem Beispiel ermöglicht Scale Out Worker auf Computer a.
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
Das Einrichten des Features für horizontale Hochskalierung ist abgeschlossen. Sie können jetzt Pakete in horizontal skalieren ausgeführt werden. Weitere Informationen finden Sie unter [Ausführen von Paketen in horizontaler Hochskalierung für Integration Services (SSIS)](run-packages-in-integration-services-ssis-scale-out.md).

