---
title: Einrichten einer SQL Server-Datenbankwarnung (Windows) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8eabe827b89c3931523bda848e01471853cbde6b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="set-up-a-sql-server-database-alert-windows"></a>Einrichten einer SQL Server-Datenbankwarnung (Windows)
  Sie können mithilfe des Systemmonitors eine Warnung erstellen, die ausgelöst wird, wenn ein Schwellenwert für einen Leistungsindikator des Systemmonitors erreicht wird. Als Reaktion auf die Warnung kann der Systemmonitor eine Anwendung starten, wie z. B. eine benutzerdefinierte Anwendung, die für das Verarbeiten der Warnung geschrieben wurde. Sie können beispielsweise eine Warnung erstellen, die ausgelöst wird, wenn die Anzahl der Deadlocks einen bestimmten Wert überschreitet.  
  
 Warnungen können auch mit Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent definiert werden. Weitere Informationen finden Sie unter [Warnungen](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef).  
  
### <a name="to-set-up-a-sql-server-database-alert"></a>So richten Sie eine SQL Server-Datenbankwarnung ein  
  
1.  Erweitern Sie in der Navigationsstruktur des Fensters Leistung die Option **Leistungsprotokolle und Warnungen**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Warnungen**, und klicken Sie dann auf **Neue Warnungseinstellungen**.  
  
3.  Geben Sie im Dialogfeld **Neue Warnungseinstellungen** einen Namen für die neue Warnung ein, und klicken Sie dann auf **OK**.  
  
4.  Fügen Sie im Dialogfeld für die neue Warnung auf der Registerkarte **Allgemein** einen **Kommentar**hinzu, und klicken Sie auf **Hinzufügen** , um der Warnung einen Leistungsindikator hinzuzufügen.  
  
     Jede Warnung muss mindestens einen Leistungsindikator aufweisen.  
  
5.  Wählen Sie im Dialogfeld Leistungsindikatoren hinzufügen in der Liste **Leistungsobjekt** ein SQL Server-Objekt aus, und wählen Sie dann in der Liste **Leistungsindikatoren wählen**einen Leistungsindikator aus.  
  
6.  Klicken Sie auf **Hinzufügen**, um der Warnung den Leistungsindikator hinzuzufügen. Sie können weitere Leistungsindikatoren hinzufügen, oder klicken Sie auf **Schließen** , um zum Dialogfeld für die neue Warnung zurückzukehren.  
  
7.  Klicken Sie im Dialogfeld für die neue Warnung in der Liste **Warnung bei Wert** auf **größer als**oder **kleiner als** , und geben Sie dann in das Feld **Limit**einen Schwellenwert ein.  
  
     Die Warnung wird generiert, wenn der Wert für den Leistungsindikator größer oder kleiner als der Schwellwert ist (je nachdem, ob Sie auf **größer als** oder **kleiner als**geklickt haben).  
  
8.  Legen Sie in den Feldern **Daten erfassen alle** die Stichprobenfrequenz fest.  
  
9. Legen Sie auf der Registerkarte **Aktion** die Aktionen fest, die jedes Mal ausgeführt werden, wenn die Warnung ausgelöst wird.  
  
10. Legen Sie auf der Registerkarte **Zeitplan** den Beginn und das Ende des Zeitplans für die Warnungssuche fest.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer SQL Server-Datenbankwarnung](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)  
  
  
