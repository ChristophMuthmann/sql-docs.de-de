---
title: "Erstellen und Zuordnen einer Serverumgebung | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.isenvprop.permissions.f1"
  - "sql13.ssis.ssms.isenvprop.general.f1"
  - "sql13.ssis.ssms.iscreateenv.f1"
  - "sql13.ssis.ssms.isenvprop.variables.f1"
ms.assetid: b1cbb697-713f-48e4-b234-b23724d87451
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# Erstellen und Zuordnen einer Serverumgebung
  Sie erstellen eine Serverumgebung, um Laufzeitwerte für Pakete festzulegen, die in einem auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellten Projekt enthalten sind. Anschließend können Sie die Umgebungsvariablen Parametern für ein bestimmtes Paket, für Einstiegspunktpakete oder für alle Pakete in einem angegebenen Projekt zuordnen. Ein Einstiegspunktpaket ist in der Regel ein übergeordnetes Paket, von dem ein untergeordnetes Paket ausgeführt wird.  
  
> [!IMPORTANT]  
>  Ein Paket kann jeweils nur mit den Werten ausgeführt werden, die in einer einzelnen Serverumgebung enthalten sind.  
  
 Sie können Sichten nach einer Liste von Serverumgebungen, Umgebungsverweisen und Umgebungsvariablen abfragen. Sie können auch gespeicherte Prozeduren aufrufen, um Umgebungen, Umgebungsverweise und Umgebungsvariablen hinzuzufügen, zu löschen und zu ändern. Weitere Informationen finden Sie im Abschnitt **Serverumgebungen, Servervariablen und Serverumgebungsverweise** im [SSIS Catalog](../../integration-services/service/ssis-catalog.md).  
  
### So erstellen und verwenden Sie eine Serverumgebung  
  
1.  Erweitern Sie in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] den Knoten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Kataloge> **SSISDB** im Objekt-Explorer, und navigieren Sie zum Ordner **Umgebungen** für das Projekt, für das Sie eine Umgebung erstellen können.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Umgebungen**, und klicken Sie dann auf **Umgebung erstellen**.  
  
3.  Geben Sie einen Namen für die Umgebung und optional eine Beschreibung ein, und klicken Sie dann auf **OK**.  
  
4.  Klicken Sie mit der rechten Maustaste auf die neue Umgebung, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Gehen Sie auf der Seite **Variablen** wie folgt vor, um eine Variable hinzuzufügen.  
  
    1.  Wählen Sie den **Typ** für die Variable aus. Der Name der Variablen **muss nicht** mit dem Namen des Projektparameters übereinstimmen, den Sie der Variablen zuordnen.  
  
    2.  Geben Sie eine optionale **** Beschreibung für die Variable ein.  
  
    3.  Geben Sie den **** Wert für die Umgebungsvariable ein.  
  
         Informationen zu den Benennungsregeln für Umgebungsvariablen finden Sie im Abschnitt **Umgebungsvariable** im [SSIS Catalog](../../integration-services/service/ssis-catalog.md).  
  
    4.  Geben Sie an, ob die Variable einen vertraulichen Wert enthält, indem Sie das Kontrollkästchen **Vertraulich** aktivieren oder deaktivieren.  
  
         Bei Auswahl von **Vertraulich**wird der Variablenwert nicht im Feld **Wert** angezeigt.  
  
         Vertrauliche Werte werden im SSISDB-Katalog verschlüsselt. Weitere Informationen zur Verschlüsselung finden Sie unter [SSIS Catalog](../../integration-services/service/ssis-catalog.md).  
  
6.  Gehen Sie auf der Seite **Berechtigungen** wie folgt vor, um ausgewählten Benutzern und Rollen Berechtigungen zu erteilen oder zu verweigern.  
  
    1.  Klicken Sie auf **Durchsuchen**, und wählen Sie dann im Dialogfeld **Alle Prinzipale durchsuchen** mindestens einen Benutzer und eine Rolle aus.  
  
    2.  Wählen Sie im Bereich **Anmeldenamen oder Rollen** den Benutzer oder die Rolle aus, dem bzw. der Sie Berechtigungen erteilen oder verweigern möchten.  
  
    3.  Klicken Sie im Bereich **Explizit** neben den einzelnen Berechtigungen auf **Erteilen** oder **Verweigern** .  
  
7.  Um ein Skript für die Umgebung zu erstellen, klicken Sie auf **Skript**. Das Skript wird standardmäßig in einem neuen Abfrage-Editor-Fenster angezeigt.  
  
    > [!TIP]  
    >  Sie müssen auf **Skript** klicken, nachdem Sie Änderungen an den Umgebungseigenschaften vorgenommen, z. B. eine Variable hinzugefügt, haben und bevor Sie im Dialogfeld **Umgebungseigenschaften** auf **OK** klicken. Andernfalls wird kein Skript generiert.  
  
8.  Klicken Sie auf **OK** , um die Änderungen an den Umgebungseigenschaften zu speichern.  
  
9. Erweitern Sie unter dem Knoten **SSISDB** im Objekt-Explorer den Ordner **Projekte**, klicken Sie mit der rechten Maustaste auf das Projekt, und klicken Sie dann auf **Konfigurieren**.  
  
10. Klicken Sie auf der Seite **Verweise** auf **Hinzufügen** , um eine Umgebung hinzuzufügen, und klicken Sie dann auf **OK** , um den Verweis in der Umgebung zu speichern.  
  
11. Klicken Sie mit der rechten Maustaste erneut auf das Projekt, und klicken Sie dann auf **Konfigurieren**.  
  
12. Um die Umgebungsvariable einem Parameter zuzuordnen, den Sie dem Paket zur Entwurfszeit hinzugefügt haben, oder einem Parameter, der beim Konvertieren des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekts in das Projektbereitstellungsmodell generiert wurde, gehen Sie wie folgt vor.  
  
    1.  Klicken Sie auf der Seite **Parameter** auf der Registerkarte **Parameter** neben dem Feld **Wert** auf die Schaltfläche zum Durchsuchen.  
  
    2.  Klicken Sie auf **Umgebungsvariable verwenden**, und wählen Sie dann die Umgebungsvariable aus, die Sie erstellt haben.  
  
13. Um die Umgebungsvariable einer Eigenschaft des Verbindungs-Managers zuzuordnen, gehen Sie wie folgt vor. Parameter für die Eigenschaften des Verbindungs-Managers werden automatisch auf dem SSIS-Server generiert.  
  
    1.  Klicken Sie auf der Seite **Parameter** auf der Registerkarte **Verbindungs-Manager** neben dem Feld **Wert** auf die Schaltfläche zum Durchsuchen.  
  
    2.  Klicken Sie auf **Umgebungsvariable verwenden**, und wählen Sie dann die Umgebungsvariable aus, die Sie erstellt haben.  
  
14. Klicken Sie zweimal auf **OK** , um die Änderungen zu speichern.  
  
  