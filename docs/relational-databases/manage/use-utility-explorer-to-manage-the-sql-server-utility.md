---
title: Verwenden des Hilfsprogramm-Explorers zum Verwalten des SQL Server-Hilfsprogramms | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 74012c90-b42e-4171-b27a-9c30cf69ff98
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd65300d9d3c79ea0604d6ea83c1c9377b7982cc
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="use-utility-explorer-to-manage-the-sql-server-utility"></a>Verwenden des Hilfsprogramm-Explorers zum Verwalten des SQL Server-Hilfsprogramms
  Als Komponente von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]stellt der Hilfsprogramm-Explorer eine Verbindung mit [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanzen her, um im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm eine Strukturansicht aller Objekte bereitzustellen. Der Inhaltsbereich des Hilfsprogramm-Explorers bietet verschiedene Möglichkeiten zur Anzeige von Zusammenfassungsdaten und detaillierten Daten zum Status verwalteter Instanzen von SQL Server. Der Hilfsprogramm-Explorer stellt auch eine Benutzeroberfläche für die Anzeige und Verwaltung von Richtliniendefinitionen bereit. Die Funktionen des Hilfsprogramm-Explorers können sich je nach den Objekten im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm geringfügig unterscheiden; sie umfassen in der Regel jedoch die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm verwalteten Objekte, Daten und Richtlinien. Weitere Informationen finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
## <a name="create-utility-control-point"></a>Erstellen eines Steuerungspunkts für das Hilfsprogramm  
 Bevor Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm verwenden können, müssen Sie einen Steuerungspunkt für das Hilfsprogramm erstellen. Weitere Informationen finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md) oder [Erstellen eines Steuerungspunkts für das SQL Server-Hilfsprogramm &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
## <a name="enroll-an-instance-of-sql-server-or-a-data-tier-application-from-utility-explorer"></a>Registrieren einer SQL Server-Instanz oder Datenebenenanwendung im Hilfsprogramm-Explorer  
 Sie können eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] problemlos im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm registrieren. Klicken Sie im Hilfsprogramm-Explorer mit der rechten Maustaste auf den Knoten **Verwaltete Instanzen** , und klicken Sie dann auf **Verwaltete Instanz hinzufügen**. Führen Sie die Schritte im Assistenten aus, um den Vorgang abzuschließen. Weitere Informationen finden Sie unter [ Registrieren einer Instanz von SQL Server &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
 Um eine Datenebenenanwendung auf einer verwalteten Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm bereitzustellen, klicken Sie auf die Registerkarte **Objekt-Explorer**, erweitern den Knoten **Verwaltung** und klicken dann mit der rechten Maustaste auf **Datenebenenanwendungen**. Wählen Sie im Kontextmenü **Datenebenenanwendung bereitstellen**aus. Weitere Informationen finden Sie unter [Bereitstellen einer Datenebenenanwendung](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md).  
  
## <a name="viewing-utility-explorer"></a>Anzeigen des Hilfsprogramm-Explorers  
 Der Hilfsprogramm-Explorer wird in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] standardmäßig nicht angezeigt. Wenn auf der [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] -Benutzeroberfläche kein Hilfsprogramm-Explorer angezeigt wird, klicken Sie im Menü **Ansicht** auf **Hilfsprogramm-Explorer**. Um den Inhaltsbereich des Hilfsprogramm-Explorers anzuzeigen, klicken Sie im Menü **Ansicht** auf **Inhalt des Hilfsprogramm-Explorers**.  
  
## <a name="viewing-objects-in-utility-explorer"></a>Anzeigen von Objekten im Hilfsprogramm-Explorer  
 Der Navigationsbereich und der Inhaltsbereich des Hilfsprogramm-Explorers enthalten Daten, Objekte und Richtlinien, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm verwaltet werden. Geben Sie im Navigationsbereich die Informationen an, die im Dashboard und in den Blickpunkten angezeigt werden sollen, und verwenden Sie dann den Inhaltsbereich und die Detailregisterkarten, um auf die Daten und Richtlinieninformationen der vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm verwalteten Objekte zuzugreifen.  
  
