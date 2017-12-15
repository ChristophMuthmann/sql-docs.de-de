---
title: Starten des SQL Server-Import/Export-Assistenten | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Import and Export Wizard
- starting SQL Server Import and Export Wizard
- Import and Export Wizard
- starting Import and Export Wizard
ms.assetid: 5fc4f6d1-1f6f-444e-9aeb-827f85e1c405
caps.latest.revision: "130"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1c54f2e961abc3ec9bbbc3b19214e78d58208104
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="start-the-sql-server-import-and-export-wizard"></a>Starten des SQL Server-Import/Export-Assistenten

 > Inhalte im Zusammenhang mit früheren Versionen von SQL Server finden Sie unter [Run the SQL Server Import and Export Wizard (Ausführen des Import/Export-Assistenten von SQL Server)](https://msdn.microsoft.com/library/ms140052(SQL.120).aspx).

Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistenten mit einer der in diesem Thema beschriebenen Methoden zum Importieren von Daten aus und Exportieren von Daten in unterstützte Datenquellen.

> [!IMPORTANT]
> In diesem Thema wird nur beschrieben, wie Sie den Assistenten **starten** . Wenn Sie andere Themen interessieren, lesen Sie die Seite [Verwandte Tasks und Inhalte](#related).

So starten Sie den Assistenten
-   Von [Startmenü](#startStart).
-   Von [Befehlszeile](#startCmd). 
-   Von [SQL Server Management Studio (SSMS)](#startSSMS).
-   Von [Visual Studio mit SQL Server Data Tools (SSDT)](#startVS).

## <a name="prerequisite---is-the-wizard-installed-on-your-computer"></a>Voraussetzung: Installation des Assistenten auf dem Computer
Wenn Sie den Assistenten ausführen möchten, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aber nicht auf Ihrem Computer installiert ist, können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten mit den SQL Server Data Tools (SSDT) installieren. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

> [!NOTE]
> Sie müssen SQL Server installieren, um die 64-Bit-Version des SQL Server-Import/Export-Assistenten verwenden zu können. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen und installieren daher auch nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten.

## <a name="startStart"></a> Startmenü  
### <a name="start-the-sql-server-import-and-export-wizard-from-the-start-menu"></a>Starten des SQL Server-Import/Export-Assistenten über das Menü „Start“
1.  Suchen und erweitern Sie **Microsoft SQL Server 2016** im Menü **Start**.
3.  Klicken Sie auf eine der folgenden Optionen:
  
    -   **SQL Server 2016-Datenimport und -export (64 Bit)**
          
    -   **SQL Server 2016-Datenimport und -export (32 Bit)**  
  
    Führen Sie die 64-Bit-Version des Assistenten aus, sofern für die Datenquelle kein 32-Bit-Datenanbieter erforderlich ist.
 
    ![Starten des Assistenten über das Startmenü](../../integration-services/import-export-data/media/start-wizard-start.jpg)
  
## <a name="startCmd"></a> Command prompt
### <a name="start-the-sql-server-import-and-export-wizard-from-the-command-prompt"></a>Starten des SQL Server-Import/Export-Assistenten über die Eingabeaufforderung  
Führen Sie in einem Eingabeaufforderungsfenster **DTSWizard.exe** von einem der folgenden Speicherorte aus.  
  
-   **C:\Programme\Microsoft SQL Server\130\DTS\Binn** bei einer 64-Bit-Version.  
  
-   **C:\Programme (x86)\Microsoft SQL Server\130\DTS\Binn** bei einer 32-Bit-Version.  
  
Führen Sie die 64-Bit-Version des Assistenten aus, sofern für die Datenquelle kein 32-Bit-Datenanbieter erforderlich ist.

![Starten des Assistenten über cmd](../../integration-services/import-export-data/media/start-wizard-cmd.jpg)  
  
## <a name="startSSMS"></a> SQL Server Management Studio (SSMS)
### <a name="start-the-sql-server-import-and-export-wizard-from-sql-server-management-studio-ssms"></a>Starten des SQL Server-Import/Export-Assistenten in SQL Server Management Studio (SSMS)    
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.
    
2.  Erweitern Sie **Datenbanken**.
3.  Klicken Sie mit der rechten Maustaste auf eine Datenbank.
4.  Zeigen Sie auf **Aufgaben**.
5.  Klicken Sie auf eine der folgenden Optionen:
  
    -   **Daten importieren**
      
    -   **Daten exportieren**  

    ![Starten des Assistenten in SSMS](../../integration-services/import-export-data/media/start-wizard-ssms.jpg) 

Wenn Sie SQL Server nicht installiert haben, bzw. SQL Server installiert haben, jedoch nicht SQL Server Management Studio, lesen Sie [Herunterladen von SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md).
  
## <a name="startVS"></a> Visual Studio
### <a name="start-the-sql-server-import-and-export-wizard-from-visual-studio-with-sql-server-data-tools-ssdt"></a>Starten des SQL Server-Import/Export-Assistenten aus Visual Studio mit SQL Server Data Tools (SSDT) 
 Führen Sie in Visual Studio mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]mit einem geöffneten Integration Services-Projekt eine der folgenden Aktionen aus. 
  
-   Klicken Sie im Menü **Projekt** auf **SSIS-Import/Export-Assistent**. 

    ![Starten des Assistenten aus einem Projekt](../../integration-services/import-export-data/media/start-wizard-project.jpg) 
    
    \- Oder –
    
-   Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den Ordner **SSIS-Pakete** , und klicken Sie dann auf **SSIS-Import/Export-Assistent**.

    ![Starten des Assistenten aus Paketen](../../integration-services/import-export-data/media/start-wizard-packages.jpg)

Wenn Sie Visual Studio nicht installiert haben, bzw. Visual Studio installiert haben, jedoch nicht SQL Server Data Tools, lesen Sie [Herunterladen von SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="get-the-wizard"></a>Beziehen des Assistenten
Wenn Sie den Assistenten ausführen möchten, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aber nicht auf Ihrem Computer installiert ist, können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistenten mit den SQL Server Data Tools (SSDT) installieren. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="get-help-while-the-wizard-is-running"></a>Aufrufen der Hilfe während der Ausführung des Assistent
> [!TIP]
> Drücken Sie auf einer beliebigen Seite oder in einem beliebigen Dialogfeld des Assistenten F1, um die Dokumentation für die aktuelle Seite anzuzeigen.   

 ## <a name="whats-next"></a>Wie geht es weiter?  
 Beim Starten des Assistenten ist die erste Seite **Willkommen beim SQL Server-Import/Export-Assistenten**. Sie müssen auf dieser Seite keine Aktionen durchführen. Weitere Informationen finden Sie unter [Willkommen beim SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
## <a name="related"></a> Verwandte Tasks und Inhalte  
 Im Folgenden werden einige weitere grundlegenden Tasks aufgelistet.
-   **Sehen Sie sich ein kurzes Beispiel zur Funktionsweise des Assistenten an.**

    -   **Wenn Sie lieber mit Screenshots arbeiten:** Sehen Sie sich das folgende einfache vollständige Beispiel auf der Seite [Get started with this simple example of the Import and Export Wizard](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md) (Erste Schritte mit diesem einfachen Beispiel für den Import/Export-Assistenten) an.

    -   **Wenn Sie sich lieber ein Video ansehen möchten:** Sehen Sie sich dieses vierminütige YouTube-Video an, in dem der Assistent vorgestellt wird und klar und deutlich erklärt wird, wie Daten nach Excel exportiert werden können: [Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049) (Verwenden des SQL Server-Import/Export-Assistenten zum Exportieren nach Excel).

-   **Weitere Informationen zur Funktionsweise des Assistenten:**

    -   **Weitere Informationen zum Assistenten:** Wenn Sie eine Übersicht über den Assistenten suchen, lesen Sie [Importieren und Exportieren von für SQL Server unterstützten Datenquellen](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Weitere Informationen zu den Schritten des Assistenten:** Weitere Informationen zu den einzelnen Schritten des Assistenten finden Sie auf der Seite [Steps in the SQL Server Import and Export Wizard](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md) (Schritte im SQL Server-Import/Export-Assistenten). Es ist außerdem eine eigene Dokumentationsseite für jede Seite des Assistenten verfügbar.

    -   **Weitere Informationen zum Herstellen einer Verbindung zwischen Datenquellen und -zielen:** Um weitere Informationen zum Herstellen einer Verbindung mit Ihren Daten zu erhalten, wählen Sie aus der folgenden Liste die Seite aus, die Sie besonders interessiert: [Connect to data sources with the SQL Server Import and Export Wizard](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md) (Herstellen einer Verbindung mit Datenquellen mit dem SQL Server-Import/Export-Assistenten). Es sind separate Dokumentationsseiten für verschiedene, häufig verwendete Datenquellen verfügbar.


