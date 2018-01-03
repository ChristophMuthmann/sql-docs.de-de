---
title: Speichern von Paketen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.savecopyas.f1
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
caps.latest.revision: "48"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e81823e1a6af46813b8d8df969d7a2060d1c1b17
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="save-packages"></a>Speichern von Paketen
  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] erstellen Sie Pakete mithilfe des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers und speichern diese als XML-Dateien (DTSX-Dateien) im Dateisystem. Sie können auch Kopien der Paket-XML-Datei in der msdb-Datenbank in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oder im Paketspeicher speichern. Der Paketspeicher stellt die Ordner im Dateisystempfad dar, die von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] verwaltet werden.  
  
 Wenn Sie ein Paket im Dateisystem speichern, können Sie es später mit [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nach [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bzw. in den Paketspeicher importieren. Weitere Informationen finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../integration-services/service/integration-services-service-ssis-service.md).  
  
 Darüber hinaus können Sie mit dem Eingabeaufforderungs-Hilfsprogramm **dtutil**ein Paket zwischen dem Dateisystem und msdb kopieren. Weitere Informationen finden Sie unter [dtutil Utility](../integration-services/dtutil-utility.md).  
## <a name="save-a-package-to-the-file-system"></a>Speichern eines Pakets im Dateisystem  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, das Sie als Datei speichern möchten.  
  
2.  Klicken Sie im Projektmappen-Explorer auf das Paket, das Sie speichern möchten.  
  
3.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern**.  
  
    > [!NOTE]  
    >  Sie können den Pfad und den Dateinamen des gespeicherten Pakets im Eigenschaftenfenster überprüfen.  

## <a name="save-a-copy-of-a-package"></a>Speichern einer Kopie eines Pakets
  In diesem Verfahren wird beschrieben, wie Sie eine Kopie eines Pakets im Dateisystem, im Paketspeicher oder in der **msdb**-Datenbank in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] speichern. Wenn Sie einen Speicherort zum Speichern der Paketkopie angeben, können Sie auch den Namen des Pakets aktualisieren.  
  
 Der Paketspeicher kann sowohl die **msdb** -Datenbank als auch die Ordner im Dateisystem, nur **msdb**oder nur Ordner im Dateisystem einschließen. In **msdb**werden Pakete in der **sysssispackages** -Tabelle gespeichert. Diese Tabelle schließt eine **folderid** -Spalte ein, die den logischen Ordner identifiziert, zu dem das Paket gehört. Logische Ordner bieten eine gute Möglichkeit, gespeicherter Pakete in **msdb** auf die gleiche Weise zu gruppieren, in der Ordner im Dateisystem das Gruppieren von im Dateisystem gespeicherten Paketen ermöglichen. Zeilen in der **sysssispackagefolders** -Tabelle in **msdb** definieren die Ordner.  
  
 Wenn **msdb** nicht als Teil des Paketspeichers definiert ist, können Sie Pakete weiterhin vorhandenen logischen Ordnern zuordnen, wenn Sie SQL Server in der Option **Paketpfad** auswählen.  
  
> [!NOTE]  
>  Das Paket muss im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer geöffnet sein, damit Sie eine Kopie des Pakets speichern können.  
  
### <a name="to-save-a-copy-of-a-package"></a>So speichern Sie eine Kopie eines Pakets  
  
1.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, von dem Sie eine Kopie speichern möchten.  
  
2.  Klicken Sie im Menü **Datei** auf **Kopie von \<Paketdatei> speichern unter**.  
  
3.  Wählen Sie im Dialogfeld **Kopie des Pakets speichern** in der Liste **Paketspeicherort** einen Paketspeicherort aus. Die folgenden Optionen stehen zur Verfügung:  
    -   SQL Server
    -   Dateisystem 
    -   SSIS-Paketspeicher 
  
4.  Falls der Speicherort **SQL Server** oder **SSIS-Paketspeicher**ist, stellen Sie einen Servernamen bereit.  
  
5.  Wenn Sie in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]speichern, geben Sie den Authentifizierungstyp an und, falls Sie die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung verwenden, einen Benutzernamen und ein Kennwort.  
  
