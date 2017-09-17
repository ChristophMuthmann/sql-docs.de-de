---
title: 'Schritt 1: Konfigurieren von Pymssql Python-Entwicklungsumgebung | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0a1932b41ada3469deed6d36a3c68c3827687cc5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Schritt 1: Konfigurieren der Entwicklungsumgebung für Pymssql Python-Entwicklung
Sie müssen Ihre Entwicklungsumgebung mit den Voraussetzungen zu konfigurieren, um die Entwicklung einer Anwendung mithilfe der Python-Treiber für SQL Server.    
  
Beachten Sie, dass die Python-SQL-Treiber das TDS-Protokoll verwenden, die standardmäßig in SQL Server und Azure SQL-Datenbank aktiviert ist.  Es ist keine zusätzliche Konfiguration erforderlich.  
  
## <a name="windows"></a>Windows  
  
1. **Installieren Sie Python-Laufzeit und pip-Paket-manager**  
a. Wechseln Sie zu ["Python.org"](https://www.python.org/downloads/)  
b. Klicken Sie auf den entsprechenden Windows Installer-Msi-Link.   
c. Einmal heruntergeladenen führen Sie die MSI-Datei zum Installieren von Python-Laufzeit  
  
2. **Herunterladen von Pymssql Modul** aus [hier](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Stellen Sie sicher, dass Sie die richtige Whl-Datei auszuwählen.  Zum Beispiel: Wählen Sie bei Verwendung von Python 2.7 auf einem 64-Bit-Computer: Pymssql‑2.1.1‑cp27‑none‑win_amd64.whl. Sobald Sie herunterladen die Datei .whl platzieren Sie es in den Ordner "c:" / Python27.  
      
3. **Öffnen von cmd.exe**  
  
4. **Installieren Sie Pymssql-Modul**     
    Beispielsweise bei Verwendung von Python 2.7 auf einem 64-Bit-Computer:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Installieren Sie Python-Laufzeit und pip-Paket-Manager** Python vorinstallierte stammen, auf die meisten Ubuntu-Distributionen.  Wenn Ihr Computer nicht installierte Python verfügt, erhalten Sie entweder Download der Quelle Tarball aus ["Python.org"](https://www.python.org/downloads/) und lokal zu erstellen, oder können Sie die Paket-Manager:  
```  
> sudo apt-get install python   
```  
  
2.  **Geöffneten Terminaldienste**  
  
3.  **Installieren Sie Pymssql-Modul und Abhängigkeiten**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Installieren Sie Python-Laufzeit und pip-Paket-manager**  
a. Wechseln Sie zu ["Python.org"](https://www.python.org/downloads/)  
b. Klicken Sie auf den entsprechenden Mac Installer Pkg-Link.   
c. Einmal heruntergeladenen Ausführen der Pkg Python-Laufzeit installieren  
  
2.  **Geöffneten Terminaldienste**  
  
3. **Installieren von Homebrew-Paket-manager**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Installieren Sie FreeTDS-Modul**  
```  
> brew install FreeTDS  
```  
  
5.  **Installieren Sie Pymssql-Modul**  
```  
> sudo -H pip install pymssql  
```
