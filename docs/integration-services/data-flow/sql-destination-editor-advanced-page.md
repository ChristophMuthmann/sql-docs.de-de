---
title: "Ziel-Editor f&#252;r SQL (Seite Erweitert) | Microsoft Docs"
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
  - "sql13.dts.designer.sqlserverdestadapter.advanced.f1"
helpviewer_keywords: 
  - "Ziel-Editor für SQL"
ms.assetid: 9b46bcf8-ddaf-4d7d-90a6-80bc19517e9b
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Ziel-Editor f&#252;r SQL (Seite Erweitert)
  Auf der Seite **Erweitert** des Dialogfelds **Ziel-Editor für SQL** können Sie Optionen für die erweiterte Masseneinfügung angeben.  
  
 Weitere Informationen zum SQL Server-Ziel finden Sie unter [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md).  
  
## enthalten  
 **Identität beibehalten**  
 Gibt an, ob der Task Werte in Identitätsspalten einfügen soll. Der Standardwert dieser Eigenschaft ist **False**.  
  
 **NULL-Werte beibehalten**  
 Gibt an, ob der Task NULL-Werte beibehalten soll. Der Standardwert dieser Eigenschaft ist **False**.  
  
 **Tabellensperre**  
 Gibt an, ob die Tabelle beim Laden der Daten gesperrt wird. Der Standardwert dieser Eigenschaft ist **True**.  
  
 **Check-Einschränkungen**  
 Gibt an, ob Einschränkungen vom Task überprüft werden sollen. Der Standardwert dieser Eigenschaft ist **True**.  
  
 **Trigger auslösen**  
 Gibt an, ob die Masseneinfügung Trigger in Tabellen auslösen soll. Der Standardwert dieser Eigenschaft ist **False**.  
  
 **Erste Zeile**  
 Gibt die erste einzufügende Zeile an. Der Standardwert dieser Eigenschaft ist **-1**. Er zeigt an, dass kein Wert zugewiesen wurde.  
  
> [!NOTE]  
>  Löschen Sie den Inhalt des Textfelds im Dialogfeld **Ziel-Editor für SQL** , um anzugeben, dass Sie keinen Wert für diese Eigenschaft zuweisen möchten. Verwenden Sie im Fenster **Eigenschaften**, im Dialogfeld **Erweiterter Editor** und im Objektmodell den Wert -1.  
  
 **Letzte Zeile**  
 Gibt die letzte einzufügende Zeile an. Der Standardwert dieser Eigenschaft ist **-1**. Er zeigt an, dass kein Wert zugewiesen wurde.  
  
> [!NOTE]  
>  Löschen Sie den Inhalt des Textfelds im Dialogfeld **Ziel-Editor für SQL** , um anzugeben, dass Sie keinen Wert für diese Eigenschaft zuweisen möchten. Verwenden Sie im Fenster **Eigenschaften**, im Dialogfeld **Erweiterter Editor** und im Objektmodell den Wert -1.  
  
 **Maximale Anzahl von Fehlern**  
 Gibt die Anzahl der Fehler an, die auftreten können, bevor die Masseneinfügung abgebrochen wird. Der Standardwert dieser Eigenschaft ist **–1**. Er zeigt an, dass kein Wert zugewiesen wurde.  
  
> [!NOTE]  
>  Löschen Sie den Inhalt des Textfelds im Dialogfeld **Ziel-Editor für SQL** , um anzugeben, dass Sie keinen Wert für diese Eigenschaft zuweisen möchten. Verwenden Sie im Fenster **Eigenschaften**, im Dialogfeld **Erweiterter Editor** und im Objektmodell den Wert -1.  
  
 **Timeout**  
 Gibt die Anzahl der Sekunden an, die abgewartet werden, bevor die Masseneinfügung aufgrund eines Timeouts abgebrochen wird.  
  
 **Spalten sortieren**  
 Geben Sie die Namen der zu sortierenden Spalten an. Jede Spalte kann in auf- oder absteigender Reihenfolge sortiert werden. Wenn Sie mehrere Spalten verwenden, nach denen sortiert werden soll, trennen Sie die Namen in der Liste mit Kommas.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Ziel-Editor für SQL &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/sql-destination-editor-connection-manager-page.md)   
 [Ziel-Editor für SQL &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/sql-destination-editor-mappings-page.md)   
 [Massenladen von Daten mithilfe des SQL Server-Ziels](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  