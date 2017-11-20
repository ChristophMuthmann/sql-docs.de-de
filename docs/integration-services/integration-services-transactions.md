---
title: Integration Services-Transaktionen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7355d98c342052997441c2013e056b0453962c5a
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-transactions"></a>Integration Services-Transaktionen
  Pakete verwenden Transaktionen, um die von Tasks ausgeführten Datenbankaktionen in unteilbare Einheiten einzubinden und somit die Integrität der Daten zu erhalten. Alle [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Containertypen – Pakete, For-Schleifen-Container, Foreach-Schleifen-Container und Sequenzcontainer sowie die Taskhosts, die die einzelnen Tasks kapseln – können so konfiguriert werden, dass sie Transaktionen verwenden. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] stellt für das Konfigurieren von Transaktionen drei Optionen bereit: **NotSupported**, **Supported**und **Required**.  
  
-   **Required** bedeutet, dass der Container eine Transaktion startet, es sei denn, eine andere Transaktion ist bereits durch den übergeordneten Container gestartet worden. Wenn bereits eine Transaktion vorhanden ist, nimmt der Container an dieser Transaktion teil. Wenn beispielsweise ein Paket, für das die Unterstützung von Transaktionen nicht konfiguriert wurde, einen Sequenzcontainer enthält, der die Option **Required** verwendet, startet der Sequenzcontainer eine eigene Transaktion. Wenn das Paket jedoch mit der Option **Required** konfiguriert wurde, nimmt der Sequenzcontainer an der Pakettransaktion teil.  
  
-   **Supported** bedeutet, dass der Container keine Transaktion startet, sondern an der durch den übergeordneten Container gestarteten Transaktion teilnimmt. Wenn beispielsweise ein Paket mit vier SQL ausführen-Tasks eine Transaktion startet und alle vier Tasks die Option **Supported** verwenden, wird für die entsprechenden Datenbankaktualisierungen ein Rollback ausgeführt, wenn einer der Tasks einen Fehler auslöst. Wenn das Paket keine Transaktion startet, sind die vier SQL ausführen-Tasks nicht durch eine Transaktion gebunden, und das Rollback wird lediglich für den fehlgeschlagenen Task ausgeführt.  
  
-   **NotSupported** bedeutet, dass der Container keine Transaktion startet, und auch an keiner vorhandenen Transaktion teilnimmt. Eine von einem übergeordneten Container gestartete Transaktion hat keine Auswirkung auf untergeordnete Container, deren Konfiguration keine Transaktionen zulässt. Wenn ein Paket beispielsweise so konfiguriert ist, dass es eine Transaktion startet, und ein For-Schleifen-Container des Pakets die Option **NotSupported** verwendet, kann für keinen der Tasks in der For-Schleife ein Rollback ausgeführt werden, falls ein Fehler auftritt.  
  
 Sie konfigurieren Transaktionen, indem Sie für den Container die TransactionOption-Eigenschaft festlegen. Diese Eigenschaft können Sie mithilfe des Fensters **Eigenschaften** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]oder programmgesteuert festlegen.  
  
> [!NOTE]  
>  Mit der **TransactionOption** -Eigenschaft wird festgelegt, ob der von einem Container angeforderte Wert der **IsolationLevel** -Eigenschaft angewendet wird. Weitere Informationen finden Sie in der Beschreibung der **IsolationLevel** -Eigenschaft im Thema [Festlegen von Paketeigenschaften](../integration-services/set-package-properties.md).  
  
## <a name="configure-a-package-to-use-transactions"></a>Konfigurieren eines Pakets für die Verwendung von Transaktionen
Beim Konfigurieren eines Pakets zur Verwendung von Transaktionen stehen zwei Optionen zur Verfügung:  
  
-   Eine einzelne Transaktion für das Paket. In diesem Fall wird diese Transaktion durch das Paket selbst *initiiert* , während einzelne Tasks und Container des Pakets an dieser einzelnen Transaktion beteiligt sind.  
  
-   Mehrere Transaktionen im Paket. In diesem Fall unterstützt das Paket Transaktionen, die Transaktionen werden jedoch tatsächlich von einzelnen Tasks und Containern im Paket initiiert.  
  
 Im Folgenden wird beschrieben, wie beide Optionen konfiguriert werden.  
  
