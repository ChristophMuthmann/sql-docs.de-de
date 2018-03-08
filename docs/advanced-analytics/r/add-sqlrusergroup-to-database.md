---
title: "Fügen Sie als Datenbankbenutzer SQLRUserGroup | Microsoft Docs"
ms.custom: 
ms.date: 12/21/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- Implizite Authentifizierung
- SQLRUserGroup
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 8e448e665044b1b8f63d30b7c99adf62419ae283
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/11/2018
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>Fügen Sie SQLRUserGroup als einen Datenbankbenutzer hinzu.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Artikel erläutert das Erteilen Sie der Gruppe der Worker von Diensten verwendeten Konten Machine Learning in SQL Server die Berechtigungen zum Herstellen einer Verbindung mit der Datenbank, und führen R oder Python-Aufträge im Namen des Benutzers erforderlich.

## <a name="what-is-sqlrusergroup"></a>Was ist SQLRUserGroup?

Während des Setups von [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] oder [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)], neue Windows-Benutzerkonten werden erstellt, um die Ausführung von R zu unterstützen oder ein Python-Skript Aufgaben unter den Sicherheitstoken für die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Dienst.

Sie können diese Konten anzeigen, in der Windows-Benutzergruppe **SQLRUserGroup**. Standardmäßig werden 20 Konten erstellt, ist in der Regel mehr als ausreichend, für die Ausführung von Machine Learning-Aufträge.

Wenn ein Benutzer ein Machine learning-Skript von einem externen Client sendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktiviert ein Konto Arbeitsthreads verfügbar, wird es auf die Identität des aufrufenden Benutzers zugeordnet und führt das Skript im Namen des Benutzers. Dieser neue Dienst des Datenbankmoduls unterstützt die sichere Ausführung externer Skripts, die aufgerufen *implizite Authentifizierung*.

Jedoch Wenn R oder Python-Skripts von einem remote Data Science-Client ausgeführt werden sollen, und Sie die Windows-Authentifizierung verwenden, geben Sie diese Konten über die Berechtigung zum Anmelden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz in Ihrem Namen.

## <a name="add-sqlrusergroup-as-a-sql-server-login"></a>Hinzufügen von SQLRUserGroup als SQL Server-Anmeldung

1. Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Objekt-Explorer den Knoten **Sicherheit**, klicken Sie mit der rechten Maustaste auf **Anmeldungen**, und wählen Sie anschließend **Neue Anmeldung**.

2. In der **Anmeldung - neu** wählen Sie im Dialogfeld **Suche**. (Geben Sie nichts in das Feld noch.)
    
     ![Klicken Sie auf Suchen, die zum Hinzufügen von neuen Anmeldenamen für Machine Learning](media/implied-auth-login1.png "klicken Sie auf Suchen, Hinzufügen von neuen Anmeldenamen für Machine Learning")

3. In der **Benutzer oder Gruppe auswählen** klicken Sie auf die **Objekttypen** Schaltfläche.

     ![Suchen von Objekttypen, die neue Anmeldung für Machine Learning hinzufügen](media/implied-auth-login2.png "Objekttypen hinzuzufügende neue Anmeldung für Machine Learning suchen")

4. In der **Objekttypen** wählen Sie im Dialogfeld **Gruppen**. Deaktivieren Sie alle anderen Kontrollkästchen.

     ![Wählen Sie im Dialogfeld Objekttypen Gruppen](media/implied-auth-login3.png "Gruppen auswählen, im Dialogfeld "Objekttypen"")

4. Klicken Sie auf **erweitert**, überprüfen Sie, ob die zu suchende Position der aktuellen Computer, und klicken Sie dann auf **Jetzt suchen**.

     ![Klicken Sie auf "Jetzt suchen", um die Liste der Gruppen abrufen](media/implied-auth-login4.png "klicken Sie auf Jetzt suchen zum Abrufen der Liste der Gruppen")

5. Führen Sie einen Bildlauf durch die Liste der Gruppenkonten auf dem Server, bis Sie beginnen mit gefunden `SQLRUserGroup`.
    
    + Der Name der Gruppe, die für den Launchpad-Dienst zugeordnet ist die _Standardinstanz_ ist immer **SQLRUserGroup**, unabhängig davon, ob Sie R, Python oder beide installiert. Wählen Sie dieses Konto für die Standardinstanz nur ein.
    + Bei Verwendung einer _benannte Instanz_, den Namen der Instanz wird auf den Namen der Standard-Worker-Gruppenname angefügt `SQLRUserGroup`. Daher, wenn die Instanz "MLTEST" benannt wird, der Standardbenutzernamen Gruppe für diese Instanz wäre **SQLRUserGroupMLTest**.
 
     ![Beispiel für Gruppen auf Server](media/implied-auth-login5.png "Beispiel für Gruppen auf Server")
   
5. Klicken Sie auf **OK** um das Dialogfeld "Erweiterte Suche" zu schließen.

    > [!IMPORTANT]
    > Achten Sie darauf, dass Sie das richtige Konto für die Instanz ausgewählt haben. Jede Instanz können eigenen Launchpad-Dienst und die Gruppe für diesen Dienst erstellt haben. Ein Launchpad-Konten oder eine workerrolle können nicht für Instanzen freigegeben werden.

6. Klicken Sie auf **OK** einmal zum Schließen der **Benutzer oder Gruppe auswählen** (Dialogfeld).

7. In der **Anmeldung - neu** (Dialogfeld), klicken Sie auf **OK**. In der Standardeinstellung ist die Anmeldung der **öffentlichen** Rolle zugewiesen und verfügt über die Berechtigung, eine Verbindung zum Datenbankmodul herzustellen.

## <a name="change-the-number-of-worker-accounts-in-sqlrusergroup"></a>Ändern der Anzahl von Worker-Konten in SQLRUserGroup

Wenn Sie beabsichtigen, die von Machine Learning viel zu nutzen, können Sie die Anzahl der Konten, die zum Ausführen externer Skripts verwendet werden, wie in diesem Artikel beschrieben erhöhen: 

+ [Ändern des benutzerkontenpools für Machine learning](modify-the-user-account-pool-for-sql-server-r-services.md)

Standardmäßig werden 20 Konten erstellt, das 20 gleichzeitige Sitzungen unterstützt. Parallelisierte Aufgaben belegen keine zusätzliche Konten. Wenn ein Benutzer eine bewerteten Aufgabe, die parallelen Verarbeitung verwendet ausführt, ist das gleiche workerkonto z. B. für alle Threads wiederverwendet.
