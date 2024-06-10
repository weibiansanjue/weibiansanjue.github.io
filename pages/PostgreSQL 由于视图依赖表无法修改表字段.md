tags:: [[tagPostgreSQL]]

- 场景与问题描述
	- 场景：修改表字段长度
	- >cannot alter type of a column used by a view or rule
	  >rule _RETURN on view 视图名 depends on column "字段名"
- 数据库
	- PostgreSQL 9.4.6
	- Kingbase v8r6/r7
- PostgreSQL 系统表
	- [pg_attribute](http://postgres.cn/docs/9.6/catalog-pg-attribute.html)
	- [pg_class](http://postgres.cn/docs/9.6/catalog-pg-class.html)
- 查询
	- ```sql
	  select 
	    relname       -- 表（视图）名
	    , attname     -- 字段名
	    , attnum
	    , attrelid
	    , atttypid
	    , atttypmod   -- 字段长度
	  from
	    pg_catalog.pg_class pclass
	    left join pg_catalog.pg_attribute attr on pclass."oid" = attr.attrelid
	  where 
	    relname = ''  -- 表（视图）名
	  --  and attname = ''  -- 字段名
	  ;
	  ```
- 修改字段长度
	- ```sql
	  update
	    pg_catalog.pg_attribute 
	  set
	    atttypmod = xxx  -- 设置字段长度
	  -- select relname, attname, attnum, attrelid, atttypid, atttypmod 
	  -- from pg_catalog.pg_class pclass
	  --   left join pg_catalog.pg_attribute attr on pclass."oid" = attr.attrelid
	  where
	    attrelid in (select oid from pg_catalog.pg_class where relname = '' )  -- 表名
	    and attname = ''  -- 字段名
	  ;
	  ```