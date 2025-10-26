本文档基于 [官方 API 文档](https://coddingtonbear.github.io/obsidian-local-rest-api/)，将各主要接口的功能、参数及调用方式整理成表，以便于快速查阅和集成。

**通用说明**:
*   **`{path}`**: 表示从 Vault 根目录开始的**相对路径**，例如 `My Notes/My First Note.md`。
*   **认证**: 所有示例中的 `YOUR_API_KEY` 都需要替换为您在插件中获取的实际 API Key。

---

### Vault (文件与目录操作)

| Method | Endpoint | Description | Parameters | Example Call |
| :--- | :--- | :--- | :--- | :--- |
| `GET` | `/vault/` | 获取 Vault 中所有的文件和文件夹列表。 | **无** | `curl -H "Authorization: Bearer YOUR_API_KEY" http://127.0.0.1:27123/vault/` |
| `GET` | `/vault/{path}` | 读取指定路径的文件内容。 | **Path**: `{path}` - 文件的完整相对路径。 | `curl -H "Authorization: Bearer YOUR_API_KEY" http://127.0.0.1:27123/vault/My%20Folder/My%20Note.md` |
| `POST` | `/vault/{path}` | 创建一个新文件或完全覆盖一个已存在的文件。 | **Path**: `{path}`<br>**Body**: 文件的原始文本内容 (Raw Text)。 | `curl -X POST -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: text/plain" -d "# New Note" http://127.0.0.1:27123/vault/NewNote.md` |
| `PATCH` | `/vault/{path}` | 在现有文件内容的开头或结尾追加文本。 | **Path**: `{path}`<br>**Body**: JSON 对象，包含 `action` (`"append"` 或 `"prepend"`) 和 `data` (要添加的文本)。 | `curl -X PATCH -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"action": "append", "data": "\n\n## Appended Content"}' http://127.0.0.1:27123/vault/ExistingNote.md` |
| `DELETE` | `/vault/{path}` | 删除指定路径的文件或空的文件夹。 | **Path**: `{path}` - 要删除的文件或文件夹的相对路径。 | `curl -X DELETE -H "Authorization: Bearer YOUR_API_KEY" http://127.0.0.1:27123/vault/NoteToDelete.md` |

---

### Commands (命令面板操作)

| Method | Endpoint | Description | Parameters | Example Call |
| :--- | :--- | :--- | :--- | :--- |
| `GET` | `/commands/` | 获取 Obsidian 中所有可用的命令及其 ID。 | **无** | `curl -H "Authorization: Bearer YOUR_API_KEY" http://127.0.0.1:27123/commands/` |
| `POST` | `/commands/{command-id}` | 执行一个指定的命令。 | **Path**: `{command-id}` - 从 `/commands/` 接口获取的命令 ID。 | `curl -X POST -H "Authorization: Bearer YOUR_API_KEY" http://127.0.0.1:27123/commands/app%3Aopen-settings` |

---

### Periodic Notes (周期性笔记)

此功能需要您已安装并配置 `Periodic Notes` 插件。

| Method | Endpoint | Description | Parameters | Example Call |
| :--- | :--- | :--- | :--- | :--- |
| `GET` | `/periodic/` | 获取所有类型的周期性笔记列表。 | **Query**: `?type=` 可选值为 `daily`, `weekly`, `monthly`, `quarterly`, `yearly`。 | `curl -H "Authorization: Bearer YOUR_API_KEY" http://127.0.0.1:27123/periodic/?type=daily` |
| `POST` | `/periodic/daily/` | 创建或打开今天的日报。 | **Body** (可选): JSON 对象，如 `{"data": "# My Content"}`，用于写入内容。 | `curl -X POST -H "Authorization: Bearer YOUR_API_KEY" http://127.0.0.1:27123/periodic/daily/` |
| `GET` | `/periodic/daily/{date}` | 获取指定日期的日报内容。 | **Path**: `{date}` - 日期，格式为 `YYYY-MM-DD`。 | `curl -H "Authorization: Bearer YOUR_API_KEY" http://127.0.0.1:27123/periodic/daily/2025-10-01` |
| `POST` | `/periodic/weekly/` | 创建或打开本周的周报。 | **Body** (可选): JSON 对象，用于写入内容。 | `curl -X POST -H "Authorization: Bearer YOUR_API_KEY" http://127.0.0.1:27123/periodic/weekly/` |

*(注：`monthly`, `quarterly`, `yearly` 的操作与 `daily` 和 `weekly` 类似，此处不再赘述。)*

---

### Search (搜索)

| Method | Endpoint | Description | Parameters | Example Call |
| :--- | :--- | :--- | :--- | :--- |
| `POST` | `/search/` | 在 Vault 中执行一次搜索查询。 | **Body**: JSON 对象，至少包含 `query` 字段。其他可选字段如 `tag`, `path` 等。 | `curl -X POST -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"query": "n8n integration"}' http://127.0.0.1:27123/search/` |

---

### Dataview (Dataview 插件交互)

此功能需要您已安装并配置 `Dataview` 插件。

| Method | Endpoint     | Description       | Parameters                                         | Example Call                                                                                                                                                     |
| :----- | :----------- | :---------------- | :------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `POST` | `/dataview/` | 执行一次 Dataview 查询。 | **Body**: JSON 对象，包含 `query` 字段，内容为 Dataview 查询语句。 | `curl -X POST -H "Authorization: Bearer YOUR_API_KEY" -H "Content-Type: application/json" -d '{"query": "LIST FROM #project"}' http://127.0.0.1:27123/dataview/` |