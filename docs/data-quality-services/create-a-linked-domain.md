---
title: "Erstellen einer verknüpften Domäne | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/08/2011
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
- sql13.dqs.kb.linkeddomain.f1
ms.assetid: fd99d422-c53d-4d7c-9cdd-303c703683b6
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 14b11ae1442a695e683aafc60da424cc6c9f9497
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="create-a-linked-domain"></a>Erstellen einer verknüpften Domäne
  In diesem Thema wird beschrieben, wie eine verknüpfte Domäne in einer Wissensdatenbank in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) erstellt wird. Eine verknüpfte Domäne wird aus einer anderen, zuvor vorhandenen Domäne, erstellt und erbt alle Werte, Regeln und Eigenschaften von der Domäne, mit der sie verknüpft wird - mit Ausnahme des Namens und der Beschreibung. Sie können einen Satz verknüpfter Domänen als eine Domäne verwalten. Indem Sie eine Domäne mit der anderen verknüpfen, erstellen Sie eine Domäne, die ihre Inhalte von einer anderen Domäne erbt.  
  
## <a name="scenarios"></a>Szenarien  
 Verknüpfte Domänen sind in den folgenden Szenarien besonders nützlich.  
  
### <a name="mapping-multiple-fields-to-domains-that-share-values-rules-and-properties"></a>Zuordnen von mehreren Feldern zu Domänen, für Werte, Regeln und Eigenschaften gemeinsam nutzen  
 Sie können der gleichen Domäne nicht zwei Felder zuordnen, aber Sie könnten einer Domäne ein Feld zuordnen und dann einer Domäne ein zweites Feld zuordnen, die mit der ersten Domäne verknüpft ist. Auf diese Weise werden die Felder zu zwei verschiedenen Domänen zugeordnet, die die gleichen Inhalte und Eigenschaften aufweisen (außer Name und Beschreibung). Weitere Informationen finden Sie unter [Map two fields to linked domains](#Map).  
  
### <a name="controlling-data-flow-to-composite-domains"></a>Steuern des Datenflusses zu Verbunddomänen  
 Verknüpfte Domänen ermöglichen es Ihnen, den Datenfluss zwischen Felder und Verbunddomänen zu steuern. Sie können unterscheiden, wenn Daten von einem Feld in eine Verbunddomäne fließen und wenn Daten von einem anderen, sehr ähnlichen Feld nicht in die Verbunddomäne fließen. Dies erreichen Sie, indem Sie angeben, dass von zwei verknüpften Domänen eine Teil einer Verbunddomäne ist, die andere aber nicht. Aus Domänenperspektive sind verknüpfte Domänen identisch. Sie enthalten das gleiche Wissen. Aus Verbunddomänenperspektive unterscheiden sich verknüpfte Domänen allerdings voneinander. Die eine ist Teil der Verbunddomäne, die andere aber nicht.  
  
 Ein Beispiel ist ein Datensatz, der die folgenden Felder enthält: Kundenvorname, Kundennachname und Vorname des Vaters. Angenommen, Sie ordnen den Kundenvornamen und den Vornamen des Vaters einer Vornamendomäne zu und machen die Vornamendomäne und die Nachnamendomäne zu Teilen einer Verbunddomäne für vollständige Namen. Das Problem ist, dass der Vorname des Vaters der Verbunddomäne ohne Nachname hinzugefügt wird. Wenn Sie allerdings die beiden Vornamenfelder mit einer Domäne verknüpfen und die beiden Domänen miteinander verknüpfen, können Sie die Kundenvornamedomäne der Verbunddomäne für vollständige Namen hinzufügen und das Feld für den Vornamen des Vaters nicht der Verbunddomäne hinzufügen. Dadurch verhindern Sie, dass der Vorname des Vaters der Verbunddomäne hinzugefügt wird.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um eine verknüpfte Domäne zu erstellen, müssen Sie eine Wissensdatenbank und eine vorhandene Domäne haben, zu der Sie eine Verknüpfung herstellen möchten.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_kb_editor“ oder „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um eine verknüpfte Domäne zu erstellen.  
  
##  <a name="Create"></a> Erstellen einer verknüpften Domäne  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Öffnen oder erstellen Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm eine Wissensdatenbank. Wählen Sie **Domänenverwaltung** als Aktivität aus, und klicken Sie dann auf **Öffnen** oder **Erstellen**. Weitere Informationen finden Sie unter [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md) oder [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md).  
  
3.  Klicken Sie in der **Domänenliste** auf der Seite **Domänenverwaltung** mit der rechten Maustaste auf die Domäne, die Sie mit einer neuen Domäne verknüpfen möchten, und klicken Sie dann auf **Verknüpfte Domäne erstellen**.  
  
    > [!NOTE]  
    >  Es gibt kein Symbol für das Erstellen einer verknüpften Domäne. Sie müssen daher den Befehl im Kontextmenü verwenden.  
  
4.  Geben Sie im Dialogfeld **Domäne erstellen** einen Namen ein, der für die Wissensdatenbank eindeutig ist, und eine Beschreibung mit bis zu 256 Zeichen. Überprüfen Sie, ob der Name der verknüpften Domäne richtig ist.  
  
5.  Klicken Sie auf **OK** , um die Erstellung der verknüpften Domäne abzuschließen.  
  
6.  Falls notwendig können Sie den Namen oder die Beschreibung der verknüpften Domäne auf der Registerkarte „Domäneneigenschaften“ ändern.  
  
7.  Klicken Sie auf **Fertig stellen** , um die Domänenverwaltungsaktivität abzuschließen, wie in [End the Domain Management Activity](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)beschrieben.  
  
##  <a name="Map"></a> Map two fields to linked domains  
  
1.  Öffnen Sie eine Wissensdatenbank mit der Wissensermittlungsaktivität, und ordnen Sie der Datenbank und der Tabelle oder Sicht die Wissensdatenbank zu.  
  
2.  Ordnen Sie einer Domäne ein Feld zu, und versuchen Sie dann, der gleichen Domäne ein zweites Feld zuzuordnen.  
  
3.  Im Popupfenster, das angibt, dass die Domäne bereits verwendet wird, klicken Sie auf „Ja“, um eine verknüpfte Domäne zu erstellen.  
  
4.  Geben Sie im Dialogfeld „Domäne erstellen“ einen Domänennamen und eine Beschreibung ein, und klicken Sie dann auf „OK“.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Erstellen einer verknüpften Domäne  
 Nachdem Sie eine verknüpfte Domäne erstellt haben, können Sie andere Domänenverwaltungsaufgaben in der Domäne ausführen, Sie können die Wissensermittlung durchführen, um der Domäne Wissen hinzuzufügen, oder Sie können der Domäne eine Abgleichsrichtlinie hinzufügen. Weitere Informationen finden Sie unter [Durchführen der Wissensermittlung](../data-quality-services/perform-knowledge-discovery.md), [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md) oder [Erstellen einer Abgleichsrichtlinie](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Behavior"></a> Verhalten einer verknüpften Domäne  
 Sie können die Einstellungen für eine verknüpfte Domäne wie folgt ändern:  
  
-   Sie können den Namen und die Beschreibung einer verknüpften Domäne ändern.  
  
-   Um die Domäneneigenschaften für die Eigenschaften **Datentyp**, **Führende Werte verwenden**oder **Formatausgabe an** zu ändern, wählen Sie die Domäne aus, zu der Sie eine Verknüpfung erstellt haben, und ändern Sie diese Einstellungen auf der Registerkarte **Domäneneigenschaften** für diese Domäne. Sie können diese Einstellungen nicht in den Eigenschaften der verknüpften Domäne ändern. Weitere Informationen finden Sie unter [Create a Domain](../data-quality-services/create-a-domain.md).  
  
-   Einstellungen auf den Registerkarten **Verweisdaten**, **Domänenregeln**, **Domänenwerte**und **Begriffsbasierte Beziehungen** der Domänenverwaltungsseite können für die verknüpfte Domäne oder die Domäne, mit der sie verknüpft wurde, geändert werden. Die Änderungen werden von der anderen Domäne geerbt.  
  
 Verknüpfte Domänen besitzen die folgenden Eigenschaften:  
  
-   Sie können die Verknüpfung zweier Domänen nicht aufheben. Um die Verknüpfung zu entfernen, löschen Sie eine der verknüpften Domänen.  
  
-   Wenn Sie in der Domänenliste der Domänenverwaltungsseite eine verknüpfte Domäne auswählen, enthält die Zeichenfolge, die die verknüpfte Domäne im Bereich mit der Tabelle **Wert** identifiziert, einen Hinweis darauf, dass die Domäne eine verknüpfte Domäne ist.  
  
-   Wenn Sie eine Domäne löschen, mit der eine andere Domäne verknüpft ist, werden beide Domänen gelöscht. Sie können jedoch eine verknüpfte Domäne löschen. In diesem Fall wird die Domäne, von der die Verknüpfung ausgeht, nicht gelöscht.  
  
-   Eine verknüpfte Domäne kann nicht mit einer Domäne verknüpft werden, die ihrerseits mit einer anderen Domäne verknüpft ist.  
  
-   Sie können keine Domäne oder Verbunddomäne erstellen, die mit einer Verbunddomäne verknüpft ist.  
  
-   Wenn Sie auf eine verknüpfte Domäne auf einer der Domänenverwaltungsregisterkarten doppelklicken, wird die Domäne für die Bearbeitung mit einem Hinweis in der Namenszeichenfolge geöffnet, dass es sich um eine verknüpfte Domäne handelt.  
  
  

