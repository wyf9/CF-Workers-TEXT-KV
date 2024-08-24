# 文本文件储存器 CF-Workers-TEXT-KV

CF-Workers-TEXT-KV 是一个在 Cloudflare Workers 上运行的无服务器应用程序,可以将文本文件存储到 Cloudflare Workers KV 键值存储中,并且可以通过 URL 请求读取或更新这些文本文件。它提供了一个安全的方式来管理和访问您的文本文件,同时利用了 Cloudflare 的全球分布式网络。

## Mod

Mod by @wyf9.

- 移除了配置页面的显示和修改api, 使得只能从 Cloudflare Dashboard 进行操作, 增加安全性
- 修改使用说明

## 功能特性

- **文本文件存储**: 您可以将任何文本文件存储到 Cloudflare Workers KV 键值存储中,包括纯文本、JSON、XML 等格式。
- **通过 URL 读取文件**: 只需通过构造合适的 URL,就可以读取存储在 KV 中的文本文件内容。
~~- **通过 URL 更新文件**: 您可以使用 URL 查询参数将新的文本内容上传到 KV,从而实现文件的更新。~~
- **Base64 编码支持**: 支持使用 Base64 编码的方式上传和下载文件,以应对某些特殊字符场景。
- **安全访问控制**: 通过设置 token 参数,可以限制只有拥有正确密钥的请求才能访问您的文件。从 Cloudflare 控制台创建/更新文件，增加安全性。
- ~~**在线一键上传**: 直接在线上传可选明文、密文两种方式。~~

## 使用说明 

1. **部署到 Cloudflare Workers**

  将项目代码部署到您的 Cloudflare Workers 服务。您需要先在 Cloudflare 上创建一个 Workers 项目,然后将 `worker.js` 文件的内容复制粘贴到 Workers 编辑器中。

2. **创建 KV 命名空间**

  在您的 Cloudflare Workers 项目中,创建一个新的 `KV` 命名空间,用于存储文本文件。记下这个 KV 命名空间的名称,因为您需要将它绑定到 Workers 上。

3. **设置 TOKEN 变量**

  - 为了增加安全性,您需要设置一个 TOKEN 变量,作为访问文件的密钥。在 Cloudflare Workers 的环境变量设置中,添加一个名为 `TOKEN` 的变量,并为其赋予一个安全的值。
  - 默认 TOKEN 为：`@`

4. **设置 KV 变量**

在环境变量设置页中找到 KV 命名空间绑定，增加绑定:

- 变量: `KV`
- 命名空间: 选择在第 2 步中创建的 KV 命名空间

~~5. **访问配置页面**~~

~~例如 您的workers项目域名为：`txt.yixiu.workers.dev` , token值为 `@yixiu`；~~
~~- 访问 `https://您的Workers域名/config?token=您的TOKEN` 或 `https://您的Workers域名/您的TOKEN`，您将看到一个配置页面，其中包含了使用说明和下载脚本的链接。~~
~~- 你的项目配置页则为：~~
~~```url~~
~~https://txt.yixiu.workers.dev/config?token=@yixiu~~
~~或~~
~~https://txt.yixiu.workers.dev/@yixiu~~
~~```~~

~~6. **上传文件**~~

~~- 直接在线上传可选明文、密文两种方式~~
~~- **注意：因为URL长度限制，如果保存内容过长则只能通过直接编辑`KV`对应文件内容来实现大文件的修改保存。**~~

6. **上传/更新文件**

您可以使用 Cloudflare Dashboard 修改 KV 命名空间的内容, 同时支持文件上传或直接编辑等。

编辑时的 `键` 为文件名，`值` 为文件内容。

> 可以直接使用 `https://您的Workers域名/@manage` 快速跳转到 Cloudflare Dashboard 的 KV 命名空间列表。

7. **通过 URL 访问文件**

例如 您的workers项目域名为：`txt.yixiu.workers.dev` , token值为 `test` , 需要访问的文件名为 `ip.txt`；
  - 构造 URL 的格式为 `https://您的Workers域名/文件名?token=您的TOKEN`。您就可以在浏览器中查看该文件的内容了。
  - 你的访问地址则为： `https://txt.yixiu.workers.dev/ip.txt?token=test`。

~~8. **简单的更新文件内容**~~

~~要更新某个文件的内容,可以使用 URL 查询参数 `text` 或 `b64` 来指定新的文本内容或 Base64 编码后的内容。URL 的格式为:~~
~~```url~~
~~https://您的Workers域名/文件名?token=您的TOKEN&text=新文本内容~~
~~或~~
~~https://您的Workers域名/文件名?token=您的TOKEN&b64=Base64编码的新文本内容~~
~~```~~
~~Workers 会自动将新内容存储到对应的文件中。~~

通过这个无服务器应用,您可以方便地在 Cloudflare 的分布式网络上存储和管理文本文件,同时享受高性能和安全可靠的优势。欢迎使用 CF-Workers-TEXT-KV!
