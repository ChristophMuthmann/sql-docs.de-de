---
title: "Ändern der Definitionen von Ressourcenintegritätsrichtlinien (SQL Server-Hilfsprogramm) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.SWB.UE.UTILITY.ADMINISTRATION.F1
ms.assetid: 27bec0b6-92e9-448e-8c70-fe36802cf128
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cec210a329c442240451cce7cec04dba9fafd9c0
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="modify-a-resource-health-policy-definition-sql-server-utility"></a>Ändern der Definitionen von Ressourcenintegritätsrichtlinien (SQL Server-Hilfsprogramm)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Definitionen von Ressourcenintegritätsrichtlinien in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] geändert werden. Bevor Sie eine Richtlinie zur Ressourcenauslastung im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm ändern können, müssen Sie einen Steuerungspunkt für das Hilfsprogramm (UCP) erstellen. Weitere Informationen finden Sie unter [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Die Richtlinien zur Ressourcenauslastung des Hilfsprogramms können für Datenebenenanwendungen und verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konfiguriert werden. Richtlinien zur Ressourcenauslastung können global für alle Datenebenenanwendungen und verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm definiert werden, oder Sie definieren sie für jede Datenebenenanwendung und jede verwaltete Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einzeln im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramm. Sie können auch globale Richtlinien implementieren und einzelne Datenebenenanwendungen oder verwaltete Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anhand eigener Richtliniendefinitionen konfigurieren lassen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="modify-global-resource-utilization-policies-in-a-sql-server-utility"></a>Ändern globaler Richtlinien zur Ressourcenauslastung in einem SQL Server-Hilfsprogramm  
  
1.  Stellen Sie eine Verbindung mit dem UCP in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]her.  
  
2.  Klicken Sie im Navigationsbereich des Hilfsprogramm-Explorers auf **Hilfsprogrammverwaltung** , um globale Überwachungsrichtlinien anzuzeigen oder zu ändern, und klicken Sie dann im Bereich Inhalt des Hilfsprogramm-Explorers auf die Registerkarte **Richtlinie** .  
  
3.  Wählen Sie im Bereich Inhalt des Hilfsprogramm-Explorers die Option **Globale Überwachungsrichtlinien für Datenebenenanwendungen festlegen** oder Globale **Überwachungsrichtlinien für verwaltete Instanzen festlegen** aus, indem Sie auf den Pfeil oder die Richtlinienbeschreibung klicken.  
  
4.  Verwenden Sie die Steuerelemente auf der rechten Seite der Richtlinienbeschreibungen, um Richtliniengrenzwerte für die Unter- oder Überauslastung festzulegen.  
  
5.  Verwenden Sie ggf. die Schaltflächen **Anwenden**, **Verwerfen**oder **Standard wiederherstellen** . Bei der Richtlinienänderung kann es bis zu 15 Minuten dauern, bis die Änderungen an das Dashboard des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms übertragen und Details aufgelistet werden.  
  
6.  Um Daten zu aktualisieren, klicken Sie mit der rechten Maustaste auf den Knoten **Hilfsprogrammverwaltung** im Navigationsbereich des Hilfsprogramm-Explorers und wählen **Aktualisieren**aus.  
  
#### <a name="modify-resource-health-policy-definitions-for-an-individual-data-tier-application-or-an-individual-managed-instance-of-sql-server-in-a-sql-server-utility"></a>Ändern der Definitionen von Ressourcenintegritätsrichtlinien für eine einzelne Datenebenenanwendung oder eine einzelne verwaltete Instanz von SQL Server in einem SQL Server-Hilfsprogramm  
  
1.  Stellen Sie eine Verbindung mit dem UCP in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]her.  
  
2.  Klicken Sie im Navigationsbereich des Hilfsprogramm-Explorers auf **Bereitgestellte Datenebenenanwendungen**oder auf **Verwaltete Instanzen**, um Überwachungsrichtlinien für eine einzelne Datenebenenanwendung oder verwaltete Instanz anzuzeigen oder zu ändern.  
  
3.  Klicken Sie im Inhaltsbereich des Hilfsprogramm-Explorers auf die Datenebenenanwendung oder den Namen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, deren Richtlinien Sie ändern möchten, und klicken Sie dann auf die Registerkarte **Richtliniendetails** .  
  
4.  Wählen Sie die Richtlinie aus, die angezeigt oder geändert werden soll, indem Sie auf den Pfeil oder die Richtlinienbeschreibung klicken. Globale Richtlinien sind standardmäßig ausgewählt.  
  
5.  Aktivieren Sie das Optionsfeld **Globale Richtlinie überschreiben** , um globale Richtlinien zu überschreiben und eine einzelne Richtliniendefinition für die angegebene Datenebenenanwendung zu implementieren.  
  
6.  Verwenden Sie die Steuerelemente auf der rechten Seite der Richtlinienbeschreibung, um Richtliniengrenzwerte für die Unter- oder Überauslastung festzulegen.  
  
7.  Verwenden Sie ggf. die Schaltflächen **Anwenden**, **Verwerfen**oder **Standard wiederherstellen** . Bei der Richtlinienänderung kann es bis zu 15 Minuten dauern, bis die Änderungen an das Dashboard des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms übertragen und Details aufgelistet werden.  
  
8.  Um Daten zu aktualisieren, klicken Sie mit der rechten Maustaste auf den Knoten **Bereitgestellte Datenebenenanwendungen** im Navigationsbereich des Hilfsprogramm-Explorers, und wählen Sie **Aktualisieren**aus.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Anzeigen der Ergebnisse zu Ressourcenintegritätsrichtlinien &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)  
  
  
