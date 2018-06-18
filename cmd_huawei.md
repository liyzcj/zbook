# HUAWEI Command

Some commands of work.

## HACS

```shell
# 冻结双机
crm configure property maintenance-mode=true
# 冻结单个资源
crm resource unmanage <rsc>
# 切换资源
crm resource move <rsc> [<node>] [force]
```

#### 查询和修改资源参数
| Command                                      | Function |
| -------------------------------------------- | -------- |
| crm configure show <rsc>                     | 查询     |
| crm resource param <rsc> set <param> <value> | 修改     |
| crm resource param <rsc> delete <param>      | 删除     |

​	