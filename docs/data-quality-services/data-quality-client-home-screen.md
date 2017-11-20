---
title: Startbildschirm des Data Quality-Clients | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/29/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.clienthome.f1
ms.assetid: 7c6ec469-bc7d-4d19-8e21-11dcf8ade108
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 00ed6a9eaa24ff9981ca4184a7ec8ef3107ffc0f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="data-quality-client-home-screen"></a>Startbildschirm des Data Quality-Clients
  Über diesen Bildschirm können Sie auf die Benutzeroberflächen für die drei wichtigsten [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] -Taskgruppen (DSQ) zugreifen: Wissensdatenbank-Verwaltung, Data Quality-Projekte und Verwaltung.  
  
## <a name="options"></a>Optionen  
  
### <a name="knowledge-base-management"></a>Wissensdatenbank-Verwaltung  
 Eine DQS-Wissensdatenbank ist ein Repository mit Metadaten, die von DQS zur Verbesserung der Datenqualität verwendet werden. Diese Metadaten werden von der DQS-Plattform in einem computergestützten Wissensermittlungsprozess und vom Data Steward in einem interaktiven Domänenverwaltungsprozess erstellt.  
  
 **Neue Wissensdatenbank**  
 Erstellen Sie eine Wissensdatenbank entweder von Grund auf neu oder basierend auf den Metadaten einer vorhandenen Wissensdatenbank. Mit diesem Befehl wird eine Seite geöffnet, in der Sie die Wissensdatenbank identifizieren können, basierend auf einer vorhandenen Datenbank die gewünschte Wissensdatenbankaktivität ausführen können und anschließend die Wissensdatenbank erstellen können.  
  
 **Öffnen der Wissensdatenbank**  
 Öffnen Sie eine Wissensdatenbank, um die Domänen zu verwalten, die Wissensermittlung auszuführen oder eine Abgleichsrichtlinie erstellen zu können. Wenn Sie auf die Schaltfläche **Wissensdatenbank öffnen** klicken, wird die Seite **Öffnen der Wissensdatenbank** angezeigt, auf der eine Liste vorhandener Wissensdatenbanken mitsamt deren Eigenschaften, aktuellen Status, Wissensdatenbanken und Details zu den Domänen angezeigt wird. Wählen Sie eine Wissensdatenbank aus, und öffnen Sie sie mittels **Wissensdatenbank öffnen**.  
  
 **Zuletzt verwendete Wissensdatenbank**  
 Öffnen Sie eine bereits erstellte Wissensdatenbank aus der Liste auf dem Bildschirm. Wenn keine Sperrung vorliegt, klicken Sie mit der rechten Maustaste, und wählen Sie dann die Aktivität aus, mit der Sie die Wissensdatenbank starten möchten (Domänenverwaltung, Wissensermittlung oder Abgleichsrichtlinie).  
  
 Sie können eine gesperrte Wissensdatenbank nur dann öffnen und bearbeiten, wenn Sie sie selbst gesperrt haben. Wenn dies der Fall ist, wird die Wissensdatenbank mit dem Status geöffnet, den sie beim Schließen aufwies. Selbiges ist in Klammern angegeben. Wenn eine Wissensdatenbank gesperrt wird und Sie sie nicht gesperrt haben, können Sie sie nur schreibgeschützt öffnen.  
  
### <a name="data-quality-projects"></a>Data Quality-Projekte  
 Ein Data Quality-Projekt ist der Prozess, bei dem DQS die Datenbereinigung oder den Datenabgleich ausführt, wobei für beide eine computergestützte Datenkorrektur und eine interaktive Datenbereinigung verwendet werden.  
  
 **Neues Data Quality-Projekt**  
 Starten Sie das Projekt zum Erstellen eines neuen Projekts. Mit diesem Befehl wird eine Seite geöffnet, in der Sie das Projekt identifizieren, es einer Wissensdatenbank zuordnen, Details über die Datenbank anzeigen, die gewünschte Projektaktivität auswählen und anschließend das Projekt erstellen können.  
  
 **Data Quality-Projekt öffnen**  
 Öffnen Sie ein Projekt, um die Datenbereinigung oder den Datenabgleich auszuführen. Wenn Sie auf die Schaltfläche **Data Quality-Projekt öffnen** klicken, wird die Seite **Data Quality-Projekt öffnen** angezeigt, auf der eine Liste vorhandener Projekte mitsamt deren Eigenschaften, aktuellen Status, Wissensdatenbanken und Details zu den Domänen und Abgleichsrichtlinienregeln angezeigt wird. Wählen Sie ein Projekt aus, und öffnen Sie es mittels **Data Quality-Projekt öffnen**.  
  
 **Zuletzt verwendetes Data Quality-Projekt**  
 Wählen Sie ein bereits erstelltes Projekt aus der Liste auf dem Bildschirm aus. Sie können ein gesperrtes Projekt nur öffnen, wenn Sie es selbst gesperrt haben. Wenn dies der Fall ist, wird das Projekt mit dem Status geöffnet, den es beim Schließen aufwies. Selbiges ist in Klammern angegeben. Wenn das Projekt abgeschlossen wurde, wird es im Exportschritt der Aktivität geöffnet.  
  
### <a name="administration"></a>Verwaltung  
 Die DQS-Verwaltung ermöglicht die Überwachung, Konfiguration und Wartung von DQS.  
  
 **Aktivitätsüberwachung**  
 Zeigen Sie eine Sicht mit dem Status aller (aktuellen und vergangenen) Aktivitäten an, die sich auf den verbundenen [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]beziehen. Die überwachten Aktivitätstypen umfassen die Wissensverwaltung, ein Data Quality-Projekt und die SSIS-basierte Datenkorrektur.  
  
 **Konfiguration**  
 Zeigen Sie die Konfigurationseigenschaften für Verweisdatendienstkonten, (beide durch Windows Azure Marketplace und direkt zu Verweisdatendiensten) allgemeine Einstellungen (interaktive Bereinigung, Abgleich und Profilerstellung) und Einstellungen über den Protokollschweregrad an.  
  
## <a name="see-also"></a>Siehe auch  
 [DQS-Wissensdatenbanken und -Domänen](../data-quality-services/dqs-knowledge-bases-and-domains.md)   
 [Data Quality-Projekte &#40;DQS&#41;](../data-quality-services/data-quality-projects-dqs.md)   
 [DQS-Verwaltung](../data-quality-services/dqs-administration.md)  
  
  

