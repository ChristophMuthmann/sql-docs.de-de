---
title: Importieren einer Wissensdatenbank aus einer DQS-Datei | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
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
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4375d8083fb1bb129631231c74e13859fce3ab53
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="import-a-knowledge-base-from-a-dqs-file"></a>Importieren einer Wissensdatenbank aus einer DQS-Datei

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In diesem Thema wird beschrieben, wie eine gesamte Wissensdatenbank aus einer DQS-Datendatei in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) importiert wird. Sie erstellen die Datendatei, indem Sie eine vorhandene Wissensdatenbank innerhalb der Anwendung exportieren [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] (siehe [Exportieren einer Wissensdatenbank in eine DQS-Date](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)).  
  
 Durch Verwendung einer DQS-Datendatei zum Exportieren des Inhalts einer Wissensdatenbank und Importieren des Inhalts in eine andere Wissensdatenbank auf dem gleichen [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] oder einem anderen [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] wird der Wissensgenerierungsprozess vereinfacht, Zeit gespart und der Aufwand verringert. Auf diese Weise haben Sie die Möglichkeit, eine Wissensdatenbank und ihr Wissen zusammen mit anderen zu nutzen und somit Zeit zu sparen. Die DQS-Datei enthält alle Informationen aus der Wissensdatenbank, einschließlich Domänen und der Abgleichsrichtlinie, aber keine Informationen über angefügte Verweisdaten. Veröffentlichte und unveröffentlichte Daten werden importiert.  
  
 Eine DQS-Datendatei wird verschlüsselt und kann nicht angezeigt werden.  
  
 Wenn Sie eine Wissensdatenbank importieren, können Sie den gleichen Namen verwenden, sofern der Wissensdatenbankname nicht bereits in der Clientanwendung vorhanden ist. In diesem Fall müssen Sie die Wissensdatenbank umbenennen.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um eine Wissensdatenbank aus einer DQS-Datei importieren zu können, müssen Sie diese zuvor in eine DQS-Datei exportiert haben.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_kb_editor“ oder „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um eine Wissensdatenbank aus einer DQS-Datei zu importieren.  
  
##  <a name="Import"></a> Import a knowledge base from a .dqs file  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie auf dem [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Neue Wissensdatenbank**.  
  
3.  Geben Sie einen Namen für die Wissensdatenbank ein.  
  
4.  Klicken Sie auf den Abwärtspfeil für **Wissensdatenbank erstellen aus**, und wählen Sie dann **Aus DQS-Datei importieren**aus.  
  
5.  Klicken Sie für **Datendatei auswählen**auf **Durchsuchen**.  
  
6.  Wechseln Sie im Dialogfeld **Aus Datendatei importieren** zum Ordner, in dem die zu importierende DQS-Datei gespeichert ist, und klicken Sie dann auf den Namen der Datei. Klicken Sie auf **Öffnen**.  
  
7.  Überprüfen Sie, ob in der Liste **Domäne** die richtige Wissensdatenbank und Domänen angezeigt werden.  
  
8.  Wählen Sie die auszuführende Aktivität aus, und klicken Sie dann auf **Erstellen**.  
  
9. Überprüfen Sie im Dialogfeld **Wissensdatenbank importieren** , ob in der Statuszeile angegeben ist, dass der Importvorgang abgeschlossen wurde. Klicken Sie auf **OK**.  
  
10. Schließen Sie die erforderliche Wissensermittlung, Domänenverwaltung oder Abgleichsrichtlinientasks ab, und klicken Sie dann auf **Fertig stellen**.  
  
11. Klicken Sie auf **Veröffentlichen** , um das Wissen in der Wissensdatenbank zu veröffentlichen, oder klicken Sie auf **Nein** , wenn dieses nicht veröffentlicht werden soll.  
  
12. Wenn Sie die Wissensdatenbank veröffentlichten, klicken Sie auf **OK**.  
  
13. Überprüfen Sie auf der Startseite von Data Quality Services, dass die Wissensdatenbank unter **Zuletzt verwendete Wissensdatenbank**aufgeführt wird.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Importieren einer Wissensdatenbank aus einer DQS-Datei  
 Nachdem Sie eine Wissensdatenbank aus einer DQS-Datei importiert haben, können Sie der Wissensdatenbank Wissen hinzufügen oder die Wissensdatenbank in einem Bereinigungs- oder Abgleichsprojekt verwenden - je nach Inhalt der Wissensdatenbank. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md), [Verwalten einer Verbunddomäne](../data-quality-services/managing-a-composite-domain.md), [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md), [Datenbereinigung](../data-quality-services/data-cleansing.md) oder [Datenabgleich](../data-quality-services/data-matching.md).  
  
  
