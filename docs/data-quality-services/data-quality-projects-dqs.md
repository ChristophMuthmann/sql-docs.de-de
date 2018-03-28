---
title: Data Quality-Projekte (DQS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a43fc9c0-19b6-414a-8661-4c7c55e0c03e
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97ee117319697d817f760a25332728648fa565f9
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="data-quality-projects-dqs"></a>Data Quality-Projekte (DQS)
  Ein Data Quality-Projekt in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) ist ein Mittel, die Qualität von den Quelldaten mithilfe einer Wissensdatenbank zu verbessern durch das Ausführen von *Datenbereinigung* und *Datenabgleichsaktivitäten* und das Exportieren der resultierenden Daten dann in eine SQL Server-Datenbank oder eine CSV-Datei. Sie können ein Data Quality-Projekt als Bereinigungsprojekt oder Abgleichsprojekt erstellen, um jeweilige Aktivitäten auszuführen. Bereinigung und Abgleichsprojekte können mit der gleichen Wissensdatenbank ausgeführt werden, da Wissen für Datenbereinigung und das Abgleichen in die gleiche Wissensdatenbank integriert werden können.  
  
 Ein Data Quality-Projekt hat die folgenden Vorteile:  
  
-   Data Quality-Projekte ermöglichen es Ihnen, die Quelldaten mithilfe von Wissen in einer DQS-Wissensdatenbank zu bereinigen.  
  
-   Sie können Datenabgleiche für Ihre Quelldaten durchführen, indem Sie die Abgleichsrichtlinie in einer Wissensdatenbank verwenden.  
  
-   Stellt einen Assistenten bereit, um Sie durch die Bereinigungs- und Abgleichsaktivitäten zu führen und exportiert die Daten gemäß Ihrer Auswahl in eine SQL Server-Datenbank oder eine CSV-Datei. Der Data Steward kann das Data Quality-Projekt verwenden, um die computergestützten/interaktiven Schritte zum Bereinigen und Abgleichen von Daten auszuführen.  
  
##  <a name="Cleansing"></a> Data Quality-Projekt: Bereinigungsaktivität  
 Data Quality-Projekte ermöglichen es Ihnen, die Quelldaten basierend auf einer Wissensdatenbank zu bereinigen. Die Datenbereinigungsaktivität in DQS ist ein zwei Schritte umfassender Prozess:  
  
1.  In einem *computergestützten* Datenbereinigungsprozess werden Quelldaten im Hinblick auf das Wissen in der Wissensdatenbank analysiert und Änderungen vorgeschlagen. Die verarbeiteten Daten werden von DQS kategorisiert (vorgeschlagen, neu, ungültig und richtig) und werden dem Benutzer zur weiteren Verarbeitung angezeigt.  
  
2.  Ein *interaktiver* Bereinigungsprozess, der es dem Data Steward ermöglicht, die vom computerunterstützten Datenbereinigungsprozess vorgeschlagenen Daten zu genehmigen, abzulehnen oder zu ändern.  
  
 Ausführliche Informationen zur Bereinigungsaktivität in einem Data Quality-Projekt finden Sie unter [Data Cleansing](../data-quality-services/data-cleansing.md).  
  
##  <a name="Matching"></a> Data Quality-Projekt: Abgleichsaktivität  
 Ein Data Quality-Abgleichsprojekt ermöglicht es Ihnen, Abgleichsaktivitäten auf Grundlage der Abgleichsrichtlinie in einer Wissensdatenbank auszuführen, um Datenduplizierung durch das Identifizieren exakter und ungefährer Treffer zu verhindern und dadurch das Entfernen doppelter Daten zu ermöglichen. Es wird empfohlen, dass Sie die Daten bereinigen, bevor Sie entsprechende Abgleiche ausführen. Gehen Sie folgendermaßen vor:  
  
1.  Erstellen Sie ein Data Quality-Projekt, wählen Sie die **Bereinigungsaktivität** aus, schließen Sie die Datenbereinigungsaktivität für die Quelldaten ab, und exportieren Sie sie dann in eine Tabelle in einer SQL Server-Datenbank.  
  
2.  Erstellen Sie ein weiteres Data Quality-Projekt mithilfe einer Wissensdatenbank, die eine Abgleichsrichtlinie enthält, wählen Sie die **Abgleichsaktivität** aus, und wählen Sie dann auf der Seite **Struktur** die Datenbank und die Tabelle aus, in die Sie die gereinigten Daten in Schritt 1 exportiert haben.  
  
3.  Schließen Sie die Abgleichsaktivität für die bereinigten Daten ab.  
  
 Ausführliche Informationen zur Abgleichsaktivität in einem Data Quality-Projekt finden Sie unter [Data Matching](../data-quality-services/data-matching.md).  
  
##  <a name="ProfilingNotification"></a> Datenprofilerstellung und Benachrichtigungen  
 Beim Ausführen der Bereinigungs- und Abgleichsaktivitäten in einem Data Quality-Projekt werden Ihnen Statistiken und Informationen über die von DQS verarbeiteten Daten in Echtzeit angezeigt. Mithilfe der Datenprofilerstellung können Sie die Effektivität der Bereinigungs- und Abgleichsprozesse bewerten und potenziell bestimmen, inwiefern die Datenbereinigung oder der -abgleich dabei behilflich waren, die Datenqualität zu verbessern. DQS-Profilerstellung stellt zwei Data Quality-Dimensionen bereit: *Vollständigkeit* (das Ausmaß des Vorhandenseins von Daten) und *Genauigkeit* (das Ausmaß, in dem Daten für den beabsichtigten Zweck verwendet werden können). Außerdem werden auf Grundlage der Datenprofilinformationen dem Benutzer Benachrichtigungen zu den Aktionen angezeigt, die ausgeführt werden können, um die Datenbereinigungs- und Datenabgleichsvorgänge zu verbessern. Weitere Informationen zur Datenprofilerstellung und zu Benachrichtigungen finden Sie unter [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie ein Data Quality-Projekt erstellt wird.|[Erstellen eines Data Quality-Projekts](../data-quality-services/create-a-data-quality-project.md)|  
|Beschreibt, wie ein Data Quality-Projekt geöffnet, entsperrt, umbenannt oder gelöscht wird.|[Öffnen, Entsperren, Umbenennen und Löschen eines Data Quality-Projekts](open-unlock-rename-and-delete-a-data-quality-project.md)|  
|Beschreibt, wie ein Integration Services-Projekt in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]geöffnet wird.|[Öffnen von Integration Services-Projekten im Data Quality-Client](../data-quality-services/open-integration-services-projects-in-data-quality-client.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DQS-Wissensdatenbanken und -Domänen](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
