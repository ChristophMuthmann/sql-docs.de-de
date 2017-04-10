---
title: "Import und Export von Paketen (SSIS-Dienst) | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Pakete [Integration Services], importieren"
  - "Pakete [Integration Services], exportieren"
  - "Importieren von Paketen"
  - "Exportieren von Paketen"
ms.assetid: ef18ec11-b536-47d9-abd1-794099f43486
caps.latest.revision: 51
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 51
---
# Import und Export von Paketen (SSIS-Dienst)
    
> **WICHTIG!** In diesem Thema wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst beschrieben, ein Windows-Dienst zur Verwaltung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] unterstützt den Dienst für die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie Objekte, z. B. Pakete, auf dem Integration Services-Server verwalten.  
  
 Pakete können in der sysssispackages-Tabelle in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-msdb-Datenbank oder im Dateisystem gespeichert werden.  
  
 Der Paketspeicher, bei dem es sich um den logischen Speicherort handelt, der vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst überwacht und verwaltet wird, kann sowohl die msdb-Datenbank als auch die in der Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst angegebenen Dateisystemordner einschließen.  
  
 Sie können Pakete zwischen den folgenden Speichertypen importieren und exportieren:  
  
-   Dateisystemordner überall im Dateisystem.  
  
-   Ordner im SSIS-Paketspeicher. Die beiden Standardordner heißen File System und MSDM.  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-msdb-Datenbank.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ermöglicht Ihnen das Importieren und Exportieren von Paketen. Damit können Sie das Speicherformat und den Speicherort der Pakete ändern. Mit den Import- und Export-Features können Sie Pakete zum Dateisystem, zum Paketspeicher oder zur msdb-Datenbank hinzufügen und Pakete aus einem Speicherformat in ein anderes Format kopieren. So können z.B. in msdb gespeicherte Pakete in das Dateisystem kopiert werden und umgekehrt.  
  
 Zum Kopieren eines Pakets in ein anderes Format können Sie auch das Eingabeaufforderungs-Hilfsprogramm **dtutil** („dtutil.exe“) verwenden. Weitere Informationen finden Sie unter [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
## So importieren oder exportieren Sie ein Paket  
  
> **WICHTIG!** In diesem Thema wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst erläutert, der Teil von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]ist. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] unterstützt den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst aus Gründen der Abwärtskompatibilität mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Informationen zum Verwalten von Paketen in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] finden Sie unter [Integration Services-Server &#40;SSIS&#41;](https://msdn.microsoft.com/library/ms141134.aspx).  
  
 Sie können ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket aus folgenden Speicherorten importieren bzw. in folgende Speicherorte exportieren:  
  
-   Sie können ein Paket importieren, das in einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], im Dateisystem oder im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher gespeichert ist. Das importierte Pakete wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder in einem Ordner im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher gespeichert.  
  
-   Sie können ein Paket exportieren, das in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], im Dateisystem oder im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher in einem anderen Speicherformat und an einem anderen Speicherort gespeichert ist.  
  
 Es gibt jedoch einige Einschränkungen im Hinblick auf das Importieren und Exportieren eines Pakets zwischen verschiedenen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   In einer Instanz von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]können Sie Pakete von einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Instanz importieren, Sie können jedoch keine Pakete in eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Instanz exportieren.  
  
