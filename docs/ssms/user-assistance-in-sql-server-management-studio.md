---
title: "Benutzerunterstützung in SQL Server Management Studio | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Help [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], user assistance
ms.assetid: 3c33a474-e507-4712-86fe-ae40e8370319
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d57d3d1dcd90bfe3af4ef8b630d3f0c0a2e0ff3c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="user-assistance-in-sql-server-management-studio"></a>Benutzerunterstützung in SQL Server Management Studio
Die Benutzerunterstützung ist in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] über das Menü ? und die [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]-Onlinedokumentation verfügbar. Über das Menü ? in [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] können Sie auf verschiedene Arten Informationen zu [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]abrufen. Außerdem erhalten Sie über dieses Menü Zugriff auf die [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Community und MSDN Onlineressourcen, die bislang noch nicht über die Hilfeumgebung verfügbar waren. Darüber hinaus lässt sich die Hilfeumgebung jetzt so konfigurieren, dass sie in der [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] -Umgebung oder in einem eigenen externen Fenster gestartet wird.  
  
## <a name="the-help-interface"></a>Die Hilfeoberfläche  
Die Optionen **Inhalt** und **Index** verfügen über eine Benutzeroberfläche und eine Funktionalität, mit denen Benutzer von [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] bereits vertraut sind. Folgende andere Optionen sind verfügbar:  
  
-   **Gewusst wie**  
  
    Enthält eine hierarchisch strukturierte Liste verknüpfter Seiten mit hilfreichen Themen zu allgemeinen [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Aufgaben. Der Inhalt ist nach Komponente und Aufgabe (Beispiel: Themen zur Replikation) usw. geordnet.  
  
-   **Suchen**  
  
    Sucht nach Themen, mit oder ohne vordefinierte Filter. Die Suche in [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] ist eine eigene Seite im Registerformat. Der Benutzer kann die Suche anhand von vordefinierten Thementyp-, Sprach- oder Technologiefiltern verfeinern. Standardmäßig wird bei der Suche kein vordefinierter Filter verwendet, und nur Themen in den installierten Auflistungen werden durchsucht.  
  
    Durch Aktivieren der Onlinehilfe kann der Benutzer Onlineressourcen in die Suche einbeziehen. Weitere Informationen finden Sie unter "MSDN Online- und [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Communities" nachfolgend in diesem Thema.  
  
-   **Dynamische Hilfe**  
  
    Zeigt automatisch Links zu relevanten Informationen an, wenn Benutzer in der [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] -Umgebung arbeiten.  
  
-   **Hilfefavoriten**  
  
    Speichert für einen einfachen späteren Zugriff Lesezeichen zu Benutzerthemen.  
  
Mit der Hilfe zur Hilfe (Hilfe zu[!INCLUDE[msCoName](../includes/msconame_md.md)] Document Explorer) gelangen Benutzer zur Hilfeviewer-Dokumentation. Die Themen sind allerdings getrennt von der [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Onlinedokumentation aufgelistet. Wenn Sie Informationen zum Hilfeviewer benötigen, wählen Sie in der **-Onlinedokumentation im Menü ? die Option** Hilfe zur Hilfe [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] aus.  
  
## <a name="msdn-online-and-sql-server-communities"></a>MSDN Online- und SQL Server-Communities  
Über die Hilfe in [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] können sich Benutzer auch auf verschiedene Arten an MSDN Online- und [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]-Communities im Web wenden, um Informationen zu erhalten. Folgende Aktionen sind möglich:  
  
-   Zugreifen auf [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Communities von der Seite Gewusst wie.  
  
-   Durchsuchen der Websites von MSDN Online- und [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Communities.  
  
#### <a name="to-access-sql-server-focused-communities-from-the-how-do-i-page"></a>So greifen Sie auf SQL Server bezogene Communities von der Seite Gewusst wie zu  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]im Menü **Hilfe** auf **Gewusst wie**.  
  
2.  Die [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] **Gewusst wie** wird geöffnet. Klicken Sie rechts auf der Randleiste mit den Community-Links auf den Namen der Community-Website, auf die Sie zugreifen möchten.  
  
    > [!NOTE]  
    > Für den Computer mit [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] muss eine direkte Webverbindung bestehen.  
  
    Bevor Sie MSDN Online- oder [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Communities durchsuchen können, müssen Sie die Onlinesuche aktivieren.  
  
#### <a name="to-enable-online-search"></a>So aktivieren Sie die Onlinesuche  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**. Erweitern Sie im Dialogfeld **Optionen** bei Bedarf die Knoten **Umgebung** und **Hilfe** , und klicken Sie dann auf **Online**.  
  
2.  Wählen Sie im Bereich **Beim Laden von Hilfeinhalten** eine Onlineoption aus.  
  
3.  Wählen Sie in der Liste **Diese Anbieter durchsuchen** die Suchanbieter aus, die Sie durchsuchen möchten, und heben Sie die Auswahl für die Anbieter auf, die nicht durchsucht werden sollen.  
  
4.  Wenn **Codezone-Community** einer der ausgewählten Suchanbieter ist, wählen Sie die entsprechenden Elemente in der Liste **Codezone-Community** aus, bzw. heben Sie die Auswahl für nicht gewünschte Elemente auf.  
  
5.  Klicken Sie auf **OK**.  
  
#### <a name="to-search-msdn-online-and-sql-server-focused-communities-from-the-search-page"></a>So durchsuchen Sie MSDN Online- und SQL Server-Communities über die Seite Suchen  
  
1.  Klicken Sie im Menü **Hilfe** auf **Suchen**.  
  
2.  Geben Sie in das Feld **Suchen nach** die Suchbegriffe ein, und klicken Sie dann auf **Suchen**.  
  
Unabhängig davon, ob Sie die Suche mithilfe der verfügbaren Filter ausführen (Technologie, Sprache und Thementyp), wird die Suche für alle ausgewählten Suchanbieter ausgeführt.  
  
## <a name="launching-help"></a>Starten der Hilfe  
Die Hilfe lässt sich aus [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]auf zwei Arten anzeigen. Wenn die [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Onlinedokumentation aus [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]heraus geöffnet wird, wird sie standardmäßig in einem Dokumentfenster außerhalb der [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] -Umgebung geöffnet. Dieses Fenster ist weiterhin mit [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]verknüpft. Es kann auf bestimmte [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] -Ereignisse reagieren, und wenn Sie [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]schließen, wird auch die Onlinedokumentation geschlossen. Das Öffnen der Onlinedokumentation auf diese Weise ist vor allem dann nützlich, wenn Sie mit zwei Bildschirmen arbeiten. Sie können das Fenster Onlinedokumentation auf den zweiten Bildschirm ziehen und dadurch schnell darauf zugreifen, ohne dass es der eigentlichen Arbeit im Weg ist.  
  
Sie können die Onlinedokumentation auch als Dokumentfenster in [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]öffnen. Diese Möglichkeit bietet sich an, wenn der Bildschirmbereich klein ist und Sie die Funktion von [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] zum Ausblenden von Fenstern nutzen möchten.  
  
> [!NOTE]  
> Wenn die Onlinedokumentation vollständig unabhängig von [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]sein soll, öffnen Sie die [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Onlinedokumentation über das Menü **Start** . In diesem Fall reagiert die Onlinedokumentation nicht auf Ihre Aktionen in der [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] -Umgebung und wird nicht geschlossen, wenn Sie [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]beenden.  
  
#### <a name="to-configure-help-and-sql-server-books-online-to-launch-inside-the-management-studio-window"></a>So konfigurieren Sie die Hilfe und die SQL Server-Onlinedokumentation zum Starten innerhalb des Fensters von Management Studio  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**, erweitern Sie **Umgebung**, erweitern Sie **Hilfe**, und klicken Sie dann auf **Allgemein**.  
  
2.  Klicken Sie im Feld **Hilfe anzeigen mit** auf **Integrierter Hilfeviewer**.  
  

