

```markdown
# MySQL 命令大全

## 目录
- [连接与退出](#连接与退出)
- [数据库操作](#数据库操作)
- [表操作](#表操作)
- [数据操作](#数据操作)
- [查询操作](#查询操作)
- [用户与权限管理](#用户与权限管理)
- [事务管理](#事务管理)
- [备份与恢复](#备份与恢复)
- [性能优化](#性能优化)
- [高级功能](#高级功能)

---

## 连接与退出
```sql
-- 连接到本地MySQL服务器
mysql -u root -p

-- 连接到远程MySQL服务器
mysql -h 主机名 -P 端口 -u 用户名 -p

-- 退出MySQL命令行
exit;
\q
```

---

## 数据库操作
```sql
-- 显示所有数据库
SHOW DATABASES;

-- 创建数据库
CREATE DATABASE 数据库名;

-- 删除数据库
DROP DATABASE 数据库名;

-- 切换数据库
USE 数据库名;

-- 显示当前数据库
SELECT DATABASE();
```

---

## 表操作
```sql
-- 显示当前数据库的所有表
SHOW TABLES;

-- 创建表
CREATE TABLE 表名 (
    列1 数据类型 [约束],
    列2 数据类型 [约束],
    PRIMARY KEY (列1)
);

-- 示例：创建用户表
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE
);

-- 删除表
DROP TABLE 表名;

-- 修改表结构
ALTER TABLE 表名 ADD COLUMN 列名 数据类型; -- 添加列
ALTER TABLE 表名 DROP COLUMN 列名;        -- 删除列
ALTER TABLE 表名 MODIFY COLUMN 列名 新数据类型; -- 修改列类型
ALTER TABLE 表名 RENAME TO 新表名;        -- 重命名表

-- 查看表结构
DESC 表名;
SHOW CREATE TABLE 表名;
```

---

## 数据操作
```sql
-- 插入数据
INSERT INTO 表名 (列1, 列2) VALUES (值1, 值2);

-- 批量插入
INSERT INTO 表名 (列1, 列2) VALUES (值1, 值2), (值3, 值4);

-- 更新数据
UPDATE 表名 SET 列1=新值 WHERE 条件;

-- 删除数据
DELETE FROM 表名 WHERE 条件;

-- 清空表（重置自增ID）
TRUNCATE TABLE 表名;
```

---

## 查询操作
```sql
-- 基本查询
SELECT 列1, 列2 FROM 表名 WHERE 条件;

-- 去重查询
SELECT DISTINCT 列名 FROM 表名;

-- 排序
SELECT * FROM 表名 ORDER BY 列名 ASC|DESC;

-- 分页查询
SELECT * FROM 表名 LIMIT 偏移量, 行数;
SELECT * FROM 表名 LIMIT 行数 OFFSET 偏移量;

-- 聚合函数
SELECT COUNT(*) FROM 表名;       -- 计数
SELECT AVG(列名) FROM 表名;      -- 平均值
SELECT SUM(列名) FROM 表名;      -- 求和
SELECT MAX(列名) FROM 表名;      -- 最大值
SELECT MIN(列名) FROM 表名;      -- 最小值

-- 分组查询
SELECT 列名, COUNT(*) FROM 表名 GROUP BY 列名 HAVING 条件;

-- 连接查询
SELECT * FROM 表1 INNER JOIN 表2 ON 表1.列 = 表2.列; -- 内连接
SELECT * FROM 表1 LEFT JOIN 表2 ON 表1.列 = 表2.列;  -- 左连接
SELECT * FROM 表1 RIGHT JOIN 表2 ON 表1.列 = 表2.列; -- 右连接
```

---

## 用户与权限管理
```sql
-- 创建用户
CREATE USER '用户名'@'主机' IDENTIFIED BY '密码';

-- 删除用户
DROP USER '用户名'@'主机';

-- 修改密码
ALTER USER '用户名'@'主机' IDENTIFIED BY '新密码';

-- 授予权限
GRANT 权限 ON 数据库.表 TO '用户名'@'主机';
-- 示例：授予所有权限
GRANT ALL PRIVILEGES ON *.* TO '用户名'@'localhost';

-- 撤销权限
REVOKE 权限 ON 数据库.表 FROM '用户名'@'主机';

-- 刷新权限
FLUSH PRIVILEGES;

-- 查看用户权限
SHOW GRANTS FOR '用户名'@'主机';
```

---

## 事务管理
```sql
-- 开启事务
START TRANSACTION;
BEGIN;

-- 提交事务
COMMIT;

-- 回滚事务
ROLLBACK;

-- 设置自动提交
SET autocommit = 0; -- 关闭自动提交
SET autocommit = 1; -- 开启自动提交
```

---

## 备份与恢复
```bash
# 备份整个数据库
mysqldump -u 用户名 -p 数据库名 > 备份文件.sql

# 恢复数据库
mysql -u 用户名 -p 数据库名 < 备份文件.sql

# 备份单个表
mysqldump -u 用户名 -p 数据库名 表名 > 备份文件.sql
```

---

## 性能优化
```sql
-- 查看执行计划
EXPLAIN SELECT * FROM 表名 WHERE 条件;

-- 创建索引
CREATE INDEX 索引名 ON 表名 (列名);

-- 删除索引
DROP INDEX 索引名 ON 表名;

-- 优化表（整理碎片）
OPTIMIZE TABLE 表名;

-- 分析表（更新索引统计信息）
ANALYZE TABLE 表名;
```

---

## 高级功能
```sql
-- 存储过程
DELIMITER //
CREATE PROCEDURE 存储过程名()
BEGIN
    -- SQL语句
END //
DELIMITER ;

-- 触发器
CREATE TRIGGER 触发器名 BEFORE|AFTER INSERT|UPDATE|DELETE ON 表名
FOR EACH ROW
BEGIN
    -- 触发时执行的SQL
END;

-- 视图
CREATE VIEW 视图名 AS SELECT 列1, 列2 FROM 表名 WHERE 条件;

-- 事件调度器
SHOW VARIABLES LIKE 'event_scheduler'; -- 查看事件调度器状态
SET GLOBAL event_scheduler = ON;       -- 开启事件调度器

-- 创建定时任务
CREATE EVENT 事件名
ON SCHEDULE EVERY 1 DAY
DO
    -- 执行的SQL语句
```

---

**提示**：部分命令可能需要管理员权限，使用时请确保有足够的权限。
```