-   In einer Instanz von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]können Sie keine Pakete von einer [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-Instanz importieren bzw. dorthin exportieren.  
  
 Die folgenden Schritte beschreiben, wie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwendet wird, um ein Paket zu importieren oder zu exportieren.  
  
#### So importieren Sie ein Paket mit SQL Server Management Studio  
  
1.  Klicken Sie auf **Start**, zeigen Sie auf **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und klicken Sie dann auf **SQL Server Management Studio**.  
  
2.  Legen Sie im Dialogfeld **Verbindung mit Server herstellen** die folgenden Optionen fest:  
  
    -   Wählen Sie im Feld **Servertyp** die Option **Integration Services**aus.  
  
    -   Geben Sie im Feld **Servername** einen Servernamen an, oder klicken Sie auf **<Suche fortsetzen>**, um nach dem zu verwendenden Server zu suchen.  
  
3.  Wenn der Objekt-Explorer nicht geöffnet ist, klicken Sie im Menü **Ansicht** auf **Objekt-Explorer**.  
  
4.  Erweitern Sie im Objekt-Explorer den Ordner **Gespeicherte Pakete** .  
  
5.  Erweitern Sie die Unterordner, um den Ordner zu suchen, in den Sie ein Paket importieren möchten.  
  
6.  Klicken Sie mit der rechten Maustaste auf den Ordner, und wählen Sie **Paket importieren** aus. Führen Sie dann eine der folgenden Aktionen aus:  
  
    -   Zum Importieren aus einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wählen Sie die Option **SQL Server** aus, geben Sie den Server an, und wählen Sie den Authentifizierungsmodus aus. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung auswählen, geben Sie einen Benutzernamen und ein Kennwort ein.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, wählen Sie das zu importierende Paket aus, und klicken Sie auf **OK**.  
  
    -   Zum Importieren aus dem Dateisystem wählen Sie die Option **Dateisystem** aus.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, wählen Sie das zu importierende Paket aus, und klicken Sie auf **Öffnen**.  
  
    -   Zum Importieren aus dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher wählen Sie die Option **SSIS-Paketspeicher** aus, und geben Sie den Server an.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, wählen Sie das zu importierende Paket aus, und klicken Sie auf **OK**.  
  
7.  Aktualisieren Sie optional den Paketnamen.  
  
8.  Zum Aktualisieren der Schutzebene des Pakets klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, und wählen Sie im Dialogfeld **Paketschutzebene** eine andere Schutzebene aus. Falls die Option **Sensible Daten mit einem Kennwort verschlüsseln** oder **Alle Daten mit einem Kennwort verschlüsseln** ausgewählt ist, geben Sie ein Kennwort ein, und bestätigen Sie es.  
  
9. Klicken Sie auf **OK** , um den Import abzuschließen.  
  
#### So exportieren Sie ein Paket mit SQL Server Management Studio  
  
1.  Klicken Sie auf **Start**, zeigen Sie auf **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und klicken Sie dann auf **SQL Server Management Studio**.  
  
2.  Legen Sie im Dialogfeld **Verbindung mit Server herstellen** die folgenden Optionen fest:  
  
    -   Wählen Sie im Feld **Servertyp** die Option **Integration Services**aus.  
  
    -   Geben Sie im Feld **Servername** einen Servernamen an, oder klicken Sie auf **<Suche fortsetzen>**, um nach dem zu verwendenden Server zu suchen.  
  
3.  Wenn der Objekt-Explorer nicht geöffnet ist, klicken Sie im Menü **Ansicht** auf **Objekt-Explorer**.  
  
4.  Erweitern Sie im Objekt-Explorer den Ordner **Gespeicherte Pakete** .  
  
5.  Erweitern Sie die Unterordner, um das Paket zu suchen, das Sie exportieren möchten.  
  
6.  Klicken Sie mit der rechten Maustaste auf das Paket, klicken Sie auf **Exportieren**, und führen Sie eine der folgenden Aktionen aus:  
  
    -   Zum Exportieren einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wählen Sie die Option **SQL Server** aus, geben Sie den Server an, und wählen Sie den Authentifizierungsmodus aus. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung auswählen, geben Sie einen Benutzernamen und ein Kennwort ein.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, und erweitern Sie den Ordner **SSIS-Pakete**, um den Ordner zu suchen, in dem Sie das Paket speichern möchten. Aktualisieren Sie optional den Standardnamen des Pakets, und klicken Sie dann auf **OK**.  
  
    -   Zum Exportieren in das Dateisystem wählen Sie die Option **Dateisystem** aus.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, um den Ordner zu suchen, in den Sie das Paket exportieren möchten, geben Sie den Namen der Paketdatei ein, und klicken Sie dann auf **Speichern**.  
  
    -   Zum Exportieren in den [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher wählen Sie die Option **SSIS-Paketspeicher** aus, und geben Sie den Server an.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, erweitern Sie den Ordner **SSIS-Pakete**, und wählen Sie den Ordner aus, in dem Sie das Paket speichern möchten. Geben Sie optional in das Textfeld **Paketname** einen neuen Namen für das Paket ein. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Zum Aktualisieren der Schutzebene des Pakets klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, und wählen Sie im Dialogfeld **Paketschutzebene** eine andere Schutzebene aus. Falls die Option **Sensible Daten mit einem Kennwort verschlüsseln** oder **Alle Daten mit einem Kennwort verschlüsseln** ausgewählt ist, geben Sie ein Kennwort ein, und bestätigen Sie es.  
  
8.  Klicken Sie auf **OK** , um den Export abzuschließen.  
  
## Siehe auch  
 [Paketverwaltung &#40;SSIS-Dienst&#41;](../../integration-services/service/package-management-ssis-service.md)  
  
  