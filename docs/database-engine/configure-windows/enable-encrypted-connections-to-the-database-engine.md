---
title: "Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 754242a86367b07b98caa9f70f457b70d0840075
ms.openlocfilehash: a00e09f47685eba578296b8e390d3c7d15fc6953
ms.contentlocale: de-de
ms.lasthandoff: 09/12/2017

---
# <a name="enable-encrypted-connections-to-the-database-engine"></a>Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie Sie verschlüsselte Verbindungen für eine Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] durch Angeben eines Zertifikats für die [!INCLUDE[ssDE](../../includes/ssde-md.md)] mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Managers aktivieren können. Für den Servercomputer muss ein Zertifikat bereitgestellt worden sein, und der Clientcomputer muss so eingerichtet sein, dass er die Stammzertifizierungsstelle des Zertifikats als vertrauenswürdig einstuft. Zertifikate werden bereitgestellt, indem sie mithilfe eines Importvorgangs in Windows installiert werden.  
  
 Das Zertifikat muss für die **Serverauthentifizierung**ausgegeben sein. Der Name des Zertifikats muss der vollqualifizierte Domänenname (FQDN) des Computers sein.  
  
 Zertifikate werden lokal für diesen Benutzer auf dem Computer gespeichert. Sie müssen den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Configuration Manager mit einem Konto mit lokalen Administratorberechtigungen ausführen, um ein Zertifikat zu installieren, das von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden soll.
 
  
 Der Client muss in der Lage sein, den Besitzer des vom Server verwendeten Zertifikats zu überprüfen. Wenn der Client über das Zertifikat für öffentliche Schlüssel der Zertifizierungsstelle verfügt, die das Serverzertifikat signiert hat, sind keine weiteren Konfigurationsschritte erforderlich. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows enthält die Zertifikate für öffentliche Schlüssel von vielen Zertifizierungsstellen. Wenn das Serverzertifikat von einer öffentlichen oder privaten Zertifizierungsstelle signiert wurde, für die der Client kein öffentliches Schlüsselzertifikat besitzt, müssen Sie das Zertifikat für öffentliche Schlüssel der Zertifizierungsstelle installieren, die das Serverzertifikat signiert hat.  
  
> [!NOTE]  
>  Wenn Sie die Verschlüsselung bei einem Failovercluster verwenden möchten, müssen Sie das Serverzertifikat mit dem vollqualifizierten DNS-Namen des virtuellen Servers auf allen Knoten im Failovercluster installieren. Wenn Sie z.B. über einen Cluster mit zwei Knoten verfügen, wobei die Knotennamen test1.*\<Ihr_Unternehmen>*.com und test2.*\<Ihr_Unternehmen>*.com lauten, und ein virtueller Server den Namen „virtsql“ trägt, müssen Sie ein Zertifikat für virtsql.*\<Ihr_Unternehmen>*.com auf beiden Knoten installieren. Sie können den Wert der Option **ForceEncryption**auf **Yes**.  

