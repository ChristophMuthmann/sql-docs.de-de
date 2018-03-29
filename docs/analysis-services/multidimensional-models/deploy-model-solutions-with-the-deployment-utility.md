---
title: Bereitstellen von Modelllösungen mit dem Bereitstellungshilfsprogramm | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deploying [Analysis Services], command prompt
- command prompt utilities [SQL Server], Microsoft.AnalysisServices.Deployment
- Microsoft.AnalysisServices.Deployment utility
- Analysis Services deployments, command prompt
ms.assetid: 584f78ac-5f18-41e0-b292-d1949ec05196
caps.latest.revision: ''
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 38e91da35dc590b3acbe0f49517e3fad891510fc
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-model-solutions-with-the-deployment-utility"></a>Bereitstellen von Modelllösungen mit dem Bereitstellungshilfsprogramm
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Mithilfe des Hilfsprogramms **Microsoft.AnalysisServices.Deployment** können Sie das Bereitstellungsmodul von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] von der Eingabeaufforderung aus starten. Als Eingabedatei verwendet das Hilfsprogramm die XML-Ausgabedateien, die beim Erstellen eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]generiert werden. Die Eingabedateien können problemlos geändert werden, um die Bereitstellung eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts anzupassen. Anschließend kann das generierte Bereitstellungsskript entweder sofort ausgeführt oder für eine spätere Bereitstellung gespeichert werden.  
  
> [!NOTE]
> Die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Assistenten/Bereitstellungshilfsprogramm wird mit installiert [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS). Achten Sie darauf, dass Sie die neueste Version verwenden. Standardmäßig ist die neueste Version des bereitstellungs-Assistenten C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio installiert. 

## <a name="syntax"></a>Syntax  
  
```  
  
Microsoft.AnalysisServices.Deployment [ASdatabasefile]   
    {[/s[:logfile]] | [/a] | [[/o[:output_script_file]] [/d]]}  
```  
  
