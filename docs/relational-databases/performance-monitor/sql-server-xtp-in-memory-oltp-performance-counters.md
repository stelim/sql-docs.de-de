---
title: Leistungsindikatoren für SQL Server XTP (In-Memory OLTP) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a701f2354b23d0f6936124ae2c00c1efd812a2f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746968"
---
# <a name="sql-server-xtp-in-memory-oltp-performance-counters"></a>Leistungsindikatoren für SQL Server XTP (In-Memory OLTP)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet Objekte und Leistungsindikatoren, die vom Systemmonitor zum Überwachen der In-Memory OLTP-Aktivität verwendet werden können. Die Objekte und Leistungsindikatoren sind für alle Instanzen einer bestimmten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Computer freigegeben, beginnend mit [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 In der Vergangenheit begann die Namen von Objekten und Leistungsindikatoren mit *XTP*, wie in **XTP-Cursors**. Ab jetzt beginnen die Namen mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]und entsprechen folgendem Muster:  
  
-   **SQL Server** *\<Version>* **XTP-Cursor**  
  
 Der Wert für *\<Version>* ist z.B. 2016.  
  
##  <a name="SQLServerPOs"></a> SQL Server-XTP-Leistungsobjekte  
 In der folgenden Tabelle werden diese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Leistungsobjekte beschrieben.  
  
|Leistungsobjekt|und Beschreibung|  
|------------------------|-----------------|  
|[SQL Server-XTP-Cursor](../../relational-databases/performance-monitor/sql-server-xtp-cursors.md)|Das Leistungsobjekt für SQL Server-XTP-Cursor enthält Leistungsindikatoren für interne Cursor der In-Memory-OLTP-Engine. Cursor sind die Bausteine auf unterer Ebene, die die In-Memory-OLTP-Engine zur Verarbeitung von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfragen verwendet. Daher können Sie diese in der Regel nicht direkt steuern.|  
|[SQL Server XTP-Datenbanken](../../relational-databases/performance-monitor/sql-server-xtp-databases.md)|Das Leistungsobjekt „SQL Server XTP-Datenbanken“ stellt spezielle Leistungsindikatoren für In-Memory-OLTP-Datenbanken bereit.|  
|[SQL Server-XTP Garbage Collection](../../relational-databases/performance-monitor/sql-server-xtp-garbage-collection.md)|Das SQL Server-XTP-Leistungsobjekt für die Garbage Collection enthält Leistungsindikatoren für die Garbage Collection der In-Memory-OLTP-Engine.|  
|[SQL Server 2016 XTP IO Governor](../../relational-databases/performance-monitor/sql-server-xtp-io-governor.md)|Das Leistungsobjekt „SQL Server XTP IO Governor“ enthält Leistungsindikatoren, die sich auf den In-Memory OLTP IO Rate Governor beziehen.|
|[SQL Server XTP-Phantomprozessor](../../relational-databases/performance-monitor/sql-server-xtp-phantom-processor.md)|Das SQL Server-XTP-Leistungsobjekt „Phantomprozessor“ enthält Leistungsindikatoren, die sich auf den für das zur Phantomverarbeitung verwendete Subsystem der XTP-Engine beziehen. Diese Komponente ist dafür verantwortlich, Phantomzeilen in Transaktionen zu erkennen, die auf der SERIALIZABLE-Isolationsstufe ausgeführt werden.|  
|[SQL Server-XTP-Speicher](../../relational-databases/performance-monitor/sql-server-xtp-storage.md)|Das Leistungsobjekt „SQL Server-XTP-Speicher“ enthält Leistungsindikatoren für den In-Memory-OLTP-Speicher in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[XTP-Transaktionsprotokoll für SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transaction-log.md)|Das Leistungsobjekt „SQL Server-XTP-Transaktionsprotokoll“ enthält Leistungsindikatoren für die In-Memory-OLTP-Transaktionsprotokollierung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[SQL Server-XTP-Transaktionen](../../relational-databases/performance-monitor/sql-server-xtp-transactions.md)|Das Leistungsobjekt „SQL Server-XTP-Transaktionen“ enthält Leistungsindikatoren für die In-Memory-OLTP-Engine-Transaktionen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  
