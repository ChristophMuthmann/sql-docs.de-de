---
title: Verweisen auf die ADO-Bibliotheken In Visual Basic 6-Anwendungen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology: drivers
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- libraries [ADO]
- referencing libraries in a Visual Basic application[ADO]
- ADO, libraries
ms.assetid: cfd37a82-aad2-41cd-8d13-1566c43d95f0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 20044ab8bc57f8c943a26457cd165d95afcd077f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="referencing-the-ado-libraries-in-a-visual-basic-6-application"></a>Verweisen auf die ADO-Bibliotheken In Visual Basic 6-Anwendungen
Um die ADO-Bibliotheken in eine Microsoft Visual Basic 6-Anwendung importieren, müssen Sie einen Verweis in Visual Basic-Projekt festlegen.  
  
### <a name="to-set-a-reference-to-the-ado-libraries-in-a-visual-basic-project"></a>Einen Verweis auf die ADO-Bibliotheken in Visual Basic-Projekt festlegen  
  
1.  Erstellen Sie ein neues oder öffnen Sie ein vorhandenes Visual Basic-Projekt.  
  
2.  Klicken Sie auf die **Projekt** Menüelement und wählen Sie dann **Verweise...**  aus dem Dropdown-Menü Bereich.  
  
3.  Von **Verfügbare Verweise**, aktivieren Sie das Kontrollkästchen für **Microsoft ActiveX Data Objects *ist n.n* Bibliothek**, wobei ***ist n.n*** stellt die neuesten Versionsnummer. Die **Speicherort** Feld unten sollten Identifizieren Ihrer Wahl als *$installDir\msado15.dll*, wobei *$installDir* bezeichnet den Pfad des Verzeichnisses, in dem die ADO-Bibliothek wurde installiert.  
  
4.  Wenn Sie ADO MD verwenden möchten, wiederholen Sie Schritt 3 auswählen **Microsoft ActiveX Data Objects (Multi-dimensional) *ist n.n* Bibliothek**. Die **Speicherort** Feld sollte diese Auswahl als identifizieren *$installDir\msadomd.dll*.  
  
5.  Wenn Sie ADOX verwenden möchten, wiederholen Sie Schritt 3 auswählen **Microsoft ADO automatischer *ist n.n* für DDL-Befehle und Sicherheit**. Die **Speicherort** Feld sollte diese Auswahl als identifizieren *$installDir\msadox.dll*.  
  
6.  Klicken Sie auf **OK** abgeschlossen, die Verweise festlegen.  
  
## <a name="backward-compatibility"></a>Abwärtskompatibilität  
 Installieren von ADO wird außerdem die folgenden Typbibliotheken früherer Versionen kopiert:  
  
-   *msado27.tlb*, Version 2.7 ADO-Typbibliothek  
  
-   *msado26.tlb*, ADO 2.6-Typbibliothek  
  
-   *msado25.tlb*, ADO 2.5-Typbibliothek  
  
-   *MSADO21*, 2,1 ADO-Typbibliothek  
  
-   *msado20.tlb*, ADO-2.0-Typbibliothek  
  
 Wenn Ihre Anwendung diese ADO-Bibliotheken aus Gründen der Abwärtskompatibilität verwenden muss, müssen Sie die entsprechende Version der Typbibliothek zu importieren. Führen Sie dazu die Verfahren im vorherigen Abschnitt, und Ersetzen Sie dabei *"MSADO15.dll"* von *msadoXX.tlb*, wobei *XX* stellt die Versionsnummer, die Sie importieren müssen.
