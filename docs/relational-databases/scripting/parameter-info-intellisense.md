---
title: "Parameterinfo (IntelliSense) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Parameterinfo (Option) [IntelliSense]"
  - "Abschluss gespeicherter Funktionsparameter [IntelliSense]"
  - "Sprachverweise [SQL Server]"
  - "IntelliSense [SQL Server], Parameterinfo (Option)"
ms.assetid: 56c2aac9-c65c-4679-b62c-d9f689876dde
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Parameterinfo (IntelliSense)
  Die Option [!INCLUDE[msCoName](../../includes/msconame-md.md)] Parameter Info **von** IntelliSense öffnet eine Parameterliste, die Informationen über die Anzahl, Namen und Typen der Parameter enthält, die für eine Funktion oder gespeicherte Prozedur erforderlich sind. Der fett formatierte Parameter gibt den nächsten Parameter an, der beim Eingeben einer Funktion oder gespeicherten Prozedur erforderlich ist.  
  
 Die Parameterliste wird auch für geschachtelte Funktionen angezeigt. Wenn Sie eine Funktion als Parameter für eine andere Funktion eingeben, werden in der Parameterliste die Parameter für die innere Funktion angezeigt. Wenn die Parameterliste der inneren Funktion vollständig ist, werden in der Parameterliste anschließend die Parameter der äußeren Funktion angezeigt.  
  
#### So zeigen Sie Parameterinfo für Funktionen oder gespeicherte Prozeduren an  
  
1.  Geben Sie nach dem Namen einer Funktion wie gewohnt eine öffnende Klammer ein, um die Parameterliste zu öffnen. Wenn Sie den Namen einer gespeicherten Prozedur eingegeben haben, geben Sie wie gewohnt ein Leerzeichen ein, um Informationen zu den Prozedurparametern abzurufen.  
  
     IntelliSense zeigt die vollständige Deklaration für die Funktion oder die Parameter für eine gespeicherte Prozedur in einem Popupfenster direkt unter der Einfügemarke an. Der erste Parameter in der Liste wird fett formatiert angezeigt.  
  
2.  Beim Eingeben der Parameter ändert sich die Fettformatierung, um den nächsten Parameter anzugeben, den Sie eingeben müssen.  
  
3.  Drücken Sie zu einem beliebigen Zeitpunkt die ESC-TASTE, um die Liste zu schließen, oder fahren Sie mit der Eingabe fort, bis die Funktion abgeschlossen ist.  
  
     Wenn Sie für eine Funktion die schließende Klammer eingeben, schließen Sie auch die Parameterliste.  
  
#### So starten Sie Parameterinfo manuell  
  
1.  Wählen Sie im Menü **Bearbeiten** **IntelliSense** und anschließend **Parameterinfo**aus.  
  
2.  Drücken Sie die Tastenkombination STRG+UMSCHALT+LEERZEICHEN.  
  
 Weitere Informationen finden Sie unter [Konfigurieren von IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-intellisense-sql-server-management-studio.md).  
  
> [!NOTE]  
>  Die Option **Parameter Info** ist nur für den [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Abfrage-Editor und den XML-Abfrage-Editor verfügbar.  
  
  