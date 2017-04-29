---
title: Statusleiste (Abfrage-Editor des Datenbankmoduls) | Microsoft Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e7f2d6f4-bb94-4cf5-a096-c34397e679af
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 34d7a9bfaf04f1ea7d201083201aa3c8a3895061
ms.lasthandoff: 04/11/2017

---
# <a name="status-bar-database-engine-query-editor"></a>Statusleiste (Abfrage-Editor des Datenbankmoduls)
  Die Statusleiste des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Fensters kann farblich codiert sein, um so anzuzeigen, mit welcher Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)] jedes Fenster verbunden ist.  
  
1.  **Before you begin:**  [Status Bar Colors](#StatusBarColors)  
  
2.  **To set a server status color in:**  [Object Explorer](#SetOEServerColor), [Registered Server](#SetRegServerColor)  
  
3.  **To use a status color:**  [Open Query Editor Using a Server Color](#OpenServerColor), [Open a Query Editor Specifying a Status Color](#OpenSpecColor)  
  
##  <a name="StatusBarColors"></a> Statusleistenfarben  
 Sie können einem bestimmten Serverknoten in entweder **Objekt-Explorer** oder **Registrierte Server**eine Statusleistenfarbe zuordnen. Die Farben können nur für Serverknoten angegeben werden, die mit einer Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)]verbunden sind, nicht aber für Serverknoten für andere SQL Server-Technologien. Ebenso können Sie eine benutzerdefinierte Statusleistenfarbe angeben, wann immer Sie ein neues [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor-Fenster mit einer Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)]verbinden. Sie können dann entweder mit der für den Serverknoten definierten Statusfarbe ein Abfrage-Editor-Fenster öffnen oder eine eindeutige Farbe für dieses Editorfenster angeben.  
  
 Eine benutzerdefinierte Statusleistenfarbe für einen Serverknoten in Objekt-Explorer muss beim Herstellen der Verbindung festgelegt werden. Um die einem vorhandenen Serverknoten zugeordnete Farbe zu ändern, müssen Sie die Verbindung trennen und dann unter Angabe der neuen Farbe die Verbindung erneut herstellen.  
  
##  <a name="SetOEServerColor"></a> Festlegen der Statusfarbe für einen Server in Objekt-Explorer  
 **So legen Sie eine Serverstatusfarbe in Objekt-Explorer fest**  
  
1.  Wählen Sie im **Objekt-Explorer**die Schaltfläche **Verbinden** und dann **Datenbankmodul...**aus.  
  
2.  Wählen Sie im Dialogfeld **Verbindung mit Server herstellen** die Option **Optionen >>**.  
  
3.  Aktivieren Sie das Kontrollkästchen **Benutzerdefinierte Farbe verwenden** .  
  
4.  Wählen Sie zur Festlegung der Farbe die Schaltfläche **Auswählen...** aus.  
  
5.  Wählen Sie entweder eine standardmäßige oder benutzerdefinierte Farbe aus und klicken Sie dann auf OK.  
  
6.  Geben Sie die restlichen Verbindungsinformationen ein und wählen Sie dann die Schaltfläche **Verbinden** aus.  
  
##  <a name="SetRegServerColor"></a> Festlegen der Statusfarbe für einen Registrierter Server  
 **So legen Sie eine Serverfarbe für einen Registrierten Server fest**  
  
1.  Klicken Sie unter **Registrierte Server**mit der rechten Maustaste auf einen Serverknoten und klicken Sie dann auf **Eigenschaften...**.  
  
2.  Wählen Sie im Dialogfeld **Serverregistrierungseigenschaften bearbeiten** die Registerkarte **Verbindungseigenschaften** aus.  
  
3.  Aktivieren Sie das Kontrollkästchen **Benutzerdefinierte Farbe verwenden** .  
  
4.  Wählen Sie zur Festlegung der Farbe die Schaltfläche **Auswählen...** aus.  
  
5.  Wählen Sie entweder eine standardmäßige oder benutzerdefinierte Farbe aus und klicken Sie dann auf OK.  
  
6.  Wählen Sie im Dialogfeld **Serverregistrierungseigenschaften bearbeiten** die Schaltfläche **Speichern** aus.  
  
##  <a name="OpenServerColor"></a> Öffnen eines Editors mithilfe einer Serverfarbe  
 **So öffnen Sie ein Editorfenster mithilfe einer Serverfarbe**  
  
-   Klicken Sie mit der rechten Maustaste entweder in **Objekt-Explorer** oder **Registrierte Server**auf einen Serverknoten, und wählen Sie **Neue Abfrage**aus.  
  
-   Markieren Sie alternativ einen Serverknoten und wählen Sie dann die Symbolleistenschaltfläche **Neue Abfrage** aus.  
  
-   Die Statusleiste im Editorfenster verwendet die für den zugeordneten Server definierte Farbe.  
  
##  <a name="OpenSpecColor"></a> Öffnen eines Editors unter Angabe einer Statusfarbe  
 **So öffnen Sie ein Editorfenster unter Angabe einer Statusfarbe**  
  
-   Öffnen Sie das Menü **Datei** , wählen Sie **Neu**aus, und wählen Sie dann **Datenbankmodul-Abfrage**aus.  
  
-   Wählen Sie im Dialogfeld **Verbindung mit Server herstellen** die Option **Optionen >>**.  
  
-   Aktivieren Sie das Kontrollkästchen **Benutzerdefinierte Farbe verwenden** .  
  
-   Wählen Sie zur Festlegung der Farbe die Schaltfläche **Auswählen...** aus.  
  
-   Wählen Sie entweder eine standardmäßige oder benutzerdefinierte Farbe aus und klicken Sie dann auf OK.  
  
-   Geben Sie die restlichen Verbindungsinformationen ein und wählen Sie dann die Schaltfläche **Verbinden** aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Abfrage- und Text-Editoren &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
