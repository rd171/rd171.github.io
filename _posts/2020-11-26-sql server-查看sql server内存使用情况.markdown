﻿---
layout: post
title:  "sql server-查看sql server内存使用情况"
date:   2020-11-26 19:00:00 +0200
categories: sql server
---

-- 查询SqlServer总体的内存使用情况   
select      type   
        , sum(virtual_memory_reserved_kb) VM_Reserved   
        , sum(virtual_memory_committed_kb) VM_Commited   
        , sum(awe_allocated_kb) AWE_Allocated   
        , sum(shared_memory_reserved_kb) Shared_Reserved   
        , sum(shared_memory_committed_kb) Shared_Commited   
        --, sum(single_pages_kb)    --SQL2005、2008   
        --, sum(multi_pages_kb)        --SQL2005、2008   
from    sys.dm_os_memory_clerks   
group by type   
order by type   


-- 查询当前数据库缓存的所有数据页面，哪些数据表，缓存的数据页面数量   
-- 从这些信息可以看出，系统经常要访问的都是哪些表，有多大？   
select p.object_id, object_name=object_name(p.object_id), p.index_id,    buffer_pages=count(*)   
from sys.allocation_units a,   
    sys.dm_os_buffer_descriptors b,   
    sys.partitions p   
where a.allocation_unit_id=b.allocation_unit_id   
    and a.container_id=p.hobt_id   
    and b.database_id=db_id()   
group by p.object_id,p.index_id   
order by buffer_pages desc   


-- 查询缓存的各类执行计划，及分别占了多少内存   
-- 可以对比动态查询与参数化SQL（预定义语句）的缓存量   
select    cacheobjtype   
        , objtype   
        , sum(cast(size_in_bytes as bigint))/1024 as size_in_kb   
        , count(bucketid) as cache_count   
from    sys.dm_exec_cached_plans   
group by cacheobjtype, objtype   
order by cacheobjtype, objtype   


-- 查询缓存中具体的执行计划，及对应的SQL   
-- 将此结果按照数据表或SQL进行统计，可以作为基线，调整索引时考虑   
-- 查询结果会很大，注意将结果集输出到表或文件中   
SELECT  usecounts ,   
        refcounts ,   
        size_in_bytes ,   
        cacheobjtype ,   
        objtype ,   
        TEXT   
FROM    sys.dm_exec_cached_plans cp   
        CROSS APPLY sys.dm_exec_sql_text(plan_handle)   
ORDER BY objtype DESC ;   
GO   