6.  Geben Sie zum Angeben des Paketpfades entweder den Pfad ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen **(…)** , um den Speicherort des Pakets anzugeben. Der Standardname des Pakets lautet Paket. Optional können Sie den Paktnamen aktualisieren, sodass er Ihren Bedürfnissen entspricht.  
  
     Wenn Sie **SQL Server** in der Option **Paketpfad** auswählen, besteht der Paketpfad aus logischen Ordnern in **msdb** und dem Paketnamen. Ist z.B. das Paket DownloadMonthlyData dem Ordner Finance im Ordner MSDB (der Standardname des logischen Stammordners in **msdb**) zugeordnet, lautet der Paketpfad MSDB/Finance/DownloadMonthlyData für das Paket DownloadMonthlyData.  
  
     Wenn Sie **SSIS-Paketspeicher** in der Option **Paketpfad** auswählen, besteht der Paketpfad aus dem Ordner, der vom Integration Services-Dienst verwaltet wird. Befindet sich z. B. das Paket UpdateDeductions im Ordner HumanResources im Dateisystemordner, der von dem Dienst verwaltet wird, lautet der Paketpfad /File System/HumanResources/UpdateDeductions. Ist das Paket PostResumes dem Ordner HumanResources im Ordner MSDB zugeordnet, lautet der Paketpfad MSDB/HumanResources/PostResumes.  
  
     Wenn Sie **Dateisystem** in der Option **Paketpfad** auswählen, setzt sich der Paketpfad aus dem Speicherort im Dateisystem und dem Dateinamen zusammen. Ist z. B. der Paketname UpdateDemographics, lautet der Paketpfad C:\HumanResources\Quarterly\UpdateDemographics.dtsx.  
  
7.  Überprüfen Sie die Paketschutzebene.  
  
8.  Klicken Sie optional auf die Schaltfläche mit den drei Punkten **(…)** neben dem Feld **Schutzebene** , um die Schutzebene zu ändern.  
  
    -   Wählen Sie im Dialogfeld **Paketschutzebene** eine andere Schutzebene aus.  
  
    -   Klicken Sie auf **OK**.  
  
9. Klicken Sie auf **OK**.  

## <a name="save-a-package-as-a-package-template"></a>Speichern eines Pakets als Paketvorlage
 In diesem Thema wird beschrieben, wie Sie beim Erstellen neuer Integration Services-Pakete in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]benutzerdefinierte Pakete als Vorlagen festlegen und verwenden. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] verwendet standardmäßig eine Paketvorlage, die ein leeres Paket erstellt, wenn Sie einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt ein neues Paket hinzufügen. Sie können diese Standardvorlage nicht ersetzen. Es können jedoch neue Vorlagen hinzugefügt werden.  
  
 Sie haben die Möglichkeit, mehrere Pakete als Vorlagen festzulegen. Sie müssen zunächst benutzerdefinierte Pakete erstellen, bevor Sie diese als Vorlagen implementieren können.  
  
 Wenn Sie benutzerdefinierte Pakete als Vorlagen zum Erstellen von Paketen verwenden, haben die neuen Pakete denselben Namen und GUID wie die Vorlage. Sie sollten den Wert der **Name** -Eigenschaft aktualisieren und einen neuen GUID für die **ID** -Eigenschaft generieren, um die Pakete voneinander zu unterscheiden. Weitere Informationen finden Sie unter [Erstellen von Paketen in SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md) und [Festlegen von Paketeigenschaften](../integration-services/set-package-properties.md).  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>So legen Sie ein benutzerdefiniertes Paket als Paketvorlage fest  
  
1.  Suchen Sie im Dateisystem nach dem Paket, welches Sie als Vorlage verwenden möchten.  
  
2.  Kopieren Sie das Paket in den Ordner DataTransformationItems. Dieser Ordner befindet sich standardmäßig unter C:\Programme\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
3.  Wiederholen Sie die Schritte 1 und 2 für jedes als Vorlage zu verwendende Paket.  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>So verwenden Sie ein benutzerdefiniertes Paket als Paketvorlage  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt, in dem Sie ein Paket erstellen möchten.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, zeigen Sie auf **Hinzufügen**, und klicken Sie dann auf **Neues Element**.  
  
3.  Klicken Sie im Dialogfeld **Neues Element hinzufügen -\<Projektname>** auf das als Vorlage zu verwendende Paket.  
  
     Die Vorlagenliste enthält die Standardpaketvorlage mit der Bezeichnung Neues SSIS-Paket. Das Paketsymbol identifiziert die als Paketvorlage verwendbaren Vorlagen.  
  
4.  Klicken Sie auf **Hinzufügen**.  
