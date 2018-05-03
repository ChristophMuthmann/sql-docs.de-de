---
title: Konfigurieren von Analysis Services-Projekteigenschaften (SSDT) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aa56475a9b5ff1e71649e4d249afa7f9851d6bfc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-analysis-services-project-properties-ssdt"></a>Konfigurieren von Analysis Services-Projekteigenschaften (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Ein [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt wird mit bestimmten Standardeigenschaften definiert, die sich auf das Erstellen und Bereitstellen des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts auswirken.  
  
 Zum Ändern der Projekteigenschaften klicken Sie mit der rechten Maustaste auf das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projektobjekt, und klicken Sie dann auf **Eigenschaften**. Alternativ können Sie im Menü **Projekt** auf Eigenschaften klicken.  
  
## <a name="property-description"></a>Eigenschaftsbeschreibung  
 In der folgenden Tabelle werden die einzelnen Projekteigenschaften unter Angabe der zugehörigen Standardwerte beschrieben sowie Informationen über das Ändern der Werte bereitgestellt.  
  
|Eigenschaft|Standardeinstellung|Description|  
|--------------|---------------------|-----------------|  
|Build/Deployment Server Edition|Die zum Entwickeln des Projekts verwendete Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Gibt die Edition von SQL Server an, auf der Projekte letztendlich bereitgestellt werden. Sind an einem Projekt mehrere Entwickler beteiligt, so muss jeder von ihnen die Edition von SQL Server kennen und verstehen, um zu wissen, welche Funktionen in das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt integriert werden sollen.|  
|Build/Deployment Server Edition|Die für die Entwicklung des Projekts verwendete Version|Gibt die Version von SQL Server an, auf der Projekte letztendlich bereitgestellt werden.|  
|Build/Ausgaben|/bin|Der relative Pfad für die Ausgabe des Projekterstellungsprozesses.|  
|Build/Kennwörter entfernen|Wahr|Gibt an, ob bekannte Kennwörter aus Verbindungszeichenfolgen entfernt werden, die während des Erstellungsprozesses in das Ausgabeverzeichnis geschrieben werden. Kennwörter werden entfernt, um eine erhöhe Sicherheit zu bieten. Werden Kennwörter entfernt, müssen sie beim Verarbeiten des bereitgestellten Projekts angegeben werden, damit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf die Quelldaten zugreifen kann.|  
|Debuggen/Startobjekt|\<Derzeit aktives Objekt >|Bestimmt das Objekt, das gestartet wird, wenn Sie das Debuggen starten.|  
|Bereitstellung/Bereitstellungsmodus|Nur geänderte Objekte bereitstellen|Standardmäßig werden nur die an den Projektobjekten vorgenommenen Änderungen bereitgestellt (vorausgesetzt, dass keine weiteren Änderungen an den Objekten außerhalb des Projekts direkt vorgenommen wurden). Sie haben auch die Möglichkeit, bei jeder Bereitstellung alle Projektobjekte zu berücksichtigen. Verwenden Sie die Einstellung Nur geänderte Objekte bereitstellen, um die bestmögliche Leistung zu erzielen.|  
|Bereitstellung/Verarbeitungsoption|Standardwert|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bestimmt standardmäßig den Verarbeitungstyp, der beim Bereitstellen der an Objekten vorgenommenen Änderungen erforderlich ist. Diese Einstellung ermöglicht im Allgemeinen die schnellste Bereitstellungszeit. Sie haben aber auch die Möglichkeit, für die jeweilige Bereitstellung die vollständige Verarbeitung oder keine Verarbeitung zu wählen.|  
|Bereitstellung/Transaktionsbereitstellung|False|Standardmäßig ist die Bereitstellung geänderter oder aller Objekte keine Transaktionsbereitstellung bei der Verarbeitung dieser bereitgestellten Objekte. Die Bereitstellung kann erfolgreich ausgeführt werden und persistent sein, auch wenn bei der Verarbeitung ein Fehler auftritt. Sie können diese Standardeinstellung ändern, um die Bereitstellung und Verarbeitung in einer einzelnen Transaktion zu integrieren.|  
|Bereitstellung/Zielserver|localhost|Standardmäßig werden Datenbankobjekte des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts auf der Standardinstanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf dem lokalen Computer bereitgestellt, auf dem [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] verwendet wird. Ändern Sie diese Standardeinstellung, um eine benannte Instanz auf dem lokalen Computer bzw. eine beliebige Instanz auf einem beliebigen Remotecomputer anzugeben, auf dem Sie über die Berechtigung zum Erstellen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekten verfügen.|  
|Bereitstellung/Datenbank|\<Projektname >|Der Name der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank, in der die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projektobjekte nach der Bereitstellung instanziiert werden, ist standardmäßig der Name des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts zum Zeitpunkt seiner Definition. Ändern Sie diese Eigenschaft, um den Namen der Datenbank auf der über die Server-Eigenschaft angegebene [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz zu ändern.|  
  
## <a name="property-configurations"></a>Eigenschaftskonfigurationen  
 Eigenschaften werden jeweils auf Konfigurationsbasis definiert. Projektkonfigurationen ermöglichen Entwicklern die Arbeit mit einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt mit verschiedenen Einstellungen für Builds, Debugvorgänge und Bereitstellungen, ohne dabei die zugrunde liegenden XML-Projektdateien direkt bearbeiten zu müssen.  
  
 Ein Projekt wird zunächst mit einer einzelnen Konfiguration mit der Bezeichnung Entwicklung erstellt. Sie können zusätzliche Konfigurationen erstellen und mithilfe des Konfigurations-Managers zwischen den Konfigurationen hin- und herschalten.  
  
 Diese häufig verwendete Konfiguration wird von allen Entwicklern verwendet, bis zusätzliche Konfigurationen erstellt werden. Jedoch kann es während der verschiedenen Phasen der Projektentwicklung, z. B. während der Erstentwicklung und beim ersten Testen eines Projekts, vorkommen, dass unterschiedliche Entwickler unterschiedliche Datenquellen verwenden und das Projekt auf unterschiedlichen Servern für unterschiedliche Zwecke bereitstellen. Konfigurationen ermöglichen es Ihnen, diese unterschiedlichen Einstellungen in unterschiedlichen Konfigurationsdateien beizubehalten.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Analysis Services-Projekten & #40; SSDT & #41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Bereitstellen von Analysis Services-Projekten & #40; SSDT & #41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