### <a name="sql-server-utility-navigation-pane"></a>Navigationsbereich des SQL Server-Hilfsprogramms  
 Der Navigationsbereich des Hilfsprogramm-Explorers stellt eine Strukturansicht der Objekte im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm bereit und gruppiert sie nach Steuerungspunkten für das Hilfsprogramm. Um Ordner zu erweitern, klicken Sie auf das Pluszeichen (+), oder doppelklicken Sie auf den UCP-Namen im Navigationsbereich des Hilfsprogramm-Explorers. Klicken Sie mit der rechten Maustaste auf Ordner oder Objekte, um allgemeine Aufgaben auszuführen. Die Strukturansicht enthält die folgenden Knoten:  
  
-   Der Knoten der obersten Ebene in der Strukturansicht ist der Steuerungspunkt für das Hilfsprogramm (UCP). Der Knotenname setzt sich wie folgt zusammen: "Hilfsprogrammname" (Computername\UCP-Instanzname). Wenn noch kein UCP eingerichtet wurde, müssen Sie einen erstellen. Wenn Sie nicht mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm verbunden sind, müssen Sie eine Verbindung mit einem Hilfsprogramm herstellen. Weitere Informationen finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md). Klicken Sie in der Strukturansicht auf den UCP-Namen, um den Inhaltsbereich des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm-Explorers mit Daten in der Dashboardsicht aufzufüllen. Weitere Informationen finden Sie unter [ Dashboard des Hilfsprogramms &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/999eb741-4a60-43f6-ab37-2df7dce845c1).  
  
     Klicken Sie mit der rechten Maustaste auf den UCP-Knoten, um Daten im Dashboard zu aktualisieren.  
  
