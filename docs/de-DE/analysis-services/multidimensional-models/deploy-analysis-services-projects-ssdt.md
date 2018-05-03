---
title: Bereitstellen von Analysis Services-Projekten (SSDT) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5203f8d373bc2c214e161280a16851010feb087b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-analysis-services-projects-ssdt"></a>Bereitstellen von Analysis Services-Projekten (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Während der Entwicklung eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]stellen Sie das Projekt häufig auf einem Entwicklungsserver bereit, um die vom Projekt definierte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank zu erstellen. Dies ist erforderlich, um das Projekt zu testen. Hierbei werden z. B. Zellen im Cube durchsucht, Dimensionselemente durchsucht oder KPI-Formeln (Key Performance Indicators) überprüft.  
  
## <a name="deploying-a-project"></a>Bereitstellen eines Projekts  
 Sie können ein Projekt eigenständig oder alle Projekte innerhalb der Projektmappe zusammen bereitstellen. Beim Bereitstellen eines Projekts werden nacheinander die folgenden Aktionen ausgeführt. Zuerst wird das Projekt erstellt. In diesem Schritt werden die Ausgabedateien erstellt, die die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank und die Objekte, aus denen sie besteht, definieren. Danach wird der Zielserver überprüft. Abschließend werden die Zieldatenbank und ihre Objekte auf dem Zielserver erstellt. Während der Bereitstellung werden vorher vorhandene Datenbanken vollständig vom Bereitstellungsmodul durch die Inhalte des Projekts ersetzt, es sei denn, diese Objekte wurden durch das Projekt im Rahmen einer früheren Bereitstellung erstellt.  
  
 Nach der erstbereitstellung, wird die Datei IncrementalSnapshot.xml im generiert die \<Projektname > \obj-Ordner. Anhand dieser Datei wird bestimmt, ob die Datenbank oder ihre Objekte auf dem Zielserver außerhalb des Projekts verändert wurden. Ist dies der Fall, werden Sie aufgefordert, alle Objekte in der Zieldatenbank zu überschreiben. Wenn alle Änderungen innerhalb des Projekts vorgenommen wurden und die inkrementelle Bereitstellung für das Projekt konfiguriert wurde, werden nur die Änderungen auf dem Zielserver bereitgestellt.  
  
 Die Projektkonfiguration und die zugehörigen Einstellungen bestimmen die Bereitstellungseigenschaften, die für die Bereitstellung des Projekts verwendet werden. Bei einem freigegebenen Projekt kann jeder Entwickler seine eigene Konfiguration mit eigenen Projektkonfigurationsoptionen verwenden. So kann z. B. jeder Entwickler einen anderen Testserver angeben, um unabhängig von anderen Entwicklern arbeiten zu können.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Analysis Services-Projekts & #40; SSDT & #41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  
