---
title: Paket-Verwaltung (SSIS-Dienst) | Microsoft Docs
ms.custom: 
ms.date: 11/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.dtsserver.importpackage.f1
- sql13.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- SQL Server Integration Services packages, managing
- packages [Integration Services], managing
- Integration Services packages, managing
- storing packages
- Stored Packages folder
- current packages
- Running Packages folder
- status information [Integration Services]
- SSIS packages, managing
- storage [Integration Services]
- monitoring [Integration Services], packages
- Integration Services service, package management
- services [Integration Services], package management
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 51d6e32f04d470c7f4ddfc8d3c4b6d994e0bd764
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="package-management-ssis-service"></a>Paketverwaltung (SSIS-Dienst)
  Paketverwaltung enthält die Überwachung, Verwaltung, importieren und Exportieren von Paketen.  
 
 ## <a name="package-store"></a>-Paketspeicher  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]enthält zwei Ordner der obersten Ebene für den Zugriff auf Pakete: 
 - **Ausführen von Paketen** 
 - **Gespeicherte Pakete**

 Der Ordner **Ausgeführte Pakete** enthält eine Auflistung der Pakete, die derzeit auf dem Server ausgeführt werden. Im Ordner **Gespeicherte Pakete** sind die im Paketspeicher gespeicherten Pakete aufgelistet. Hierbei handelt es sich um die einzigen vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwalteten Pakete. Der Paketspeicher kann aus den msdb-Datenbank- und/oder den Dateisystemordnern bestehen, die in der Konfigurationsdatei des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts aufgelistet sind. In der Konfigurationsdatei sind die zu verwaltenden msdb- und Dateisystemordner angegeben. Sie können Pakete auch an anderen Stellen des Dateisystems speichern, die nicht vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwaltet werden.  
  
 Pakete, die Sie in Msdb zu speichern, werden in einer Tabelle mit dem Namen Sysssispackages gespeichert. Wenn Sie Pakete in Msdb speichern, können Sie sie in logischen Ordnern gruppieren. Mithilfe von logischen Ordnern können Sie die Pakete nach ihrem Zweck organisieren oder Filtern von Paketen in der Sysssispackages-Tabelle. Erstellen Sie neue logische Ordner in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Standardmäßig werden alle logischen Ordner, die Sie der msdb-Datenbank hinzufügen, automatisch in den Paketspeicher übernommen.  
  
 Die logischen Ordner, die Sie erstellen, werden als Zeilen in der Tabelle Sysssispackagefolders in ' msdb ' dargestellt. Die Spalten „folderid“ und „parentfolderid“ in der „sysssispackagefolders“-Tabelle definieren die Ordnerhierarchie. Die logischen Stammordner in ' msdb ' werden die Zeilen in Sysssispackagefolders mit null-Werten in der Spalte Parentfolderid. Weitere Informationen finden Sie unter [Sysssispackages &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/sysssispackages-transact-sql.md) und [Sysssispackagefolders (Transact-SQL &)](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md).  
  
 Wenn Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] öffnen und eine Verbindung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]herstellen, werden die msdb-Ordner, die vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwaltet werden, im Ordner „Gespeicherte Pakete“ aufgelistet. Wenn in der Konfigurationsdatei Stammdateisystemordner angegeben sind, werden im Ordner Gespeicherte Pakete auch die Pakete aufgelistet, die in diesen Ordnern sowie deren Unterordnern gespeichert sind.  
  
 Sie können Pakete in beliebigen Dateisystemordnern speichern. Diese werden jedoch nur dann in den Unterordnern des Ordners **Gespeicherte Pakete** aufgeführt, wenn die betreffenden Dateisystemordner der Liste der Ordner in der Konfigurationsdatei für den Paketspeicher hinzugefügt wurden. Weitere Informationen zur Konfigurationsdatei finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
 Der Ordner **Ausgeführte Pakete** enthält keine Unterordner und ist nicht erweiterbar.  
  
 Der Ordner **Gespeicherte Pakete** enthält standardmäßig zwei Ordner: **Dateisystem** und **MSDB**. Im Ordner **Dateisystem** sind die im Dateisystem gespeicherten Pakete aufgelistet. Der Speicherort dieser Dateien wird in der Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst angegeben. Der Standardordner ist der Paketordner, der sich in %Programme%\Microsoft SQL Server\100\DTS befindet. Der Ordner **MSDB** enthält eine Liste der in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -msdb-Datenbank auf dem Server gespeicherten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Pakete. Die „sysssispackages“-Tabelle enthält die in msdb gespeicherten Pakete.  
  
 Zum Anzeigen der Liste der Pakete im Paketspeicher müssen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] öffnen und eine Verbindung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]herstellen.  
  