### <a name="configure-a-package-to-use-a-single-transaction"></a>Konfigurieren eines Pakets zur Verwendung einer einzelnen Transaktions  
 Mit dieser Option initiiert das Paket selbst eine einzelne Transaktion. Um das Paket zum Initiieren dieser Transaktion zu konfigurieren, legen Sie die TransactionOption-Eigenschaft auf **Required**fest.  
  
 Danach tragen Sie bestimmte Tasks und Container in dieser einzelnen Transaktion ein. Zum Eintragen eines Tasks oder Containers in einer Transaktion legen Sie die TransactionOption-Eigenschaft dieses Tasks oder Containers auf **Supported**fest.  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, für das Sie die Verwendung einer Transaktion konfigurieren möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Klicken Sie mit der rechten Maustaste an einer beliebigen Stelle im Hintergrund der Entwurfsoberfläche der Ablaufsteuerung, und klicken Sie anschließend auf **Eigenschaften**.  
  
5.  Legen Sie im Fenster **Eigenschaften** die TransactionOption-Eigenschaft auf **Required**fest.  
  
6.  Klicken Sie auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** mit der rechten Maustaste auf den Task oder den Container, für den Sie die Transaktion registrieren möchten, und klicken Sie auf **Eigenschaften**.  
  
7.  Legen Sie im Fenster **Eigenschaften** die TransactionOption-Eigenschaft auf **Supported**fest.  
  
    > [!NOTE]  
    >  Um eine Verbindung in einer Transaktion einzutragen, registrieren Sie die Tasks, die die Verbindung verwenden, für die Transaktion. Weitere Informationen finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
8.  Wiederholen Sie die Schritte 6 und 7 für alle Tasks und Container, für die Sie die Transaktion registrieren möchten.  
  
### <a name="configure-a-package-to-use-multiple-transactions"></a>Konfigurieren eines Pakets Verwendung mehrerer Transaktionen  
 Mit dieser Option unterstützt das Paket selbst Transaktionen, startet jedoch keine Transaktion. Um das Paket zur Unterstützung dieser Transaktion zu konfigurieren, legen Sie die TransactionOption-Eigenschaft auf **Supported**fest.  
  
 Danach konfigurieren Sie die gewünschten Tasks und Container im Paket, um Transaktionen zu initiieren oder an Transaktionen teilzunehmen. Zum Konfigurieren eines Tasks oder Containers zum Initiieren einer Transaktion legen Sie die TransactionOption-Eigenschaft dieses Tasks oder Containers auf **Required**fest.   
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, das Sie für die Verwendung von Transaktionen konfigurieren möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Klicken Sie mit der rechten Maustaste an einer beliebigen Stelle im Hintergrund der Entwurfsoberfläche der Ablaufsteuerung, und klicken Sie anschließend auf **Eigenschaften**.  
  
5.  Legen Sie im Fenster **Eigenschaften** die TransactionOption-Eigenschaft auf **Supported**fest.  
  
    > [!NOTE]  
    >  Das Paket unterstützt Transaktionen, aber die Transaktionen werden von Tasks oder Containern im Paket gestartet.  
  
6.  Klicken Sie auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** mit der rechten Maustaste auf den Task oder den Container im Paket, für den Sie eine Transaktion starten möchten, und klicken Sie auf **Eigenschaften**.  
  
7.  Legen Sie im Fenster **Eigenschaften** die TransactionOption-Eigenschaft auf **Required**fest.  
  
8.  Wenn eine Transaktion von einem Container gestartet wird, klicken Sie mit der rechten Maustaste auf den Task oder den Container, für den Sie die Transaktion registrieren möchten, und klicken Sie auf **Eigenschaften**.  
  
9. Legen Sie im Fenster **Eigenschaften** die TransactionOption-Eigenschaft auf **Supported**fest.  
  
    > [!NOTE]  
    >  Um eine Verbindung in einer Transaktion einzutragen, registrieren Sie die Tasks, die die Verbindung verwenden, für die Transaktion. Weitere Informationen finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
10. Wiederholen Sie die Schritte 6 bis 9 für alle Tasks und Container, die eine Transaktion initiieren.  

## <a name="multiple-transactions-in-a-package"></a>Mehrere Transaktionen in einem Paket
Es ist möglich, dass ein Paket nicht miteinander verbundene Transaktionen in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paket enthält. Immer wenn ein Container in der Mitte einer geschachtelten Hierarchie von Containern keine Transaktionen unterstützt, starten die Container, die sich in der Hierarchie oberhalb oder unterhalb des Containers befinden, separate Transaktionen, wenn sie für die Unterstützung von Transaktionen konfiguriert sind. Die Transaktionen führen einen Commit oder Rollback aus, und zwar nacheinander und beginnend beim innersten Task innerhalb der geschachtelten Containerhierarchie bis zum Paket. Nachdem die innere Transaktion einen Commit ausgeführt hat, erfolgt jedoch kein Rollback, wenn eine äußere Transaktion abgebrochen wird.  
  
