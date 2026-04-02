# aicode
AI 测试代码

## 文档目录树组件 (DocTree)

基于 Alpine.js + Tailwind CSS + Sortable.js 的文档目录树 Web 组件。

### 功能

- ✅ 多级树形显示，展开 / 收拢切换
- ✅ 双击节点修改名称
- ✅ 右键菜单：新增子节点、新增同级、复制、重命名、删除
- ✅ 拖拽移动节点（排序 / 变更父节点）
- ✅ 数据超过容器高度时显示滚动条
- ✅ API 接口可配置化（通过 `syncData` 函数）
- ✅ 与后端 API 同步通信

### 使用方式

```html
<div id="my-tree"></div>

<script>
  const config = {
    // 数据同步函数
    syncData: async (action, reqData) => {
      // action: 'init' | 'add_child' | 'add_sibling' | 'delete' | 'rename' | 'copy' | 'move'
      const resp = await fetch('/api/tree', {
        method: 'POST',
        body: JSON.stringify({ action, ...reqData })
      });
      return await resp.json();
      // 返回格式: { tree: [...], error: "", success: true }
    },

    // 容器样式
    container: {
      maxHeight: '500px',
      width: '300px'
    },

    // 是否启用拖拽
    enableDrag: true
  };

  DocTree.init('#my-tree', config);
</script>
```

### 树节点数据结构

```js
{
  id: "1",           // 节点唯一标识
  name: "文档名称",   // 节点显示名称
  children: []       // 子节点数组
}
```

### 演示

直接在浏览器中打开 `doc-tree.html` 即可查看演示效果（使用模拟数据）。
