---
title: Sys.dm_exec_distributed_request_steps (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS_TSQL
- DM_EXEC_DISTRIBUTED_REQUEST_STEPS
dev_langs: TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_distributed_request_steps
- sys.dm_exec_distributed_request_steps management view
ms.assetid: 1954541d-b716-4e03-8fcc-7022f428e01d
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4ae648f06b9224cf1545a0984e904c8845e6b88b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecdistributedrequeststeps-transact-sql"></a>Sys.dm_exec_distributed_request_steps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Enthält Informationen zu allen Schritten, die einer bestimmten PolyBase-Anforderung oder einer Abfrage zu verfassen. Eine Zeile pro abfrageschritt aufgeführt.  
  
|Spaltenname|Datentyp|Description|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**int**|Execution_id und Step_index bilden zusammen den Schlüssel für diese Ansicht. Eindeutige numerische Id der Anforderung zugeordnet ist.|Finden Sie unter-ID in [Sys. dm_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|  
|step_index|**int**|Die Position dieses Schritts in der Abfolge von Schritten, die die Anforderung bilden.|0 bis (n-1) für eine Anforderung mit n Schritten.|  
|operation_type|**vom Datentyp nvarchar(128)**|Der Typ des Vorgangs durch diesen Schritt dargestellt.|"MoveOperation", "OnOperation", "RandomIDOperation", "RemoteOperation", "ReturnOperation", "ShuffleMoveOperation", "TempTablePropertiesOperation", "DropDiagnosticsNotifyOperation", "HadoopShuffleOperation", "HadoopBroadCastOperation", "HadoopRoundRobinOperation"|  
|distribution_type|**nvarchar(32)**|Gibt an, auf dem der Schritt ausgeführt wird.|"AllComputeNodes ',' AllDistributions', 'ComputeNode', 'Distribution',"AllNodes", 'SubsetNodes', 'SubsetDistributions',' nicht angegeben".|  
|location_type|**nvarchar(32)**|Gibt an, auf dem der Schritt ausgeführt wird.|"Compute", "Head" oder "DMS". Alle Schritte zum Verschieben von Daten anzeigen "DMS".|  
|status|**nvarchar(32)**|Status dieses Schritts|"Ausstehend" "abgebrochen"Ausführen","Vollständig","Fehlgeschlagen","UndoFailed","PendingCancel",", "Rückgängig", "Abgebrochen"|  
|error_id|**nvarchar(36)**|Eindeutige Id des Fehlers bei diesem Schritt verknüpft sind, sofern vorhanden|Finden Sie die Id des [sys.dm_exec_compute_node_errors &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md), NULL, wenn kein Fehler aufgetreten ist.|  
|start_time|**datetime**|Zeitpunkt, zu dem der Schritt Ausführung begonnen hat|Kleiner oder gleich der aktuellen Uhrzeit und größer oder gleich End_compile_time der Abfrage zu der dieser Schritt gehört.|  
|end_time|**datetime**|Zeitpunkt, zu dem dieser Schritt hat die Ausführung abgeschlossen, wurde abgebrochen oder fehlerhaft.|Kleiner oder gleich der aktuellen Uhrzeit und größer oder gleich Start_time, für die Schritte in der Ausführung auf NULL festgelegt oder in die Warteschlange eingereiht.|  
|total_elapsed_time|**int**|Gesamtzeit hinzuaddiert, die die abfrageschritt, in Millisekunden ausgeführt wurde|Zwischen 0 und der Unterschied zwischen End_time und Start_time. 0 für Schritte in Warteschlange.|  
|row_count|**bigint**|Gesamtanzahl der Zeilen, die geändert oder von dieser Anforderung zurückgegeben|0 für Schritte, die nicht ändern oder Daten, Anzahl der betroffenen andernfalls Zeilen zurückgeben. -1 für DMS-Schritte festgelegt ist.|  
|Befehl|nvarchar(4000)|Enthält den vollständigen Text des Befehls dieses Schritts an.|Eine beliebige gültige Anforderungszeichenfolge für einen Schritt. Bei mehr als 4000 Zeichen abgeschnitten.|  
  
## <a name="see-also"></a>Siehe auch  
 [PolyBase, Problembehandlung mit dynamischen Verwaltungssichten](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Datenbank verbundene dynamische Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  