## <a name="monitor-running-packages"></a>Ausgeführte Pakete überwachen  
 Die **ausgeführte Pakete** Ordner werden derzeit ausgeführte Pakete aufgelistet. Wenn Sie Informationen zu den aktuellen Paketen auf der Seite **Zusammenfassung** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen möchten, klicken Sie auf den Ordner **Ausgeführte Pakete** . Informationen wie die Ausführungsdauer der ausgeführten Pakete werden auf der Seite **Zusammenfassung** angezeigt. Sie können den Ordner aktualisieren, um die aktuellsten Informationen anzuzeigen.  
  
 Wenn Sie Informationen zu einem einzelnen ausgeführten Paket auf der Seite **Zusammenfassung** anzeigen möchten, klicken Sie auf das Paket. Auf der Seite **Zusammenfassung** werden Informationen wie die Version und die Beschreibung des Pakets angezeigt.  
  
Beenden eines ausgeführtes Pakets aus der **ausgeführte Pakete** Ordner mit der rechten Maustaste auf das Paket, und klicken Sie dann auf **beenden**.  
  
## <a name="view-packages-in-ssms"></a>Anzeigen von Paketen in SSMS
    
 In diesem Verfahren wird beschrieben, wie eine Verbindung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] hergestellt und eine Liste der vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst verwalteten Pakete angezeigt wird.  
  
### <a name="to-connect-to-integration-services"></a>So stellen Sie eine Verbindung mit Integration Services her  
  
1.  Klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**, zeigen Sie auf **Microsoft SQL Server**, und klicken Sie dann auf **SQL Server Management Studio**.  
  
2.  Wählen Sie im Dialogfeld **Verbindung mit Server herstellen** in der Liste **Servertyp** die Option **Integration Services** aus, geben Sie im Feld **Servername** einen Servernamen an, und klicken Sie dann auf **Verbinden**.  
  
    > [!IMPORTANT]  
    >  Wenn Sie keine Verbindung mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]herstellen können, wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst wahrscheinlich nicht ausgeführt. Wenn Sie weitere Informationen zum Status des Diensts erhalten möchten, klicken Sie auf **Start**, zeigen Sie auf **Alle Programme**, zeigen Sie auf **Microsoft SQL Server**, zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**. Klicken Sie im linken Bereich auf **SQL Server-Dienste**. Suchen Sie im rechten Bereich den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst. Starten Sie den Dienst, wenn er nicht bereits ausgeführt wird.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]wird geöffnet. Standardmäßig ist das Fenster des Objekt-Explorers geöffnet und in der unteren linken Ecke des Studios positioniert. Ist der Objekt-Explorer nicht geöffnet, klicken Sie im Menü **Ansicht** auf **Objekt-Explorer** .  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>So zeigen Sie die vom Integration Services-Dienst verwalteten Pakete an  
  
1.  Erweitern Sie im Objekt-Explorer den Ordner Gespeicherte Pakete.  
  
2.  Erweitern Sie die Unterordner Gespeicherte Pakete, um die Pakete anzuzeigen.  

## <a name="import-and-export-packages"></a>Importieren und Exportieren von Paketen
 
 Pakete können in der sysssispackages-Tabelle in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-msdb-Datenbank oder im Dateisystem gespeichert werden.  
  
 Der Paketspeicher, bei dem es sich um den logischen Speicherort handelt, der vom [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst überwacht und verwaltet wird, kann sowohl die msdb-Datenbank als auch die in der Konfigurationsdatei für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst angegebenen Dateisystemordner einschließen.  
  
 Sie können Pakete zwischen den folgenden Speichertypen importieren und exportieren:  
  
-   Dateisystemordner überall im Dateisystem.  
  
-   Ordner im SSIS-Paketspeicher. Die beiden Standardordner heißen File System und MSDM.  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-msdb-Datenbank.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]bietet Ihnen die Möglichkeit zu importieren und Exportieren von Paketen und von Paketen das Speicherformat und den Speicherort der Pakete ändern. Mit den Import- und Export-Features können Sie Pakete zum Dateisystem, zum Paketspeicher oder zur msdb-Datenbank hinzufügen und Pakete aus einem Speicherformat in ein anderes Format kopieren. So können z.B. in msdb gespeicherte Pakete in das Dateisystem kopiert werden und umgekehrt.  
  
 Zum Kopieren eines Pakets in ein anderes Format können Sie auch das Eingabeaufforderungs-Hilfsprogramm **dtutil** („dtutil.exe“) verwenden. Weitere Informationen finden Sie unter [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
 Sie können ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket aus folgenden Speicherorten importieren bzw. in folgende Speicherorte exportieren:  
  
-   Sie können ein Paket importieren, das in einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], im Dateisystem oder im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher gespeichert ist. Das importierte Pakete wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder in einem Ordner im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher gespeichert.  
  
