### 使用 json-server 模拟后台数据库

1. 创建 `data` 文件 创建 `data ` 文件

```json
{
  "posts": [
    {
      "id": "1",
      "title": "我是 data.json"
    }
  ]
}
```

2. 在 `data.json` 的文件夹中打开 `Git Bash`
3. 输入命令 `json-server --watch data.json -p 3000`
4. 输入网址查看 `http://localhost:3000/posts`

- 在 `vue` 组件中使用

1. 先在 `vue` 中安装依赖 `axios` (大概 48Mb)
2. 在当前组件中 `import axios from "axios";`
3. 方法如下

```html
<div>
  <ul v-if="list.length">
    <li v-for="post in list" :key="post.id">{{ post.id }}</li>
    <p>{{list[0].id}}</p>
  </ul>
</div>
```

```vue
<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      list: [],
    };
  },
  created() {
    axios.get("http://localhost:3000/posts").then((res) => {
      this.list = res.data;
      console.log(this.list);
    });
  },
};
</script>
```
![image](71A8DCBB0D47488CA0CEBC30D3971640)