-   Klicken Sie auf den Knoten **Bereitgestellte Datenebenenanwendungen** in der Strukturansicht, um auf Listenansichtsdaten im Inhaltsbereich des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms zuzugreifen. Die Detailregisterkarten unten im Inhaltsbereichs stellen Daten für die CPU- und Speicherplatzauslastung bereit und ermöglichen den Zugriff auf Richtliniendefinitionen und Eigenschaftendetails einzelner Datenebenenanwendungen im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm. Weitere Informationen finden Sie unter [Details zu bereitgestellten Datenebenenanwendungen &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
     Klicken Sie mit der rechten Maustaste auf den Knoten **Bereitgestellte Datenebenenanwendungen** in der Strukturansicht, um auf Filtereinstellungen zuzugreifen oder Daten in der Listenansicht zu aktualisieren.  
  
-   Klicken Sie auf den Knoten **Verwaltete Instanzen** in der Strukturansicht, um auf Listenansichtsdaten im Inhaltsbereich des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms zuzugreifen. Die Detailregisterkarten am unteren Rand des Inhaltsbereichs stellen Daten zur CPU- und Speichervolumeauslastung bereit und ermöglichen den Zugriff auf Richtliniendefinitionen und Eigenschaftendetails einzelner verwalteter Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm. Weitere Informationen finden Sie unter [Details zu verwalteten Instanzen &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
     Klicken Sie mit der rechten Maustaste auf den Knoten **Verwaltete Instanzen** in der Strukturansicht, um dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hinzuzufügen, auf Filtereinstellungen zuzugreifen oder Daten in der Listenansicht zu aktualisieren.  
  
-   Klicken Sie in der Strukturansicht auf den Knoten **Hilfsprogrammverwaltung**, um auf globale Richtliniendefinitionen für alle verwalteten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen und bereitgestellte Datenebenenanwendungen im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm zuzugreifen. Auf diese Weise können Sie Informationen des UCP-Administrators anzeigen und auf Konfigurationseinstellungen für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-UMDW (Utility Management Data Warehouse) zugreifen. Weitere Informationen finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d). Mithilfe der Steuerelemente auf der Registerkarte **Richtlinie** können Sie außerdem die Empfindlichkeitseinstellung in Bezug auf Verstöße gegen Berichterstellungsrichtlinien ändern. Weitere Informationen finden Sie unter [ Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Klicken Sie mit der rechten Maustaste auf den Knoten **Hilfsprogrammverwaltung** in der Strukturansicht, um Daten im Inhaltsbereich zu aktualisieren.  
  
### <a name="sql-server-utility-dashboard"></a>Dashboard des SQL Server-Hilfsprogramms  
 Wenn Sie den UCP-Knoten in der Strukturansicht des Hilfsprogramm-Explorers auswählen, wird das Dashboard des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms im Bereich Inhalt des Hilfsprogramm-Explorers mit Daten aufgefüllt. Das Dashboard bietet auf einen Blick Statusinformationen zu allen verwalteten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen und Datenebenenanwendungen im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm sowie für Objekte, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramm verwaltet werden, Informationen zur Auslastung des Gesamtspeicherplatzes. Weitere Informationen finden Sie unter [ Dashboard des Hilfsprogramms &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/999eb741-4a60-43f6-ab37-2df7dce845c1). Weitere Informationen zum Registrieren oder Entfernen einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Registrieren einer Instanz von SQL Server &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md) oder [Bereitstellen einer Datenebenenanwendung](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md) oder [Entfernen einer Instanz von SQL Server aus dem SQL Server-Hilfsprogramm](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
### <a name="filtering-the-list-of-objects-in-utility-explorer-contents"></a>Filtern der Objektliste in "Inhalt des Hilfsprogramm-Explorers"  
 Wenn ein Knoten eine große Anzahl an Objekten enthält, ist es möglicherweise schwierig, das gesuchte Objekt zu finden. In diesen Fällen können Sie die Liste mithilfe der Filterfunktion des Hilfsprogramm-Explorers verkleinern. Angenommen, Sie möchten eine bestimmte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder nur Computer finden, deren Dateispeicherplatz unterausgelastet ist. Klicken Sie mit der rechten Maustaste auf den Ordner, den Sie filtern möchten, klicken Sie auf die Schaltfläche zum Filtern und dann auf **Filtereinstellungen** , um das Dialogfeld „Filtereinstellungen“ des Hilfsprogramm-Explorers zu öffnen. Sie können die Liste nach Namen, Computer-CPU, Instanz-CPU, Dateispeicherplatz, Volumespeicherplatz, Einstellungen zum Überschreiben von Richtlinien oder nach der zuletzt berichteten Zeit filtern. Die Spalten **Operator** und **Wert** stellen zusätzliche Filteroperatoren in einer Dropdownliste bereit.  
  
### <a name="starting-powershell"></a>Starten von PowerShell  
 Zum Starten einer PowerShell-Sitzung können Sie mit der rechten Maustaste auf den Großteil der Ordner und Objekte in der Struktur des Objekt-Explorers klicken und **PowerShell starten**auswählen. Hierdurch wird eine PowerShell-Sitzung mit aktivierter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Unterstützung gestartet. Gleichzeitig ist der Pfad auf den Speicherort des Objekts festgelegt, auf das Sie mit der rechten Maustaste im Objekt-Explorer geklickt haben. Sie können PowerShell-Befehle anschließend in einer interaktiven PowerShell-Umgebung eingeben. Weitere Informationen finden Sie unter [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md).  
  
 Powershell bietet zwar keine F1-Hilfe, verfügt jedoch über ein **Get-Help** -Cmdlet mit Informationen zur Verwendung von Powershell. Weitere Informationen zur Verwendung von Get-Help finden Sie unter [Aufrufen der SQL Server PowerShell-Hilfe](../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Konfigurieren von Integritätsrichtlinien &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)   
 [Objekt-Explorer](http://msdn.microsoft.com/library/469ea8e2-79b9-44c8-bb6f-f0e1c5dbf0f2)  
  
  