-   Sie können ein Paket exportieren, das in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], im Dateisystem oder im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher in einem anderen Speicherformat und an einem anderen Speicherort gespeichert ist.  
  
 Es gibt jedoch einige Einschränkungen im Hinblick auf das Importieren und Exportieren eines Pakets zwischen verschiedenen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   In einer Instanz von [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]können Sie Pakete von einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Instanz importieren, Sie können jedoch keine Pakete in eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Instanz exportieren.  
  
-   In einer Instanz von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]können Sie keine Pakete von einer [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-Instanz importieren bzw. dorthin exportieren.  
  
 Die folgenden Schritte beschreiben, wie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwendet wird, um ein Paket zu importieren oder zu exportieren.  
  
### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>So importieren Sie ein Paket mit SQL Server Management Studio  
  
1.  Klicken Sie auf **Start**, zeigen Sie auf **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und klicken Sie dann auf **SQL Server Management Studio**.  
  
2.  Legen Sie im Dialogfeld **Verbindung mit Server herstellen** die folgenden Optionen fest:  
  
    -   Wählen Sie im Feld **Servertyp** die Option **Integration Services**aus.  
  
    -   In der **Servernamen** Feld, geben Sie einen Servernamen ein, oder klicken Sie auf  **\<Suche fortsetzen… >** und suchen Sie den zu verwendenden Server.  
  
3.  Wenn der Objekt-Explorer nicht geöffnet ist, klicken Sie im Menü **Ansicht** auf **Objekt-Explorer**.  
  
4.  Erweitern Sie im Objekt-Explorer den Ordner **Gespeicherte Pakete** .  
  
5.  Erweitern Sie die Unterordner, um den Ordner zu suchen, in den Sie ein Paket importieren möchten.  
  
6.  Klicken Sie mit der rechten Maustaste auf den Ordner, und wählen Sie **Paket importieren**aus. Führen Sie dann eine der folgenden Aktionen aus:  
  
    -   Zum Importieren aus einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wählen Sie die Option **SQL Server** aus, geben Sie den Server an, und wählen Sie den Authentifizierungsmodus aus. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung auswählen, geben Sie einen Benutzernamen und ein Kennwort ein.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, wählen Sie das zu importierende Paket aus, und klicken Sie auf **OK**.  
  
    -   Zum Importieren aus dem Dateisystem wählen Sie die Option **Dateisystem** aus.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, wählen Sie das zu importierende Paket aus, und klicken Sie auf **Öffnen**.  
  
    -   Zum Importieren aus dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher wählen Sie die Option **SSIS-Paketspeicher** aus, und geben Sie den Server an.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, wählen Sie das zu importierende Paket aus, und klicken Sie auf **OK**.  
  
7.  Aktualisieren Sie optional den Paketnamen.  
  
8.  Zum Aktualisieren der Schutzebene des Pakets klicken Sie auf die Schaltfläche mit den drei Punkten **(…)** , und wählen Sie im Dialogfeld **Paketschutzebene** eine andere Schutzebene aus. Falls die Option **Sensible Daten mit einem Kennwort verschlüsseln** oder **Alle Daten mit einem Kennwort verschlüsseln** ausgewählt ist, geben Sie ein Kennwort ein, und bestätigen Sie es.  
  
9. Klicken Sie auf **OK** , um den Import abzuschließen.  
  
### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>So exportieren Sie ein Paket mit SQL Server Management Studio  
  
1.  Klicken Sie auf **Start**, zeigen Sie auf **Microsoft** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und klicken Sie dann auf **SQL Server Management Studio**.  
  
2.  Legen Sie im Dialogfeld **Verbindung mit Server herstellen** die folgenden Optionen fest:  
  
    -   Wählen Sie im Feld **Servertyp** die Option **Integration Services**aus.  
  
    -   In der **Servernamen** Feld, geben Sie einen Servernamen ein, oder klicken Sie auf  **\<Suche fortsetzen… >** und suchen Sie den zu verwendenden Server.  
  
3.  Wenn der Objekt-Explorer nicht geöffnet ist, klicken Sie im Menü **Ansicht** auf **Objekt-Explorer**.  
  
4.  Erweitern Sie im Objekt-Explorer den Ordner **Gespeicherte Pakete** .  
  
5.  Erweitern Sie die Unterordner, um das Paket zu suchen, das Sie exportieren möchten.  
  
6.  Klicken Sie mit der rechten Maustaste auf das Paket, klicken Sie auf **Exportieren**, und führen Sie eine der folgenden Aktionen aus:  
  
    -   Zum Exportieren einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wählen Sie die Option **SQL Server** aus, geben Sie den Server an, und wählen Sie den Authentifizierungsmodus aus. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung auswählen, geben Sie einen Benutzernamen und ein Kennwort ein.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, und erweitern Sie den Ordner **SSIS-Pakete** , um den Ordner zu suchen, in dem Sie das Paket speichern möchten. Aktualisieren Sie optional den Standardnamen des Pakets, und klicken Sie dann auf **OK**.  
  
    -   Zum Exportieren in das Dateisystem wählen Sie die Option **Dateisystem** aus.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)** , um den Ordner zu suchen, in den Sie das Paket exportieren möchten, geben Sie den Namen der Paketdatei ein, und klicken Sie dann auf **Speichern**.  
  
    -   Zum Exportieren in den [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher wählen Sie die Option **SSIS-Paketspeicher** aus, und geben Sie den Server an.  
  
         Klicken Sie auf die Schaltfläche mit den drei Punkten **(…)**, erweitern Sie den Ordner **SSIS-Pakete** , und wählen Sie den Ordner aus, in dem Sie das Paket speichern möchten. Geben Sie optional in das Textfeld **Paketname** einen neuen Namen für das Paket ein. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Zum Aktualisieren der Schutzebene des Pakets klicken Sie auf die Schaltfläche mit den drei Punkten **(…)** , und wählen Sie im Dialogfeld **Paketschutzebene** eine andere Schutzebene aus. Falls die Option **Sensible Daten mit einem Kennwort verschlüsseln** oder **Alle Daten mit einem Kennwort verschlüsseln** ausgewählt ist, geben Sie ein Kennwort ein, und bestätigen Sie es.  
  
8.  Klicken Sie auf **OK** , um den Export abzuschließen.  

## <a name="import-package-dialog-box-ui-reference"></a>Referenz zur Benutzeroberfläche für Dialogfeld "Paket importieren"
  Verwenden Sie das in **verfügbare Dialogfeld** Paket importieren [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], um ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket zu importieren und die Schutzebene des Pakets festzulegen oder zu ändern.  
  
### <a name="options"></a>enthalten  
 **Paketspeicherort**  
 Wählen Sie den Typ des Speicherortes, an den das Paket importiert werden soll. Die folgenden Optionen stehen zur Verfügung:  
  
 **SQL Server**  
  
 **Dateisystem**  
  
 **SSIS-Paketspeicher**  
  
 **Server**  
 Geben Sie einen Servernamen ein, oder wählen Sie einen Server aus der Liste aus.  
  
 **Authentifizierung**  
 Wählen Sie die Windows-Authentifizierung oder die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung aus. Diese Option ist nur verfügbar, wenn der Speicherort [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist.  
  
> [!IMPORTANT]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung.  
  
 **Authentifizierungstyp**  
 Wählen Sie einen Authentifizierungstyp aus.  
  
 **Benutzername**  
 Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden, stellen Sie einen Benutzernamen bereit.  
  
 **Kennwort**  
 Geben Sie ein Kennwort an, falls Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden.  
  
 **Paketpfad**  
 Geben Sie den Paketpfad ein, oder klicken Sie auf die Schaltfläche „Durchsuchen“ **(…)** , und suchen Sie das Paket.  
  
 **Paketname**  
 Sie können das Paket auch umbenennen. Der Standardname ist der Name des zu importierenden Pakets.  
  
 **Schutzebene**  
 Klicken Sie auf die Schaltfläche „Durchsuchen“ **(…)** , und aktualisieren Sie im Dialogfeld **Paketschutzebene** die Schutzebene. Weitere Informationen finden Sie unter [Dialogfeld „Paket- und Projektschutzebene“](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog).  

## <a name="export-package-dialog-box-ui-reference"></a>Referenz zur Benutzeroberfläche des Dialogfelds Paket exportieren
  Verwenden Sie das in **verfügbare Dialogfeld** Paket exportieren [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], um ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket an einen anderen Speicherort zu exportieren und optional die Schutzebene zu ändern.  
  
### <a name="options"></a>enthalten  
 **Paketspeicherort**  
 Wählen Sie den Speichertyp aus, in den das Paket exportiert werden soll. Die folgenden Optionen stehen zur Verfügung:  
  
 **SQL Server**  
  
 **Dateisystem**  
  
 **SSIS-Paketspeicher**  
  
 **Server**  
 Geben Sie einen Servernamen ein, oder wählen Sie einen Server aus der Liste aus.  
  
 **Authentifizierung**  
 Wählen Sie die Windows-Authentifizierung oder die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung aus. Diese Option ist nur verfügbar, wenn der Speicherort [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist.  
  
> [!IMPORTANT]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung.  
  
 **Authentifizierungstyp**  
 Wählen Sie einen Authentifizierungstyp aus.  
  
 **Benutzername**  
 Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden, stellen Sie einen Benutzernamen bereit.  
  
 **Kennwort**  
 Geben Sie ein Kennwort an, falls Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden.  
  
 **Paketpfad**  
 Geben Sie den Paketpfad ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen **(...)** , um nach dem Ordner zu suchen, in dem das Paket gespeichert werden soll.  
  
 **Schutzebene**  
 Klicken Sie auf die Schaltfläche zum Durchsuchen **(...)** , und aktualisieren Sie im Dialogfeld **Paketschutzebene** die Schutzebene. Weitere Informationen finden Sie unter [Dialogfeld „Paket- und Projektschutzebene“](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog).  

## <a name="back-up-and-restore-packages"></a>Sichern und Wiederherstellen von Paketen
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete können im Dateisystem oder in „msdb“, einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemdatenbank, gespeichert werden. In „msdb“ gespeicherte Pakete können mit den Sicherungs- und Wiederherstellungsfunktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gesichert und wiederhergestellt werden.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Sichern und Wiederherstellen der msdb-Datenbank zu erhalten:  
  
-   [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [Sichern und Wiederherstellen von Systemdatenbanken &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält das Eingabeaufforderungs-Hilfsprogramm **dtutil** (dtutil.exec), das Sie zum Verwalten von Paketen verwenden können. Weitere Informationen finden Sie unter [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### <a name="configuration-files"></a>Konfigurationsdateien  
 Alle im Paket enthaltenen Konfigurationsdateien werden im Dateisystem gespeichert. Diese Dateien werden nicht gesichert, wenn Sie die msdb-Datenbank sichern. Deshalb müssen Sie sicherstellen, dass die Konfigurationsdateien regelmäßig im Rahmen Ihres Plans zur Sicherung von in „msdb“ gespeicherten Paketen gesichert werden. Um Konfigurationen in das Sichern der msdb-Datenbank einzubeziehen, sollten Sie erwägen, anstelle von dateibasierten Konfigurationen den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurationstyp zu verwenden.  
  
### <a name="packages-stored-in-the-file-system"></a>Im Dateisystem gespeicherte Pakete  
 Die im Dateisystem gespeicherte Sicherung von Paketen sollte in den Sicherungsplan einbezogen werden, mit dem das Dateisystem des Servers gesichert wird. Die Konfigurationsdatei des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts, deren Standardname MsDtsSrvr.ini.xml lautet, enthält eine Aufstellung der Ordner auf dem Server, die vom Dienst überwacht werden. Sie sollten sicherstellen, dass diese Ordner gesichert werden. Außerdem können Pakete in anderen Ordnern auf dem Server gespeichert werden. Sie sollten sicherstellen, dass diese Ordner in den Sicherungsprozess einbezogen werden.  

## <a name="see-also"></a>Siehe auch  
 [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  