##  <a name="Arguments"></a> Argumente  
 *ASdatabasefile*  
 Der vollständige Pfad des Ordners, in dem sich die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Bereitstellungsskriptdatei (.asdatabase) befindet. Diese Datei wird generiert, wenn Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]ein Projekt bereitstellen. Sie befindet sich im Projektpapierkorb. Die AS-Datenbankdatei enthält die bereitzustellenden Objektdefinitionen. Wird dieses Argument nicht angegeben, wird der aktuelle Ordner verwendet.  
  
 **/s**  
 Führt das Hilfsprogramm im unbeaufsichtigten Modus aus; Dialogfelder werden nicht angezeigt. Weitere Informationen zu den Ausführungsmodi finden Sie im Abschnitt [Modi](#Modes)weiter unten in diesem Thema.  
  
 *logfile*  
 Der vollständige Pfad und der Dateiname der Protokolldatei. Ablaufverfolgungsereignisse werden in der angegebenen Protokolldatei protokolliert. Wenn die Protokolldatei bereits vorhanden ist, wird der Inhalt der Datei ersetzt.  
  
 **/a**  
 Führt das Hilfsprogramm im Antwortmodus aus. Alle Antworten, die während des assistentenbasierten Teils des Hilfsprogramms angegeben werden, werden in die Eingabedateien geschrieben, es werden jedoch keine wirklichen Änderungen an den Bereitstellungszielen vorgenommen.  
  
 **/o**  
 Führt das Hilfsprogramm im Ausgabemodus aus. Es erfolgt keine Bereitstellung; das XMLA-Skript (XML for Analysis), das normalerweise an die Bereitstellungsziele gesendet würde, wird stattdessen in der angegebenen Ausgabeskriptdatei gespeichert. Wenn *output_script_file* nicht angegeben wird, versucht das Hilfsprogramm, die Ausgabeskriptdatei zu verwenden, die in der Eingabedatei mit den Bereitstellungsoptionen (.deploymentoptions) angegeben ist. Wird in der Eingabedatei mit den Bereitstellungsoptionen keine Ausgabeskriptdatei angegeben, tritt ein Fehler auf.  
  
 Weitere Informationen zu den Ausführungsmodi finden Sie im Abschnitt [Modi](#Modes)weiter unten in diesem Thema.  
  
 *output_script_file*  
 Der vollständige Pfad und der Dateiname der Ausgabeskriptdatei.  
  
 **/d**  
 Falls das **/o** -Argument verwendet wird, gibt dieses Argument an, dass das Hilfsprogramm keine Verbindung mit der Zielinstanz herstellen soll. Da keine Verbindung mit den Bereitstellungszielen hergestellt wird, wird das Ausgabeskript nur basierend auf den Informationen generiert, die aus den Eingabedateien abgerufen werden.  
  
> [!NOTE]  
>  Das Argument **/d** wird nur im Ausgabemodus verwendet. Dieses Argument wird ignoriert, wenn es im Antwortmodus oder im unbeaufsichtigten Modus angegeben wird. Weitere Informationen zu den Ausführungsmodi finden Sie im Abschnitt [Modi](#Modes)weiter unten in diesem Thema.  
  
## <a name="remarks"></a>Hinweise  
 Das Hilfsprogramm **Microsoft.AnalysisServices.Deployment** liest eine Gruppe von Dateien, die die Objektdefinitionen, Bereitstellungsziele, Bereitstellungsoptionen und Konfigurationseinstellungen angeben, und versucht, die Objektdefinitionen mithilfe der angegebenen Bereitstellungsoptionen und Konfigurationseinstellungen auf den angegebenen Bereitstellungszielen bereitzustellen. Dieses Hilfsprogramm kann eine Benutzeroberfläche bereitstellen, wenn es im Antwort- oder Ausgabemodus aufgerufen wird. Weitere Informationen zum Verwenden der Benutzeroberfläche, die für dieses Hilfsprogramm zum Erstellen von Antwortdateien bereitgestellt wird, finden Sie unter [Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md).  
  
 Das Hilfsprogramm befindet sich im Ordner "\Programme Dateien (x86) \Microsoft SQL Server\140\Binn\ManagementStudio".  
  
##  <a name="Modes"></a> Modi  
 Das Hilfsprogramm kann in den folgenden Modi ausgeführt werden.  
  
|Mode|Description|  
|----------|-----------------|  
|Unbeaufsichtigter Modus|Es wird keine Benutzeroberfläche angezeigt. Alle Informationen, die für die Bereitstellung benötigt werden, werden durch die Eingabedateien angegeben. Im unbeaufsichtigten Modus gibt das Hilfsprogramm keinen Status aus. Stattdessen kann eine optionale Protokolldatei verwendet werden, um Status- und Fehlerinformationen für eine spätere Prüfung aufzuzeichnen.|  
|Antwortmodus|Die Benutzeroberfläche des Bereitstellungs-Assistenten wird angezeigt; die Benutzerantworten werden in den angegebenen Ausgabedateien gespeichert, um sie bei einer späteren Bereitstellung verwenden zu können. Im Antwortmodus erfolgt keine Bereitstellung. Der Antwortmodus dient lediglich dazu, die Benutzerantworten aufzuzeichnen.|  
|Ausgabemodus|Es wird keine Benutzeroberfläche angezeigt. Alle Informationen, die für die Bereitstellung benötigt werden, werden durch die Eingabedateien angegeben.<br /><br /> Anders als im unbeaufsichtigten Modus wird die Ausgabe des Hilfsprogramms jedoch in eine Ausgabeskriptdatei geschrieben und nicht an die in den Eingabedateien angegebenen Bereitstellungsziele gesendet. Sofern das Argument **/d** nicht angegeben wird, stellt das Hilfsprogramm eine Verbindung mit jedem Bereitstellungsziel her, um die Metadaten zu vergleichen, während die Ausgabeskriptdatei generiert wird.|  
  
 [Zurück zu den Argumenten](#Arguments)  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird gezeigt, wie ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt im unbeaufsichtigten Modus bereitgestellt wird, wobei Status- und Fehlermeldungen für eine spätere Prüfung protokolliert werden.  
  
 `Microsoft.AnalysisServices.Deployment.exe`  
  
 `<drive>:\My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin`  
  
 `/s: C:\ My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin\deployment.log`  
  
## <a name="see-also"></a>Siehe auch  
 [Referenz zum Eingabeaufforderungs-Hilfsprogramm &#40;Datenbankmodul&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