### <a name="example-of-multiple-transactions-in-a-package"></a>Beispiel für mehrere Transaktionen in einem Paket 
 Ein Paket enthält z. B. einen Sequenzcontainer, der zwei Foreach-Schleifencontainer enthält, und jeder Container enthält zwei SQL Ausführen-Tasks. Der Sequenzcontainer und die Execute SQL-Tasks unterstützen Transaktionen, die Foreach-Schleifencontainer hingegen nicht. In diesem Beispiel startet jeder Execute SQL-Task seine eigene Transaktion und führt keinen Rollback aus, wenn die Transaktion auf dem Sequenztask abgebrochen wurde.  
  
 Die TransactionOption-Eigenschaften des Sequenzcontainers, der Foreach-Schleifencontainer und die Tasks „SQL ausführen“ sind folgendermaßen festgelegt:  
  
-   Die TransactionOption-Eigenschaft des Sequenzcontainers ist auf **Required**festgelegt.  
  
-   Die TransactionOption-Eigenschaften der Foreach-Schleifencontainer sind auf **NotSupported**festgelegt.  
  
-   Die TransactionOption-Eigenschaften der Tasks „SQL ausführen“ sind auf **Required**festgelegt.  
  
 Das folgende Diagramm zeigt die fünf nicht miteinander verbundenen Transaktionen im Paket. Eine Transaktion wird durch den Sequenzcontainer gestartet, und vier Transaktionen werden durch die SQL Ausführen-Tasks gestartet.  
  
 ![Implementierung von mehreren Transaktionen](../integration-services/media/mw-dts-trans2.gif "Implementierung mehrerer Transaktionen")  
 
## <a name="inherited-transactions"></a>Vererbte Transaktionen
 Ein Paket kann mithilfe des Tasks "Paket ausführen" ein anderes Paket ausführen. Das untergeordnete Paket, d. h. das von dem Task Paket ausführen ausgeführte Paket, kann seine eigene Pakettransaktion erstellen oder aber die Pakettransaktion des übergeordneten Pakets erben.  
  
 Ein untergeordnetes Paket erbt die übergeordnete Pakettransaktion, wenn die beiden folgenden Bedingungen erfüllt sind:  
  
-   Das Paket wird durch einen Task Paket ausführen aufgerufen.  
  
-   Der Task Paket ausführen, der das Paket aufgerufen hat, nimmt ebenfalls an der übergeordneten Pakettransaktion teil.  
  
 Container und Tasks des untergeordneten Pakets können nicht an der übergeordneten Pakettransaktion teilnehmen, es sei denn, das untergeordnete Paket nimmt selbst an der Transaktion teil.  
  
### <a name="example-of-inherited-transactions"></a>Beispiel für vererbte Transaktionen  
 Im folgenden Diagramm sind drei Pakete zu sehen, die Transaktionen verwenden. Jedes Paket enthält zahlreiche Tasks. Um das Verhalten der Transaktionen zu verdeutlichen, werden nur die Tasks Paket ausführen gezeigt. Das Paket A führt die Pakete B und C aus. Das Paket B wiederum führt die Pakete D und E aus, und das Paket C führt das Paket F aus.  
  
 Die Pakete und Tasks besitzen die folgenden Transaktionsattribute:  
  
-   **TransactionOption** ist für die Pakete A und C auf **Required** festgelegt.  
  
-   **TransactionOption** ist für die Pakete B und D sowie für die Tasks Paket ausführen B, Paket ausführen D und Paket ausführen F auf **Supported** festgelegt.  
  
-   **TransactionOption** ist für das Paket E sowie für die Tasks Paket ausführen C und Paket ausführen E auf **NotSupported** festgelegt.  
  
 ![Fluss von vererbten Transaktionen](../integration-services/media/mw-dts-executepack.gif "Fluss von vererbten Transaktionen")  
  
 Nur die Pakete B, D und F können Transaktionen von ihren übergeordneten Paketen erben.  
  
 Die Pakete B und D erben die Transaktion, die von Paket A gestartet wurde.  
  
 Das Paket F erbt die Transaktion, die von Paket C gestartet wurde.  
  
 Die Pakete A und C steuern ihre eigenen Transaktionen.  
  
 Das Paket E verwendet keine Transaktionen.  
 
  
## <a name="external-resources"></a>Externe Ressourcen  
  
-   Blog-Artikel [How to Use Transactions in SQL Server Integration Services (SSIS)](http://go.microsoft.com/fwlink/?LinkId=157783)(Verwenden von Transaktionen in SQL Server Integration Services (SSIS)) unter www.mssqltips.com  
  
## <a name="see-also"></a>Siehe auch  
 [Vererbte Transaktionen](http://msdn.microsoft.com/library/90db5564-d41e-4cfe-8c9e-4e68d41eff1c)   
 [Mehrere Transaktionen](http://msdn.microsoft.com/library/c3664a94-be89-40c0-a3a0-84b74a7fedbe)  
  
  