> [!NOTE]
> Wenn Sie eine verschlüsselte Verbindung für einen Azure Search-Indexer zu SQL Server auf einer Azure-VM erstellen wollen, finden Sie weitere Informationen unter [Konfigurieren einer Verbindung eines Azure Search-Indexers mit SQL Server auf einer Azure-VM](https://azure.microsoft.com/documentation/articles/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers/). 
  
 
##  <a name="Provision"></a> So stellen Sie ein Zertifikat auf dem Server bereit bzw. installieren Sie ein Zertifikat  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**, geben Sie in das Feld **Öffnen** den Wert **MMC** ein, und klicken Sie dann auf **OK**.  
  
2.  Klicken Sie in der MMC-Konsole im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
3.  Klicken Sie im Dialogfeld **Snap-In hinzufügen/entfernen** auf **Hinzufügen**.  
  
4.  Klicken Sie im Dialogfeld **Eigenständiges Snap-In hinzufügen** auf **Zertifikate**, und klicken Sie dann auf **Hinzufügen**.  
  
5.  Klicken Sie im **Dialogfeld Zertifikate-Snap-In** auf **Computerkonto**, und klicken Sie dann auf **Fertig stellen**.  
  
6.  Klicken Sie im Dialogfeld **Eigenständiges Snap-In hinzufügen** auf **Schließen**.  
  
7.  Klicken Sie im Dialogfeld **Snap-In hinzufügen/entfernen** auf **OK**.  
  
8.  Erweitern Sie im Dialogfeld **Zertifikate-Snap-In** die Option **Zertifikate**, erweitern Sie **Eigene Zertifikate**, und klicken Sie dann mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie anschließend auf **Importieren**.  

9. Klicken Sie mit der rechten Maustaste auf das importierte Zertifikat, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Privatschlüssel verwalten**. Fügen Sie im Dialogfeld **Sicherheit** die Leseberechtigung für das Benutzerkonto hinzu, das vom SQL Server-Dienstkonto verwendet wird.  
  
10. Ergänzen Sie die Angaben im **Zertifikatimport-Assistenten**, um dem Computer ein Zertifikat hinzuzufügen, und schließen Sie dann die MMC-Konsole. Weitere Informationen zum Hinzufügen von Zertifikaten zu einem Computer finden Sie in der Windows-Dokumentation.  
  
##  <a name="Export"></a> So exportieren Sie das Serverzertifikat  
  
1.  Erweitern Sie im **Zertifikate** -Snap-In den Ordner **Zertifikate** / **Eigene Zertifikate** , klicken Sie mit der rechten Maustaste auf das **Zertifikat**, zeigen Sie auf **Alle Tasks**, und klicken Sie dann auf **Exportieren**.  
  
2.  Führen Sie den **Zertifikatexport-Assistenten**aus, und speichern Sie die Zertifikatsdatei in einem geeigneten Speicherort.  
  
##  <a name="ConfigureServerConnections"></a> So konfigurieren Sie den Server zum Annehmen verschlüsselter Verbindungen  
  
1.  Erweitern Sie im **SQL Server Configuration Manager** den Eintrag **SQL Server-Netzwerkkonfiguration**, klicken Sie mit der rechten Maustaste auf **Protokolle für** *\<Serverinstanz>*, und wählen Sie dann **Eigenschaften**.  
  
2.  Wählen Sie im Dialogfeld **Eigenschaften** von **Protokolle für** *\<Instanzname>* auf der Registerkarte **Zertifikat** das gewünschte Zertifikat aus der Dropdownliste für das Feld **Zertifikat** aus, und klicken Sie dann auf **OK**.  
  
3.  Aktivieren Sie auf der Registerkarte **Flags** im Feld **ForceEncryption** die Option **Ja**, und klicken Sie dann auf **OK** , um das Dialogfeld zu schließen.  
  
4.  Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst neu.  

### <a name="wildcard-certificates"></a>Platzhalterzertifikate  
Ab [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 unterstützen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Platzhalterzertifikate. Andere Clients unterstützen möglicherweise keine Platzhalterzertifikate. Weitere Informationen finden Sie in der Clientdokumentation. Platzhalterzertifikate können nicht mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ausgewählt werden. Sie müssen den Registrierungsschlüssel `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQLServer\SuperSocketNetLib` bearbeiten und den Fingerabdruck des Zertifikats ohne Leerraum zum Wert des **Zertifikats** hinzufügen, um ein Platzhalterzertifikat zu verwenden.  
> [!WARNING]  
> [!INCLUDE[ssnoteregistry_md](../../includes/ssnoteregistry_md.md)]  
  
##  <a name="ConfigureClientConnections"></a> So konfigurieren Sie den Client zum Anfordern verschlüsselter Verbindungen  
  
1.  Kopieren Sie entweder das Originalzertifikat oder die exportierte Zertifikatsdatei auf den Clientcomputer.  
  
2.  Installieren Sie auf dem Clientcomputer mithilfe des **Zertifikate** -Snap-Ins entweder das Stammzertifikat oder die exportierte Zertifikatsdatei.  
  
3.  Klicken Sie im Konsolenbereich mit der rechten Maustaste auf **SQL Server Native Client-Konfiguration**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf der Seite **Flags** im Feld **Protokollverschlüsselung erzwingen** auf **Ja**.  
  
##  <a name="EncryptConnection"></a> So verschlüsseln Sie eine Verbindung in SQL Server Management Studio  
  
1.  Klicken Sie auf der Symbolleiste des Objekt-Explorers auf **Verbinden**, und klicken Sie dann auf **Datenbankmodul**.  
  
2.  Vervollständigen Sie im Dialogfeld **Verbindung mit Server herstellen** die Verbindungseinstellungen, und klicken Sie dann auf **Optionen**.  
  
3.  Klicken Sie auf der Registerkarte **Verbindungseigenschaften** auf **Verbindung verschlüsseln**.  
  
## <a name="see-also"></a>Siehe auch

[TLS 1.2-Unterstützung für Microsoft SQL Server](https://support.microsoft.com/kb/3135244)  


