---
title: Alle Prinzipale durchsuchen (Dialogfeld) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: service
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6f33cd13592961f50fa69d359a9b9d22a1f38a7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="browse-all-principals-dialog-box"></a>Alle Prinzipale durchsuchen (Dialogfeld)
  Verwenden Sie das Dialogfeld **Alle Prinzipale durchsuchen** , um einen Datenbankprinzipal auszuwählen und die Berechtigungen des Prinzipals für das ausgewählte Projekt oder alle in einem ausgewählten Ordner enthaltenen Projekte zu ändern.  
  
 **Was möchten Sie tun?**  
  
-   [Öffnen des Dialogfelds "Alle Prinzipale durchsuchen"](#open_dialog)  
  
-   [Konfigurieren der Optionen](#options)  
  
##  <a name="open_dialog"></a> Öffnen des Dialogfelds "Alle Prinzipale durchsuchen"  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server her.  
  
     Sie stellen eine Verbindung mit der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz her, die den SSISDB-Katalog hostet.  
  
2.  Erweitern Sie im Objekt-Explorer die Struktur, um den Knoten **Integration Services-Kataloge** anzuzeigen.  
  
3.  Erweitern Sie den **SSISDB** -Knoten.  
  
4.  Um die Berechtigungen des Prinzipals für alle in einem ausgewählten Ordner enthaltenen Projekte zu ändern, klicken Sie mit der rechten Maustaste auf den Ordner, und klicken Sie dann auf **Eigenschaften**.  
  
     Um die Berechtigungen des Prinzipals für ein ausgewähltes Projekt zu ändern, erweitern Sie den Ordner, der das Projekt enthält, klicken Sie mit der rechten Maustaste auf das Projekt, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Wählen Sie die Seite **Berechtigungen** aus, und klicken Sie dann auf **Durchsuchen**.  
  
##  <a name="options"></a> Konfigurieren der Optionen  
 Auf dieser Seite werden die Prinzipale aus der Katalogsicht sys.database_principals der SSISDB-Datenbank angezeigt.  
  
 Durch Auswählen von Prinzipalen werden diese der Liste **Anmeldenamen oder Rollen** auf der Seite **Berechtigungen** des übergeordneten Dialogfelds hinzugefügt, sobald Sie auf **OK** geklickt und das Dialogfeld **Alle Prinzipale durchsuchen** geschlossen haben. Nachdem Sie die Prinzipale der Liste **Anmeldenamen oder Rollen** hinzugefügt haben, können Sie die entsprechenden Berechtigungen für das ausgewählte Projekt ändern.  
  
 **Spaltenauswahl**  
 Mit dieser Option können Sie den Prinzipal der Liste **Anmeldenamen oder Rollen** auf der Seite **Berechtigungen** im übergeordneten Dialogfeld hinzufügen.  
  
 **Symbolspalte**  
 Ein Symbol, das dem **Typ** des Prinzipals entspricht.  
  
 **Name**  
 Der Name des Prinzipals.  
  
 **Typ**  
 Der Typ des Prinzipals. Häufig verwendeten Typen sind folgende:  
  
-   SQL-Benutzer  
  
-   Windows-Benutzer  
  
-   Datenbankrolle  
  
  
