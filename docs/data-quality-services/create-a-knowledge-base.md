---
title: Erstellen einer Wissensdatenbank | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dqs.kb.selectkb.f1
- sql13.dqs.kb.newkb.f1
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc53cc2fe0e492e46a7367a8ed9c9454939e6c3a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-a-knowledge-base"></a>Erstellen einer Wissensdatenbank

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In diesem Thema wird beschrieben, wie eine Wissensdatenbank in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) erstellt und auf die Domänenverwaltung, die Wissensermittlung und das Hinzufügen einer Abgleichsrichtlinie vorbereitet wird.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um eine Wissensdatenbank zu erstellen, müssen Sie [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] und [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]installiert haben.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die dqs_kb_editor- oder dqs_administrator-Rolle in der DQS_MAIN-Datenbank verfügen, um eine Wissensdatenbank zu erstellen.  
  
##  <a name="Createaknowledgebase"></a> Create a knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Neue Wissensdatenbank**.  
  
3.  Geben Sie einen Namen und eine Beschreibung für die neue Wissensdatenbank ein.  
  
4.  Wählen Sie unter **Wissensdatenbank erstellen aus**aus, worauf die neue Wissensdatenbank basieren soll:  
  
    -   Wählen Sie **Keine** aus, wenn die neue Wissensdatenbank nicht auf einer vorhandenen Wissensdatenbank oder Datendatei basieren soll.  
  
    -   Wählen Sie **Vorhandene Wissensdatenbank** aus, um eine Wissensdatenbank, die bereits auf [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]erstellt wurde, oder die Standardwissensdatenbank als Grundlage für die neue Wissensdatenbank zu verwenden. Wählen Sie die Wissensdatenbank aus der Dropdownliste **Wissensdatenbank auswählen** aus, oder klicken Sie auf **Durchsuchen** , um das Dialogfeld **Wissensdatenbank auswählen** anzuzeigen, wählen Sie eine vorhandene Wissensdatenbank als Grundlage für die neue Wissensdatenbank aus, und klicken Sie dann auf **OK**. Wenn Sie eine Wissensdatenbank aus dem Tablett auswählen, werden die Domänen und Abgleichsregeln in der Wissensdatenbank im rechten Bereich des Dialogfelds angezeigt. Sie können auch die Wissensdatenbank **DQS-Daten** auswählen. Das ist die Standardwissensdatenbank, die allgemeine Standarddomänen und auf US-amerikanische Unternehmens-, Adressen- und Parteidaten bezogenes Wissen enthält.  
  
    -   Wählen Sie **Aus DQS-Datei importieren** aus, um die neue Wissensdatenbank auf eine DQS-Datei auf dem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]zu basieren. Klicken Sie auf **Durchsuchen**, wählen Sie eine DQS-Datendatei mit der Erweiterung ".dqs" aus, und klicken Sie dann auf **OK**.  
  
5.  Wählen Sie unter **Aktivität auswählen**die Aktivität aus, die Sie für die neue Wissensdatenbank ausführen möchten:  
  
    -   Wählen Sie **Domänenverwaltung** aus, um die Wissensdatenbank zu erstellen, und öffnen Sie dann die Bildschirme, in denen Sie die Domänen in der Wissensdatenbank ändern.  
  
    -   Wählen Sie **Wissensermittlung** aus, um die Wissensdatenbank zu erstellen und um den Assistenten zum Analysieren eines Datenbeispiels zu öffnen, und füllen Sie die Domänen der Wissensdatenbank mit den Ergebnissen auf.  
  
    -   Wählen Sie **Abgleichsrichtlinie** aus, um eine Abgleichsrichtlinie zu erstellen und sie der Wissensdatenbank hinzuzufügen.  
  
6.  Klicken Sie auf **Erstellen**.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Erstellen einer Wissensdatenbank  
 Nachdem Sie eine Wissensdatenbank erstellt haben, werden ein Assistent für die Wissensermittlung, ein Assistent zum Erstellen einer Abgleichsrichtlinie oder Seiten für die Domänenverwaltung angezeigt. Weitere Informationen zu Wissensermittlung, Domänenverwaltung oder Abgleichsrichtlinien finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md) oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
  
