# SVN

1. 创建仓库、管理用户、备份仓库
2. 检出  checkout
3. 提交  commit
4. 更新  update
5. 版本回退 update to reversion

### 解决冲突

> 同一个文件的同一位置被写入不同的内容（分支合并，都保留

#### wc.db任务队列

~~~~bash
error:Previous operation has not finished run ==>cleanup
无效时
sqlite.exe
sqlite3 .svn/wc.db "select * from work_queue"
~~~~

