---
title: "Start the SQL Server Import and Export Wizard | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server-Import/Export-Assistent"
  - "Starten des SQL Server-Import/Export-Assistenten"
  - "Import/Export-Assistent"
  - "Starten des Import/Export-Assistenten"
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: 130
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 112
---
# Start the SQL Server Import and Export Wizard
Sie können den Import-/Export-Assistenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit einer der folgenden Methoden starten.
-   Von [Startmenü](#startStart) oder [Befehlszeile](#startCmd) aus, um aus allen unterstützten Datenquellen zu importieren oder dorthin zu exportieren.
-   Von [SQL Server Management Studio (SSMS)](#startSSMS) aus, wenn Sie zu SQL Server importieren oder von dort exportieren.
-   Von [Visual Studio mit SQL Server Data Tools (SSDT)](#startVS) aus, wenn Sie ein SQL Server Integration Services-Projekt geöffnet haben.

In diesem Thema wird nur beschrieben, wie Sie den Assistenten **starten**.
-   Wenn Sie eine Übersicht über den Assistenten suchen, lesen Sie [Importieren und Exportieren von für SQL Server unterstützten Datenquellen](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).
-   Wenn Sie Informationen zu den Schritten im Assistenten suchen, wählen Sie die gewünschte Seite im Inhaltsnavigationsmenü aus. Es ist eine eigene Dokumentationsseite für jede Seite des Assistenten. Drücken Sie alternativ auf einer beliebigen Seite oder in einem beliebigen Dialogfeld des Assistenten auf F1, um die Dokumentation für die aktuelle Seite anzuzeigen.

**So erhalten Sie den Wizard.** Wenn Sie den Assistenten ausführen möchten, [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aber nicht auf Ihrem Computer installiert ist, können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistenten mit den SQL Server Data Tools (SSDT) installieren. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).  

## <a name="a-namestartstarta-start-the-wizard-from-the-start-menu"></a><a name="startStart"></a> Starten des Assistenten über das Startmenü  
1.  Klicken Sie im Menü **Start** auf **Alle Apps**.
2.  Suchen und erweitern Sie **Microsoft SQL Server 2016**.
3.  Klicken Sie auf eine der folgenden Optionen:
  
    -   **SQL Server 2016-Datenimport und -export (64 Bit)**
          
    -   **SQL Server 2016-Datenimport und -export (32 Bit)**  
  
Führen Sie die 64-Bit-Version des Assistenten aus, sofern für die Datenquelle kein 32-Bit-Datenanbieter erforderlich ist.
 
![Starten des Assistenten über das Startmenü](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="a-namestartcmda-start-the-wizard-from-the-command-prompt"></a><a name="startCmd"></a> Starten des Assistenten über die Eingabeaufforderung  
Führen Sie in einem Eingabeaufforderungsfenster **DTSWizard.exe** von einem der folgenden Speicherorte aus.  
  
-   **C:\Programme\Microsoft SQL Server\130\DTS\Binn** bei einer 64-Bit-Version.  
  
-   **C:\Programme (x86)\Microsoft SQL Server\130\DTS\Binn** bei einer 32-Bit-Version.  
  
Führen Sie die 64-Bit-Version des Assistenten aus, sofern für die Datenquelle kein 32-Bit-Datenanbieter erforderlich ist.

![Starten des Assistenten über cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="a-namestartssmsa-start-the-wizard-from-sql-server-management-studio-ssms"></a><a name="startSSMS"></a> Starten des Assistenten in SQL Server Management Studio (SSMS)  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] her.
2.  Erweitern Sie **Datenbanken**.
3.  Klicken Sie mit der rechten Maustaste auf eine Datenbank.
4.  Zeigen Sie auf **Aufgaben**.
5.  Klicken Sie auf eine der folgenden Optionen:
  
    -   **Daten importieren**
      
    -   **Daten exportieren**  

![Starten des Assistenten in SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

Wenn Sie SQL Server nicht installiert haben, bzw. SQL Server installiert haben, jedoch nicht SQL Server Management Studio, lesen Sie [Herunterladen von SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).
    
## <a name="a-namestartvsa-start-the-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a><a name="startVS"></a> Starten des Assistenten aus Visual Studio mit SQL Server Data Tools (SSDT)  
 Führen Sie in Visual Studio mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mit einem geöffneten Integration Services-Projekt eine der folgenden Aktionen aus.  
  
-   Klicken Sie im Menü **Projekt** auf **SSIS-Import/Export-Assistent**. 

    ![Starten des Assistenten aus einem Projekt](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- Oder –
    
-   Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner **SSIS-Pakete**, und klicken Sie dann auf **SSIS-Import/Export-Assistent**.

    ![Starten des Assistenten aus Paketen](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Wenn Sie Visual Studio nicht installiert haben, bzw. Visual Studio installiert haben, jedoch nicht SQL Server Data Tools, lesen Sie [Herunterladen von SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx). 

## <a name="get-help-while-the-wizard-is-running"></a>Aufrufen der Hilfe während der Ausführung des Assistent
> [!TIP] Drücken Sie auf einer beliebigen Seite oder in einem beliebigen Dialogfeld des Assistenten F1, um die Dokumentation für die aktuelle Seite anzuzeigen.   

 ## <a name="whats-next"></a>Wie geht es weiter?  
 Beim Starten des Assistenten ist die erste Seite **Willkommen beim SQL Server-Import/Export-Assistenten**. Sie müssen auf dieser Seite keine Aktionen durchführen. Weitere Informationen finden Sie unter [Willkommen beim SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
  