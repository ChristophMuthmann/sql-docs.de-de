---
title: "Gewähren von serverweiten Administratorrechten für Analysis Services-Instanz | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administrator rights [Analysis Services]
- server-wide administrative permissions [Analysis Services]
ms.assetid: 20d1234b-a457-4a84-ae08-fe356870c466
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b7d564225ff95de938df836f1fd49b85892e8ba3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="grant-server-admin-rights-to-an--analysis-services-instance"></a>Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz
  Mitglieder der Serveradministratorrolle in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz haben uneingeschränkten Zugriff auf alle [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte und -Daten in dieser Instanz. Ein Benutzer muss Mitglied der Serveradministratorrolle sein, um serverweite Tasks wie z. B. Erstellen oder Verarbeiten einer Datenbank, das Ändern von Servereigenschaften oder das Starten einer Ablaufverfolgung (außer für Verarbeitungsereignisse) ausführen zu können.  
  
 Rollenmitgliedschaften werden bei der Installation von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eingerichtet. Der Benutzer, der das Setupprogramm ausführt, kann sich selbst oder andere Benutzer zu dieser Rolle hinzufügen. Sie müssen mindestens einen Administrator angeben, bevor Setup fortgesetzt werden kann.  
  
 Standardmäßig werden den Mitgliedern der lokalen Administratorgruppe ebenfalls Administratorrechte im Analysis-Server gewährt. Obwohl die lokale Gruppe keine explizit gewährte Mitgliedschaft in der Serveradministratorrolle von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ist, können lokale Administratoren Datenbanken erstellen, Benutzer und Berechtigungen hinzufügen und jede andere Aufgabe ausführen, zu deren Ausführung Systemadministratoren berechtigt sind. Die implizite Gewährung von Administratorberechtigungen ist konfigurierbar. Es wird von der Servereigenschaft **BuiltinAdminsAreServerAdmins** bestimmt, die standardmäßig auf **TRUE** festgelegt ist. Sie können diese Eigenschaft in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ändern. Weitere Informationen finden Sie unter [Sicherheitseigenschaften](../../analysis-services/server-properties/security-properties.md).  
  
 Nach der Installation können Sie die Rollenzugehörigkeiten ändern und alle weiteren Benutzer hinzufügen, die vollständige Rechte für den Dienst benötigen. Sie können Serverrollen auch mithilfe von Analysis Management Objects (AMOs) verwalten. Weitere Informationen finden Sie unter [Entwickeln mit Analysis Management Objects &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]stellt verschiedene Optionen mit zunehmend präziseren Rollen für die Verarbeitung und die Abfrage auf Server-, Datenbank- und Objektebene bereit. Weitere Anweisungen zur Verwendung dieser Rollen finden Sie unter [Rollen und Berechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md).  
  
## <a name="modify-server-role-membership"></a>Ändern der Serverrollenmitgliedschaft  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Instanznamen, und klicken Sie auf **Eigenschaften**.  
  
2.  Klicken Sie im Bereich **Seite auswählen** auf **Sicherheit** , und klicken Sie anschließend unten auf der Seite auf **Hinzufügen** , um der Serverrolle einen oder mehrere Windows-Benutzer bzw. Windows-Benutzergruppen hinzuzufügen.  
  
     ![Benutzer Dialogfelds "hinzufügen" in Management Studio](../../analysis-services/instances/media/ssas-serveradminadd.png "Benutzer Dialogfelds "hinzufügen" in Management Studio")  
  
### <a name="add-computer-accounts"></a>Hinzufügen von Computerkonten  
 Mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Sie auch ein Computerkonto zur [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Administratorengruppe hinzufügen.  
  
1.  Klicken Sie im Dialogfeld **Benutzer oder Gruppen auswählen** auf **Speicherorte**.  
  
2.  Wählen Sie die Domäne der Computer aus, die Sie hinzufügen möchten, oder wählen Sie **Gesamtes Verzeichnis** aus, und klicken Sie auf **OK**.  
  
3.  Klicken Sie auf **Objekttypen**.  
  
4.  Wählen Sie **Computer** aus, und klicken Sie auf **OK**.  
  
     ![Hinzufügen von Computerkonten als Administratoren von Ssas](../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "Hinzufügen von Computerkonten als Administratoren von Ssas")  
  
5.  Geben Sie im Textfeld **Geben Sie die Namen der auszuwählenden Objekte ein** den Namen des Computers ein, und klicken Sie auf **Namen überprüfen** , um zu überprüfen, ob sich das Computerkonto in den aktuellen Speicherorten befindet. Wenn das Computerkonto nicht gefunden wird, überprüfen Sie den Computernamen und die Domäne des Computers.  
  
## <a name="nt-servicessastelemetry-account"></a>Konto "NT Service\SSASTelemetry"  
 Das Konto**NT Service/SSASTelemetry** ist ein Computerkonto mit geringen Berechtigungen, das während des Setups erstellt wurde und ausschließlich zur Ausführung der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Implementierung des Diensts Customer Experience Improvement Program (CEIP; Programm zur Verbesserung der Benutzerfreundlichkeit) verwendet wird. Für die Ausführung verschiedener Ermittlungsbefehle erfordert dieser Dienst Administratorrechte für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz. Weitere Informationen finden Sie unter [Programm zur Verbesserung der Benutzerfreundlichkeit für SQL Server Data Tools](../../sql-server/customer-experience-improvement-program-for-sql-server-data-tools.md) und [Datenschutzbestimmungen für Microsoft SQL Server](http://msdn.microsoft.com/library/57769f4a-5689-49a1-8298-e3c0db5106f8) .  
  
## <a name="see-also"></a>Siehe auch  
 [Autorisieren des Zugriffs auf Objekte und Vorgänge &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [Sicherheitsrollen &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  
